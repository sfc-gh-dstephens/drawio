# Annotations - Question Boxes

Add discovery questions to diagrams using **two consolidated boxes** positioned below or beside the main diagram. No connector lines to individual components — keep it clean.

## When to add question boxes

- **Smart discovery mode**: Always add after generating from Snowflake metadata
- **Customer-facing diagrams**: Flag what needs validation before finalizing
- **Architecture reviews**: Surface risks and opportunities
- **SE engagements**: Identify business cases alongside technical gaps

---

## Box 1: Technical Questions

Architecture unknowns that need answers to complete the picture.

```xml
<mxCell id="tech_box" value="Technical Questions" style="swimlane;startSize=22;fillColor=#FFF2CC;strokeColor=#D6B656;rounded=1;fontSize=12;fontStyle=1;align=left;" vertex="1" parent="1">
  <mxGeometry x="20" y="520" width="400" height="160" as="geometry"/>
</mxCell>
<mxCell id="tech_qs" value="- What is the Fivetran sync frequency? Full or incremental?&#10;- Are there data quality checks between Bronze and Silver?&#10;- Is Airflow the only orchestrator, or are native Tasks also used?&#10;- Who are the downstream consumers of the Gold layer?&#10;- What is the freshness SLA for reporting tables?&#10;- Is PII masked before the Silver layer?" style="text;whiteSpace=wrap;fontSize=10;align=left;spacingLeft=8;spacingTop=4;verticalAlign=top;" vertex="1" parent="tech_box">
  <mxGeometry x="5" y="24" width="390" height="130" as="geometry"/>
</mxCell>
```

### Question templates by topic

**Data sources / ingestion**
- What system writes to this stage?
- What is the sync frequency? Full or incremental loads?
- Is this API push or pull-based?

**Orchestration**
- Native Task schedule or external orchestrator?
- What triggers this pipeline to run?
- Is there retry/alerting on failure?

**Data quality**
- Are there quality checks between layers?
- What happens when quality checks fail?
- Is there monitoring for data delays?

**Consumers**
- What downstream tools read from this layer?
- Is this data exposed via Snowflake Sharing?
- What dashboards depend on these tables?

**Ownership and SLAs**
- Who owns this pipeline segment?
- What is the freshness SLA for this table?

**Security and access**
- Who has access to raw data?
- Is PII masked in this layer?
- Are there row-level security policies?

---

## Box 2: Business Case / Sales Questions

Snowflake SE perspective: competitive displacement, feature fit, Marketplace value, and pain points.

```xml
<mxCell id="biz_box" value="Business Case / Sales Questions" style="swimlane;startSize=22;fillColor=#E1D5E7;strokeColor=#9673A6;rounded=1;fontSize=12;fontStyle=1;align=left;" vertex="1" parent="1">
  <mxGeometry x="440" y="520" width="400" height="160" as="geometry"/>
</mxCell>
<mxCell id="biz_qs" value="- dbt running externally — evaluate dbt on Snowflake for consolidation?&#10;- Airflow orchestration — could Snowflake Tasks + DAGs simplify?&#10;- Batch transforms to Gold — candidate for Dynamic Tables?&#10;- Customer dim could be enriched with Marketplace demographics&#10;- 3 external tools = operational overhead — consolidation opportunity&#10;- Campaign data — evaluate Cortex AI for sentiment analysis?" style="text;whiteSpace=wrap;fontSize=10;align=left;spacingLeft=8;spacingTop=4;verticalAlign=top;" vertex="1" parent="biz_box">
  <mxGeometry x="5" y="24" width="390" height="130" as="geometry"/>
</mxCell>
```

### Question templates by topic

**Competitive displacement / migration**
- ML pipeline on Databricks — candidate for Snowpark ML?
- Spark ETL jobs — could Dynamic Tables replace this?
- Airflow orchestration — evaluate Snowflake Tasks for simplification?
- Kafka streaming — could Snowpipe Streaming handle this?
- External data lake on S3 — candidate for Iceberg Tables?
- Separate compute cluster — consolidate into Snowflake warehouses?

**Snowflake feature fit / modernization**
- Manual CDC pattern — candidate for Streams + Dynamic Tables?
- Complex scheduling — could Snowflake Tasks + DAGs simplify?
- Python transforms in external compute — move to Snowpark?
- Document processing pipeline — evaluate Cortex AI functions?
- Data shared across business units — Secure Data Sharing opportunity?
- Row-level security in app layer — native masking policies instead?
- Manual data quality checks — use Snowflake DMFs?

**Data enrichment / Marketplace**
- Customer data — enrich with Marketplace demographics or firmographics?
- Weather-sensitive analytics — Marketplace weather data available
- Financial data joins — third-party feeds on Marketplace
- Is this dataset shared externally? Evaluate Snowflake Listings
- Multiple accounts consuming same data — Secure Sharing vs ETL copies?

**Pain points / operational challenges**
- Multiple ETL tools increase operational complexity — consolidation opportunity
- Batch-only pipeline causes data latency — Snowpipe for near-real-time?
- Cross-cloud data movement adds cost — Snowflake multi-cloud simplifies
- Manual scaling/tuning of compute — Snowflake auto-scaling warehouses
- Data governance spread across tools — centralize in Snowflake Horizon?
- Long-running transforms blocking queries — separate warehouse isolation

---

## Placement rules

- Position both boxes **below the main diagram flow**, side by side
- Use consistent widths (380-420px) for visual balance
- Use `&#10;` for line breaks within the text cell (this works reliably for multiline text in value attributes)
- Prefix each question with `- ` for a bulleted list appearance
- Tailor questions to the specific architecture shown — don't dump the full template list, pick the 4-8 most relevant per box
