---
name: drawio
description: Always use when user asks to create, generate, draw, or design a diagram, flowchart, architecture diagram, ER diagram, sequence diagram, class diagram, network diagram, mockup, wireframe, or UI sketch, or mentions draw.io, drawio, drawoi, .drawio files, or diagram export to PNG/SVG/PDF.
---

# Draw.io Diagram Skill

Generate draw.io diagrams as native `.drawio` files. Optionally export to PNG, SVG, or PDF with the diagram XML embedded (so the exported file remains editable in draw.io).

This skill includes:
- **Annotations** (sticky notes) to flag questions, risks, and unknowns - see `references/annotations.md`

## Workflow

### Step 1: Determine Use Case

Ask the user which mode they need:

1. **Image to Diagram** - Provide a screenshot or image and recreate it as a `.drawio` file
2. **Proposed Snowflake Architecture** - Design a new Snowflake-centric workflow for a specific use case (e.g., customer intelligence, real-time analytics, ML pipeline). Focus is on data flow, Snowflake features, and how data gets consumed - NOT on medallion layer patterns
3. **Current + Future State** - Describe the customer's existing data stack; produce TWO diagrams: a current-state diagram showing what they have today, and a recommended Snowflake-optimized future-state diagram

### Step 2: Gather Context

After the user selects a mode, ask:

> "Do you have any notes, files, or additional context you'd like to share? This could be meeting notes, architecture docs, a file path, screenshots, or anything that helps me understand the components and relationships."

- If the user provides a **file path**, read the file and extract relevant data points (tool names, architecture details, pain points, goals).
- If the user provides an **image** (Mode 1), read and analyze the image to identify components, connections, labels, and layout.
- If the user provides **text notes**, parse them for tool names, services, data flows, and any constraints or requirements.
- If the user has **no additional context**, proceed with what they've already described.

**IMPORTANT**: Do not assume architecture details. If any of the following are unclear, ask the user before building the diagram. Each mode has specific questions listed below.

### Step 3: Generate the Diagram

Follow the mode-specific workflow below, then proceed to "How to create a diagram" for file generation and export.

---

## Mode 1: Image to Diagram

1. **Receive the image**: User provides an image path or screenshot.
2. **Analyze the image**: Use the Read tool to view the image. Identify:
   - All labeled components (boxes, icons, services, databases)
   - Connections and arrows between components (direction, labels)
   - Groupings or swim lanes
   - Layout orientation (left-to-right, top-to-bottom, hub-and-spoke)
   - Color schemes and styling
3. **Determine diagram type**: Based on analysis, choose the appropriate draw.io shapes and layout (flowchart, architecture, ER, org chart, etc.).
4. **Build the XML**: Map each visual component to mxCell elements. Reproduce the layout as closely as possible using bounding box coordinates. Use color-coded rounded rectangles for tool/service nodes (see Tool Representation below).
5. **Generate the `.drawio` file** following the standard creation flow below.

---

## Mode 2: Proposed Snowflake Architecture

Design a new Snowflake-centric architecture for a specific use case. The focus is on **data flow and Snowflake features** - how data enters, gets processed, enriched, and consumed. This is NOT a medallion/layering exercise; it is a workflow diagram showing which Snowflake capabilities apply where.

### Granularity Check

Before gathering context, ask the user what level of detail this diagram is for:

| Option | Description |
|--------|-------------|
| **Executive Overview** | Business zones and outcomes only; no specific Snowflake feature names |
| **Standard Architecture** | All key Snowflake features named as nodes, full data flow |
| **POC Blueprint** | Tables, views, policies, specific configs — build-ready level of detail |
| **Discovery / Whiteboard** | Rough draft with heavy annotations, designed to spark conversation |
| **Demo-ready** | Polished, presentation-quality, suitable to show directly to a customer |

Adapt the diagram's depth, label specificity, and annotation density based on the chosen level. For **Executive Overview**, omit Snowflake-specific feature names and use business-friendly zone labels. For **POC Blueprint**, include object names, policy names, and config notes. For **Discovery / Whiteboard**, maximize annotation boxes and flag all unknowns.

### Context Gathering (ask what you don't already know)

