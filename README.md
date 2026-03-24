# drawio

A [Cortex Code](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code) skill for generating draw.io diagrams from natural language prompts.

## What it does

- Generates native `.drawio` files (mxGraphModel XML) from plain-English descriptions
- Supports flowcharts, architecture diagrams, ER diagrams, sequence diagrams, network diagrams, mockups, and more
- Exports to PNG, SVG, or PDF with embedded diagram XML (remains editable in draw.io)
- Includes branded SVG icons for common data tools (Snowflake, Airflow, dbt, Kafka, Spark, Tableau, etc.)
- Smart discovery mode: queries live Snowflake metadata to generate architecture diagrams from actual account objects
- Adds annotation boxes to flag technical unknowns and business questions

## Installation

Copy the `drawio` folder into your Cortex Code skills directory:

```
~/.snowflake/cortex/skills/drawio/
```

## Structure

```
drawio/
  SKILL.md                        # Main skill definition
  references/
    xml-reference.md              # draw.io XML styles, edge routing, containers
    icons.md                      # SVG icon catalog for data tools
    smart-discovery.md            # Snowflake metadata discovery workflow
    annotations.md                # Question box templates for diagrams
```

## Usage

Once installed, Cortex Code automatically invokes this skill when you ask it to create or design a diagram. Examples:

- "Draw a flowchart for user authentication"
- "Create an architecture diagram for our ETL pipeline"
- "Generate a PNG diagram of the medallion architecture"
- "Diagram my Snowflake schema using live metadata"
