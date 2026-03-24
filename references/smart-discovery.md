# Smart Discovery Mode

Generate architecture diagrams from live Snowflake metadata. Instead of building diagrams from assumptions, query the account to discover what actually exists.

## Workflow

### Step 1: Scope the discovery

Before querying, ask the user to narrow the scope:
- Which **database(s)** to include? (Don't diagram the entire account)
- Which **schema(s)** within those databases?
- What **layer** of the architecture? (ingestion, transformation, serving, all)
- Any **known tools** in the stack? (Airflow, dbt, Fivetran, etc.)

### Step 2: Run discovery queries

Execute these queries against the active Snowflake connection to inventory objects. Run them in parallel where possible.

**Core objects:**

```sql
SHOW DATABASES;

SHOW SCHEMAS IN DATABASE <db>;

SHOW TABLES IN SCHEMA <db>.<schema>;

SHOW VIEWS IN SCHEMA <db>.<schema>;

SHOW DYNAMIC TABLES IN SCHEMA <db>.<schema>;

SHOW MATERIALIZED VIEWS IN SCHEMA <db>.<schema>;
```

**Pipeline objects:**

```sql
SHOW TASKS IN SCHEMA <db>.<schema>;

SHOW STREAMS IN SCHEMA <db>.<schema>;

SHOW PIPES IN SCHEMA <db>.<schema>;

SHOW STAGES IN SCHEMA <db>.<schema>;
```

**Relationships and dependencies:**

```sql
-- Task dependency graph
SELECT name, predecessors, schedule, state
FROM TABLE(INFORMATION_SCHEMA.TASK_DEPENDENTS('<db>.<schema>.<root_task>', true));

-- Dynamic table lineage (what tables feed each DT)
SELECT name, text AS query_text, target_lag, refresh_mode
FROM INFORMATION_SCHEMA.DYNAMIC_TABLES
WHERE schema_name = '<schema>';

-- Stream sources (what table each stream tracks)
SELECT stream_name, table_name, type
FROM INFORMATION_SCHEMA.STREAMS
WHERE stream_schema = '<schema>';
```

**Object counts (for layout planning):**

```sql
SELECT
  TABLE_TYPE,
  COUNT(*) as cnt
FROM <db>.INFORMATION_SCHEMA.TABLES
WHERE TABLE_SCHEMA = '<schema>'
GROUP BY TABLE_TYPE;
```

### Step 3: Detect patterns

Analyze the discovered objects for common architectural patterns:

**Medallion / layered naming:**
- Look for schema or table prefixes: `raw_`, `stg_`, `bronze_`, `silver_`, `gold_`, `dim_`, `fact_`, `rpt_`, `agg_`
- Look for schema names: `RAW`, `STAGING`, `CURATED`, `ANALYTICS`, `PRESENTATION`
- Group objects by detected layer

**ETL/ELT flow patterns:**
- `STAGE -> PIPE -> RAW table` = ingestion pipeline
- `STREAM on table A -> TASK -> table B` = CDC pipeline
- `DYNAMIC TABLE reading from X` = declarative transformation
- `TASK with SQL referencing table A writing to table B` = scheduled transform

**External tool indicators:**
- Tables with `_AIRBYTE_` or `_FIVETRAN_` metadata columns = connector-ingested
- Tables with `DBT_UPDATED_AT` or `_DBT_SOURCE_RELATION` = dbt-managed
- Task names containing `AIRFLOW` or warehouse names like `AIRFLOW_WH` = Airflow-orchestrated

### Step 4: Build the diagram

Organize discovered objects into a left-to-right flow:

```
[External Sources] -> [Ingestion] -> [Raw/Bronze] -> [Transformed/Silver] -> [Business/Gold] -> [Consumers]
```

**Layout rules:**
- **Group by schema or detected layer** using swimlane containers
- **Use icons from `references/icons.md`** for recognized tools (Snowflake for warehouses, dbt for dbt-managed models, Airflow for orchestrated tasks, etc.)
- **Use `shape=cylinder3`** for tables and views (database objects)
- **Use dashed edges** for inferred/uncertain connections
- **Use solid edges** for confirmed connections (stream->task, task predecessors, DT lineage)
- **Add annotations** per `references/annotations.md` for unknowns

**Node naming:**
- Show `SCHEMA.TABLE_NAME` for cross-schema references
- Show just `TABLE_NAME` when everything is in one schema
- Truncate very long names with ellipsis

**Sizing guidance:**
- Up to 10 objects per layer: show all individually
- 10-25 objects per layer: group related objects, show key ones individually
- 25+ objects per layer: use a summary container with count label, call out key objects only

### Step 5: Identify gaps and annotate

After building the diagram from metadata, identify what CANNOT be determined from Snowflake alone and add sticky note annotations (see `references/annotations.md`):

- **External sources**: Stages exist but what system writes to them?
- **External consumers**: Gold/analytics tables exist but what reads them?
- **Orchestration**: Are tasks managed by Snowflake natively, or triggered externally?
- **Data quality**: Are there quality checks between layers?
- **Ownership**: Who owns each pipeline segment?
- **SLAs**: What are the freshness requirements?

## Example output structure

A discovered architecture might produce a diagram with:

```
[S3 Stage?] -> [PIPE: load_events] -> [RAW.EVENTS] --(stream)--> [TASK: transform_events] -> [CURATED.EVENTS_CLEANED]
                                       [RAW.USERS]  --(DT)-----> [CURATED.USER_PROFILES]   --(DT)--> [ANALYTICS.USER_360]
                                                                                                        |
                                                                                              [Tableau? Power BI?]
```

With sticky notes:
- Near S3 Stage: "What system writes event data to this stage?"
- Near ANALYTICS schema: "What BI tool consumes these tables?"
- Near TASK: "Is this task triggered by Airflow or runs on native schedule?"