Work through these questions with the user. Skip any that are already answered from notes/context provided. Do not assume answers.

**1. Use case / goal**
> "What is the primary use case or business outcome? (e.g., customer intelligence, real-time fraud detection, ML-powered recommendations, IoT analytics)"

**2. Data sources**
> "What data sources feed this workflow? (e.g., Salesforce, Postgres CDC, Kafka stream, S3 files, API, Snowflake Marketplace). If you're not sure, tell me what kind of data you need and I can recommend sources."

**3. Data characteristics**
> "Is the data mostly batch, streaming/real-time, or a mix? How frequently does it need to refresh?"

**4. Processing / enrichment**
> "What needs to happen to the data? (e.g., joins, dedup, aggregation, ML scoring, sentiment analysis, document parsing, geocoding). Are there specific Snowflake features you want to use, or should I recommend?"

**5. Consumption / output**
> "How should the end result be consumed? (e.g., Streamlit dashboard, Cortex Agent natural language Q&A, BI tool like Tableau/Sigma, API endpoint, data share to another account, reverse ETL to CRM)"

**6. Governance / security (optional)**
> "Any governance requirements? (e.g., PII masking, row-level security, data quality checks, audit logging)"

### Building the Diagram

Once context is gathered, build the architecture as a **data flow diagram** organized around Snowflake features:

- **Layout**: Left-to-right flow from sources → ingestion → processing/enrichment → serving/consumption
- **Snowflake features as first-class nodes**: Show specific Snowflake capabilities (Snowpipe Streaming, Dynamic Tables, Cortex AI Functions, Cortex Search, Cortex Agents, Streams + Tasks, Snowpark, etc.) as labeled nodes in the flow, not hidden inside generic containers
- **Data flow edges**: Label edges with what data moves between stages (e.g., "raw events", "enriched profiles", "sentiment scores")
- **External systems**: Show non-Snowflake systems (data sources, BI tools, APIs) at the edges of the diagram
- **Annotations**: Add annotation boxes for open questions or recommendations per `references/annotations.md`

### Snowflake Feature Reference

Use this to select the right Snowflake feature for each part of the workflow:

| Need | Snowflake Feature |
|------|-------------------|
| Batch file ingestion | Snowpipe (auto-ingest from stage) |
| Real-time / streaming ingestion | Snowpipe Streaming, Kafka Connector |
| Change data capture | Streams + Tasks |
| Declarative transformations | Dynamic Tables (define target as SQL, auto-refreshes) |
| Programmatic transforms (Python/Java) | Snowpark |
| SQL-based transforms with orchestration | dbt on Snowflake, Snowflake Tasks + DAGs |
| Sentiment analysis, classification, extraction | Cortex AI Functions (SENTIMENT, CLASSIFY, EXTRACT) |
| Text summarization | Cortex SUMMARIZE, Cortex COMPLETE |
| Document / PDF parsing | Cortex PARSE_DOCUMENT |
| Semantic search over unstructured data | Cortex Search |
| Natural language Q&A interface | Cortex Agents |
| ML model training | Snowpark ML, Snowflake ML Model Registry |
| ML model inference in SQL | Model Registry (log_model + SQL inference) |
| Interactive dashboards (internal) | Streamlit in Snowflake |
| BI / reporting | Snowsight Dashboards, or connect Tableau / Sigma / Power BI |
| Share data across accounts | Secure Data Sharing, Private Listings |
| Enrich with third-party data | Snowflake Marketplace |
| PII detection + masking | Horizon Classification + Tag-based Masking Policies |
| Row-level security | Row Access Policies |
| Data quality monitoring | Data Metric Functions (DMFs) |
| Containerized workloads | Snowpark Container Services |

---

## Mode 3: Current State + Future State

This mode produces **two `.drawio` files**: one faithfully representing the customer's **existing** architecture (what they have today, regardless of platform), and one showing a recommended **Snowflake-optimized** future state that replaces or consolidates their current tools.

This is different from Mode 2. Mode 2 designs a new Snowflake workflow from scratch for a use case. Mode 3 starts from a customer's real current stack and maps it forward.

### Context Gathering (ask what you don't already know)

