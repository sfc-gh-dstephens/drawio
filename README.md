# drawio

A [Cortex Code](https://docs.snowflake.com/en/user-guide/cortex-code/cortex-code) skill for generating draw.io diagrams from natural language prompts.

## What it does

- Generates native `.drawio` files (mxGraphModel XML) from plain-English descriptions
- Supports flowcharts, architecture diagrams, ER diagrams, sequence diagrams, network diagrams, mockups, and more
- Exports to PNG, SVG, or PDF with embedded diagram XML (remains editable in draw.io)
- Uses color-coded shapes for tool/service representation with a built-in category color system
- Adds annotation boxes to flag technical unknowns and business questions

## Three Modes

1. **Image to Diagram** - Provide a screenshot or image and recreate it as an editable `.drawio` file
2. **Proposed Snowflake Architecture** - Design a new Snowflake-centric workflow for a specific use case, focused on data flow and Snowflake features (not medallion patterns)
3. **Current + Future State** - Describe the customer's existing data stack; get TWO diagrams: current state and a recommended Snowflake-optimized future state

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
    annotations.md                # Question box templates for diagrams
```

## Usage

Once installed, Cortex Code automatically invokes this skill when you ask it to create or design a diagram. Examples:

- "Draw a flowchart for user authentication"
- "Create an architecture diagram for our ETL pipeline"
- "Design a customer intelligence architecture on Snowflake"
- "Here's a screenshot of our architecture - recreate it as a drawio file"
- "Build a current and future state diagram for our data stack"