Work through these questions with the user. Skip any that are already answered from notes/context provided. Do not assume answers.

**1. Data sources**
> "What data sources does the customer use today? (e.g., Postgres, MySQL, Salesforce, SAP, S3 files, Kafka, APIs)"

**2. Ingestion / ETL tools**
> "How does data get into their current platform? (e.g., Fivetran, Airbyte, Informatica, custom scripts, SSIS, Talend)"

**3. Data platform / warehouse / lake**
> "What is the current data platform? (e.g., on-prem SQL Server, Databricks lakehouse, Redshift, BigQuery, Hadoop/HDFS, Snowflake with limited usage)"

**4. Transformation / processing**
> "How do they transform data? (e.g., Spark jobs, stored procedures, dbt, Airflow DAGs, Informatica mappings, manual SQL)"

**5. Orchestration**
> "What orchestrates their pipelines? (e.g., Airflow, Control-M, Autosys, cron, Jenkins, Azure Data Factory)"

**6. ML / AI (if applicable)**
> "Any ML or AI workloads? (e.g., SageMaker, Databricks ML, custom Python, no ML currently)"

**7. BI / reporting / consumption**
> "How is data consumed? (e.g., Tableau, Power BI, Looker, custom dashboards, Excel exports, APIs)"

**8. Governance and security**
> "How do they handle governance? (e.g., manual access controls, external catalog, no formal governance)"

**9. Pain points / goals**
> "What are the main pain points or goals driving this conversation? (e.g., too many tools, slow pipelines, no real-time, compliance gaps, cost reduction, vendor consolidation)"

### Generating Diagram 1: Current State

Build a pipeline/architecture diagram that faithfully represents the customer's existing stack as described. Use color-coded rounded rectangles for tool/service nodes (see Tool Representation below). Add annotation boxes per `references/annotations.md` to flag technical unknowns and business questions.

### Mapping to Snowflake Recommendations

Analyze the current stack and recommend Snowflake-native replacements using this table:

| Category | Common Current Tools | Recommended Snowflake Feature |
|----------|---------------------|-------------------------------|
| **Data Ingestion** | Fivetran, Airbyte, Stitch, custom scripts | Snowpipe, Snowpipe Streaming, Kafka Connector, Dynamic Tables |
| **Change Data Capture** | Debezium, Oracle GoldenGate, AWS DMS | Streams + Tasks, Dynamic Tables |
| **Transformation** | Spark, Airflow + SQL, Informatica, Talend | Snowpark (Python/Java/Scala), dbt on Snowflake, Dynamic Tables |
| **Orchestration** | Airflow, Dagster, Prefect, Luigi | Snowflake Tasks + DAGs, Snowpark Task Graph |
| **ML / AI** | SageMaker, Vertex AI, Databricks ML, custom Python | Snowpark ML, Cortex AI Functions, Cortex Fine-Tuning, ML Model Registry |
| **LLM / GenAI** | OpenAI API, Langchain, custom RAG | Cortex LLM Functions, Cortex Search, Cortex Agents |
| **BI / Reporting** | Tableau, Looker, Power BI, Metabase | Streamlit in Snowflake, Snowsight Dashboards (keep existing BI tools as optional) |
| **Data Sharing** | SFTP, API endpoints, email exports | Secure Data Sharing, Snowflake Marketplace, Private Listings |
| **Governance** | Manual tagging, external catalogs, custom RBAC | Horizon (Object Tagging, Classification, Lineage), Tag-based Masking/Row Access Policies |
| **Data Quality** | Great Expectations, dbt tests, custom checks | Data Metric Functions (DMFs), Alert + Notification Integrations |
| **Storage** | S3/GCS/ADLS data lakes, Delta Lake, Hudi | Snowflake-managed tables, Apache Iceberg tables (open format) |
| **Compute** | EMR, Dataproc, Databricks clusters | Snowflake Warehouses (auto-scale/suspend), Snowpark Container Services |

### Generating Diagram 2: Future State

Build a second architecture diagram showing the recommended Snowflake-optimized stack. Use the Data Platform color (`#29B5E8`) for all Snowflake-native components to visually distinguish them. Add annotation boxes noting key improvements and migration considerations.

### Delivering Results

When presenting the two diagrams, provide:
1. The file paths for both `.drawio` files (e.g., `current-state.drawio` and `future-state.drawio`)
2. A summary table of key changes (current tool -> recommended replacement -> reason)
3. Export/open instructions

---

## How to create a diagram

1. **Generate draw.io XML** in mxGraphModel format for the requested diagram
2. **Write the XML** to a `.drawio` file in the current working directory using the Write tool
3. **If the user requested an export format** (png, svg, pdf), locate the draw.io CLI (see below), export with `--embed-diagram`, then delete the source `.drawio` file. If the CLI is not found, keep the `.drawio` file and tell the user they can install the draw.io desktop app to enable export, or open the `.drawio` file directly
4. **Open the result** — the exported file if exported, or the `.drawio` file otherwise. If the open command fails, print the file path so the user can open it manually

## Choosing the output format

Check the user's request for a format preference. Examples:

- `/drawio create a flowchart` → `flowchart.drawio`
- `/drawio png flowchart for login` → `login-flow.drawio.png`
- `/drawio svg: ER diagram` → `er-diagram.drawio.svg`
- `/drawio pdf architecture overview` → `architecture-overview.drawio.pdf`

If no format is mentioned, just write the `.drawio` file and open it in draw.io. The user can always ask to export later.

### Supported export formats

| Format | Embed XML | Notes |
|--------|-----------|-------|
| `png` | Yes (`-e`) | Viewable everywhere, editable in draw.io |
| `svg` | Yes (`-e`) | Scalable, editable in draw.io |
| `pdf` | Yes (`-e`) | Printable, editable in draw.io |
| `jpg` | No | Lossy, no embedded XML support |

PNG, SVG, and PDF all support `--embed-diagram` — the exported file contains the full diagram XML, so opening it in draw.io recovers the editable diagram.

## draw.io CLI

The draw.io desktop app includes a command-line interface for exporting.

### Locating the CLI

First, detect the environment, then locate the CLI accordingly:

#### WSL2 (Windows Subsystem for Linux)

WSL2 is detected when `/proc/version` contains `microsoft` or `WSL`:

```bash
grep -qi microsoft /proc/version 2>/dev/null && echo "WSL2"
```

On WSL2, use the Windows draw.io Desktop executable via `/mnt/c/...`:

```bash
DRAWIO_CMD=`/mnt/c/Program Files/draw.io/draw.io.exe`
```

The backtick quoting is required to handle the space in `Program Files` in bash.

If draw.io is installed in a non-default location, check common alternatives:

```bash
# Default install path
`/mnt/c/Program Files/draw.io/draw.io.exe`

# Per-user install (if the above does not exist)
`/mnt/c/Users/$WIN_USER/AppData/Local/Programs/draw.io/draw.io.exe`
```

#### macOS

```bash
/Applications/draw.io.app/Contents/MacOS/draw.io
```

#### Linux (native)

```bash
drawio   # typically on PATH via snap/apt/flatpak
```

#### Windows (native, non-WSL2)

```
"C:\Program Files\draw.io\draw.io.exe"
```

Use `which drawio` (or `where drawio` on Windows) to check if it's on PATH before falling back to the platform-specific path.

### Export command

```bash
drawio -x -f <format> -e -b 10 -o <output> <input.drawio>
```

**WSL2 example:**

```bash
`/mnt/c/Program Files/draw.io/draw.io.exe` -x -f png -e -b 10 -o diagram.drawio.png diagram.drawio
```

Key flags:
- `-x` / `--export`: export mode
- `-f` / `--format`: output format (png, svg, pdf, jpg)
- `-e` / `--embed-diagram`: embed diagram XML in the output (PNG, SVG, PDF only)
- `-o` / `--output`: output file path
- `-b` / `--border`: border width around diagram (default: 0)
- `-t` / `--transparent`: transparent background (PNG only)
- `-s` / `--scale`: scale the diagram size
- `--width` / `--height`: fit into specified dimensions (preserves aspect ratio)
- `-a` / `--all-pages`: export all pages (PDF only)
- `-p` / `--page-index`: select a specific page (1-based)

### Opening the result

| Environment | Command |
|-------------|---------|
| macOS | `open <file>` |
| Linux (native) | `xdg-open <file>` |
| WSL2 | `cmd.exe /c start "" "$(wslpath -w <file>)"` |
| Windows | `start <file>` |

**WSL2 notes:**
- `wslpath -w <file>` converts a WSL2 path (e.g. `/home/user/diagram.drawio`) to a Windows path (e.g. `C:\Users\...`). This is required because `cmd.exe` cannot resolve `/mnt/c/...` style paths.
- The empty string `""` after `start` is required to prevent `start` from interpreting the filename as a window title.

**WSL2 example:**

```bash
cmd.exe /c start "" "$(wslpath -w diagram.drawio)"
```

## File naming

- Use a descriptive filename based on the diagram content (e.g., `login-flow`, `database-schema`)
- Use lowercase with hyphens for multi-word names
- For export, use double extensions: `name.drawio.png`, `name.drawio.svg`, `name.drawio.pdf` — this signals the file contains embedded diagram XML
- After a successful export, delete the intermediate `.drawio` file — the exported file contains the full diagram

## XML format

A `.drawio` file is native mxGraphModel XML. Always generate XML directly — Mermaid and CSV formats require server-side conversion and cannot be saved as native files.

### Basic structure

Every diagram must have this structure:

```xml
<mxGraphModel adaptiveColors="auto">
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>
    <!-- Diagram cells go here with parent="1" -->
  </root>
</mxGraphModel>
```

- Cell `id="0"` is the root layer
- Cell `id="1"` is the default parent layer
- All diagram elements use `parent="1"` unless using multiple layers

Consult `references/xml-reference.md` for common styles, style properties, edge routing details (including waypoints), and container/group examples.

### Multi-line labels

For cells with multi-line text:
- Set `html=1` in the cell style
- Use `<br>` for line breaks in the `value` attribute
- **Never use `&#xa;` in attribute values** — XML attribute value normalization causes it to render as the literal string `&#xa;` in draw.io instead of a line break

**Correct:**
```xml
<mxCell value="Cortex Analyst<br>(Text-to-SQL)" style="rounded=1;html=1;whiteSpace=wrap;..." vertex="1" parent="1">
```

**Wrong:**
```xml
<mxCell value="Cortex Analyst&#xa;(Text-to-SQL)" style="rounded=1;whiteSpace=wrap;..." vertex="1" parent="1">
```

## Edge routing

**CRITICAL: Every edge `mxCell` must contain a `<mxGeometry relative="1" as="geometry" />` child element**, even when there are no waypoints. Self-closing edge cells (e.g. `<mxCell ... edge="1" ... />`) are invalid and will not render correctly. Always use the expanded form:
```xml
<mxCell id="e1" edge="1" parent="1" source="a" target="b" style="...">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

- Use `edgeStyle=orthogonalEdgeStyle` for right-angle connectors (most common)
- **Space nodes generously** — prefer 200px horizontal / 120px vertical gaps
- **Leave room for arrowheads** — at least 20px of straight segment before the target
- Add explicit **waypoints** when edges would overlap
- Align all nodes to a grid (multiples of 10)
- **Edge labels**: Do NOT wrap edge labels in HTML markup to reduce font size. The default font size for edge labels is already 11px (vs 12px for vertices), so they are already smaller. Just set the `value` attribute directly.

See `references/xml-reference.md` for full edge routing and container guidance.

## Containers and groups

Use parent-child containment (`parent="containerId"`) for nested elements — do **not** just stack shapes. Children use **relative coordinates** within the container. See `references/xml-reference.md` for container types, rules, and examples.

## Tool Representation

Represent tools and services using **color-coded rounded rectangles** with white bold text. Assign colors by tool category and include a **color key** in the diagram corner listing only the categories that appear.

| Category | Fill Color | Examples |
|----------|-----------|----------|
| Ingestion | `#0073FF` | Fivetran, Airbyte, Stitch |
| Orchestration | `#017CEE` | Airflow, Prefect, Dagster |
| Transform | `#FF694B` | dbt, Spark, Python scripts |
| Analytics / BI | `#E97627` | Tableau, Power BI, Looker, Sigma |
| Streaming | `#231F20` | Kafka, Kinesis, Snowpipe Streaming |
| Cloud / CSP | `#0089D6` | AWS S3, Azure, GCS |
| ML / AI | `#FF3621` | Databricks, SageMaker, Snowpark ML |
| App Framework | `#FF4B4B` | Streamlit, Dash, Gradio |
| Data Platform | `#29B5E8` | Snowflake |

**Style for tool nodes:**
```
rounded=1;whiteSpace=wrap;fillColor=#COLOR;fontColor=#FFFFFF;strokeColor=#COLOR;fontStyle=1;fontSize=12;
```

Replace `#COLOR` with the category color from the table above.

**When to use colored rectangles vs native shapes**: Use colored rectangles for external tools, platforms, and services. Use draw.io native shapes (`cylinder3`, `rounded=1` with default colors, etc.) for Snowflake-internal objects like tables, views, and stages.

## Annotations (question boxes)

When a diagram warrants discovery questions, add **two consolidated boxes** below or beside the main diagram. See `references/annotations.md` for full style definitions and question templates.

- **Technical Questions** (light yellow box) — Architecture unknowns: data sources, orchestration, quality checks, consumers, SLAs, ownership, security
- **Business Case / Sales Questions** (light purple box) — SE strategic: competitive displacement, Snowflake feature fit, Marketplace enrichment, operational pain points, consolidation opportunities

Keep questions as bulleted lists inside each box. Do **not** draw connector lines from individual questions to diagram components — it clutters the diagram. The questions should be self-explanatory by referencing the component name inline (e.g. "Is Airflow the only orchestrator, or are native Tasks also used?").

## Dark mode colors

draw.io supports automatic dark mode rendering. How colors behave depends on the property:

- **`strokeColor`, `fillColor`, `fontColor`** default to `"default"`, which renders as black in light theme and white in dark theme. When no explicit color is set, colors adapt automatically.
- **Explicit colors** (e.g. `fillColor=#DAE8FC`) specify the light-mode color. The dark-mode color is computed automatically by inverting the RGB values (blending toward the inverse at 93%) and rotating the hue by 180° (via `mxUtils.getInverseColor`).
- **`light-dark()` function** — To specify both colors explicitly, use `light-dark(lightColor,darkColor)` in the style string, e.g. `fontColor=light-dark(#7EA6E0,#FF0000)`. The first argument is used in light mode, the second in dark mode.

To enable dark mode color adaptation, the `mxGraphModel` element must include `adaptiveColors="auto"`.

When generating diagrams, you generally do not need to specify dark-mode colors — the automatic inversion handles most cases. Use `light-dark()` only when the automatic inverse color is unsatisfactory.

## Style reference

For the complete draw.io style reference: https://www.drawio.com/doc/faq/drawio-style-reference.html

For the XML Schema Definition (XSD): https://www.drawio.com/assets/mxfile.xsd

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| draw.io CLI not found | Desktop app not installed or not on PATH | Keep the `.drawio` file and tell the user to install the draw.io desktop app, or open the file manually |
| Export produces empty/corrupt file | Invalid XML (e.g. double hyphens in comments, unescaped special characters) | Validate XML well-formedness before writing; see the XML well-formedness section below |
| Diagram opens but looks blank | Missing root cells `id="0"` and `id="1"` | Ensure the basic mxGraphModel structure is complete |
| Edges not rendering | Edge mxCell is self-closing (no child mxGeometry element) | Every edge must have `<mxGeometry relative="1" as="geometry" />` as a child element |
| File won't open after export | Incorrect file path or missing file association | Print the absolute file path so the user can open it manually |

## CRITICAL: XML well-formedness

- **NEVER use double hyphens (`--`) inside XML comments.** `--` is illegal inside `<!-- -->` per the XML spec and causes parse errors. Use single hyphens or rephrase.
- Escape special characters in attribute values: `&amp;`, `&lt;`, `&gt;`, `&quot;`
- Always use unique `id` values for each `mxCell`
