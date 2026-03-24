# Icon Library

Referenceable icons for common data tools. Each icon is a URL-encoded SVG embedded directly in the mxCell style.

**IMPORTANT**: Icons use `data:image/svg+xml,` (URL-encoded, NOT base64) because the `;` in `data:image/svg+xml;base64,` conflicts with draw.io's style property delimiter.

## How to use an icon

Place an icon using `shape=image` with `verticalLabelPosition=bottom` so the tool name appears beneath:

```xml
<mxCell id="mynode" value="Snowflake" style="shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,ENCODED_SVG_HERE" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="48" height="48" as="geometry"/>
</mxCell>
```

Recommended size: **48x48** for standard nodes, **36x36** for compact layouts, **64x64** for hero/emphasis nodes.

## Icon Catalog

### Snowflake
- **Color**: #29B5E8
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cg%20stroke%3D%22%2329B5E8%22%20stroke-width%3D%223%22%20stroke-linecap%3D%22round%22%20fill%3D%22none%22%3E%3Cline%20x1%3D%2224%22%20y1%3D%224%22%20x2%3D%2224%22%20y2%3D%2244%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2214%22%20x2%3D%2241.3%22%20y2%3D%2234%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2234%22%20x2%3D%2241.3%22%20y2%3D%2214%22%2F%3E%3Cline%20x1%3D%2224%22%20y1%3D%224%22%20x2%3D%2220%22%20y2%3D%228%22%2F%3E%3Cline%20x1%3D%2224%22%20y1%3D%224%22%20x2%3D%2228%22%20y2%3D%228%22%2F%3E%3Cline%20x1%3D%2224%22%20y1%3D%2244%22%20x2%3D%2220%22%20y2%3D%2240%22%2F%3E%3Cline%20x1%3D%2224%22%20y1%3D%2244%22%20x2%3D%2228%22%20y2%3D%2240%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2214%22%20x2%3D%228%22%20y2%3D%2219%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2214%22%20x2%3D%2211.5%22%20y2%3D%2212.5%22%2F%3E%3Cline%20x1%3D%2241.3%22%20y1%3D%2234%22%20x2%3D%2240%22%20y2%3D%2229%22%2F%3E%3Cline%20x1%3D%2241.3%22%20y1%3D%2234%22%20x2%3D%2236.5%22%20y2%3D%2235.5%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2234%22%20x2%3D%2211.5%22%20y2%3D%2235.5%22%2F%3E%3Cline%20x1%3D%226.7%22%20y1%3D%2234%22%20x2%3D%228%22%20y2%3D%2229%22%2F%3E%3Cline%20x1%3D%2241.3%22%20y1%3D%2214%22%20x2%3D%2236.5%22%20y2%3D%2212.5%22%2F%3E%3Cline%20x1%3D%2241.3%22%20y1%3D%2214%22%20x2%3D%2240%22%20y2%3D%2219%22%2F%3E%3C%2Fg%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2224%22%20r%3D%223%22%20fill%3D%22%2329B5E8%22%2F%3E%3C%2Fsvg%3E`

### Airflow
- **Color**: #017CEE / #00AD46
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2224%22%20r%3D%2222%22%20fill%3D%22none%22%20stroke%3D%22%23017CEE%22%20stroke-width%3D%222%22%2F%3E%3Cpath%20d%3D%22M24%2024c-4-8-2-16%206-16s8%208%204%2016%22%20fill%3D%22%23017CEE%22%20opacity%3D%220.9%22%2F%3E%3Cpath%20d%3D%22M24%2024c8-4%2016-2%2016%206s-8%208-16%204%22%20fill%3D%22%2300AD46%22%20opacity%3D%220.9%22%2F%3E%3Cpath%20d%3D%22M24%2024c4%208%202%2016-6%2016s-8-8-4-16%22%20fill%3D%22%23017CEE%22%20opacity%3D%220.7%22%2F%3E%3Cpath%20d%3D%22M24%2024c-8%204-16%202-16-6s8-8%2016-4%22%20fill%3D%22%2300AD46%22%20opacity%3D%220.7%22%2F%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2224%22%20r%3D%223%22%20fill%3D%22white%22%2F%3E%3C%2Fsvg%3E`

### dbt
- **Color**: #FF694B
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpolygon%20points%3D%2224%2C2%2044%2C14%2044%2C34%2024%2C46%204%2C34%204%2C14%22%20fill%3D%22%23FF694B%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%2228%22%20text-anchor%3D%22middle%22%20font-family%3D%22Arial%2Csans-serif%22%20font-size%3D%2214%22%20font-weight%3D%22bold%22%20fill%3D%22white%22%3Edbt%3C%2Ftext%3E%3C%2Fsvg%3E`

### Kafka
- **Color**: #231F20
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2224%22%20r%3D%2222%22%20fill%3D%22%23231F20%22%2F%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2224%22%20r%3D%225%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2210%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2236%22%20cy%3D%2216%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2236%22%20cy%3D%2232%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2224%22%20cy%3D%2238%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2212%22%20cy%3D%2232%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Ccircle%20cx%3D%2212%22%20cy%3D%2216%22%20r%3D%224%22%20fill%3D%22none%22%20stroke%3D%22white%22%20stroke-width%3D%222%22%2F%3E%3Cg%20stroke%3D%22white%22%20stroke-width%3D%221.5%22%3E%3Cline%20x1%3D%2224%22%20y1%3D%2219%22%20x2%3D%2224%22%20y2%3D%2214%22%2F%3E%3Cline%20x1%3D%2228%22%20y1%3D%2221%22%20x2%3D%2233%22%20y2%3D%2218%22%2F%3E%3Cline%20x1%3D%2228%22%20y1%3D%2227%22%20x2%3D%2233%22%20y2%3D%2230%22%2F%3E%3Cline%20x1%3D%2224%22%20y1%3D%2229%22%20x2%3D%2224%22%20y2%3D%2234%22%2F%3E%3Cline%20x1%3D%2220%22%20y1%3D%2227%22%20x2%3D%2215%22%20y2%3D%2230%22%2F%3E%3Cline%20x1%3D%2220%22%20y1%3D%2221%22%20x2%3D%2215%22%20y2%3D%2218%22%2F%3E%3C%2Fg%3E%3C%2Fsvg%3E`

### Apache Spark
- **Color**: #E25A1C
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M24%204L4%2024l20%2020%2020-20z%22%20fill%3D%22%23E25A1C%22%2F%3E%3Cpath%20d%3D%22M24%2012l-12%2012%2012%2012%2012-12z%22%20fill%3D%22%23FF8C00%22%20opacity%3D%220.6%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%2228%22%20text-anchor%3D%22middle%22%20font-family%3D%22Arial%2Csans-serif%22%20font-size%3D%229%22%20font-weight%3D%22bold%22%20fill%3D%22white%22%3ESPARK%3C%2Ftext%3E%3C%2Fsvg%3E`

### Python
- **Color**: #3776AB / #FFD43B
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M24%204c-8%200-12%204-12%208v6h12v2H10c-4%200-8%204-8%2010s2%2010%208%2010h4v-8c0-4%204-8%208-8h12c4%200%206-2%206-6V12c0-4-4-8-10-8z%22%20fill%3D%22%233776AB%22%2F%3E%3Cpath%20d%3D%22M24%2044c8%200%2012-4%2012-8v-6H24v-2h14c4%200%208-4%208-10s-2-10-8-10h-4v8c0%204-4%208-8%208H14c-4%200-6%202-6%206v6c0%204%204%208%2010%208z%22%20fill%3D%22%23FFD43B%22%2F%3E%3Ccircle%20cx%3D%2218%22%20cy%3D%2211%22%20r%3D%222.5%22%20fill%3D%22%23FFD43B%22%2F%3E%3Ccircle%20cx%3D%2230%22%20cy%3D%2237%22%20r%3D%222.5%22%20fill%3D%22%233776AB%22%2F%3E%3C%2Fsvg%3E`

### AWS S3
- **Color**: #569A31
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M8%208h32l-4%2032H12z%22%20fill%3D%22%23569A31%22%2F%3E%3Cellipse%20cx%3D%2224%22%20cy%3D%228%22%20rx%3D%2216%22%20ry%3D%225%22%20fill%3D%22%237AB648%22%2F%3E%3Cellipse%20cx%3D%2224%22%20cy%3D%2240%22%20rx%3D%2212%22%20ry%3D%224%22%20fill%3D%22%233F8624%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%2227%22%20text-anchor%3D%22middle%22%20font-family%3D%22Arial%2Csans-serif%22%20font-size%3D%2210%22%20font-weight%3D%22bold%22%20fill%3D%22white%22%3ES3%3C%2Ftext%3E%3C%2Fsvg%3E`

### Azure
- **Color**: #0089D6
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M38%2036H12a10%2010%200%2001-1-20%2012%2012%200%200123-4%208%208%200%20014%2024z%22%20fill%3D%22%230089D6%22%2F%3E%3C%2Fsvg%3E`

### Tableau
- **Color**: #E97627
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Crect%20x%3D%2222%22%20y%3D%222%22%20width%3D%224%22%20height%3D%2214%22%20fill%3D%22%23E97627%22%2F%3E%3Crect%20x%3D%2222%22%20y%3D%2232%22%20width%3D%224%22%20height%3D%2214%22%20fill%3D%22%23E97627%22%2F%3E%3Crect%20x%3D%222%22%20y%3D%2222%22%20width%3D%2214%22%20height%3D%224%22%20fill%3D%22%23C72037%22%2F%3E%3Crect%20x%3D%2232%22%20y%3D%2222%22%20width%3D%2214%22%20height%3D%224%22%20fill%3D%22%23C72037%22%2F%3E%3Crect%20x%3D%2222%22%20y%3D%2218%22%20width%3D%224%22%20height%3D%2212%22%20fill%3D%22%235B879B%22%2F%3E%3Crect%20x%3D%2216%22%20y%3D%2222%22%20width%3D%2216%22%20height%3D%224%22%20fill%3D%22%235B879B%22%2F%3E%3Crect%20x%3D%2210%22%20y%3D%2210%22%20width%3D%223%22%20height%3D%2210%22%20fill%3D%22%23E97627%22%20opacity%3D%220.7%22%2F%3E%3Crect%20x%3D%2210%22%20y%3D%2228%22%20width%3D%223%22%20height%3D%2210%22%20fill%3D%22%23E97627%22%20opacity%3D%220.7%22%2F%3E%3Crect%20x%3D%2235%22%20y%3D%2210%22%20width%3D%223%22%20height%3D%2210%22%20fill%3D%22%23E97627%22%20opacity%3D%220.7%22%2F%3E%3Crect%20x%3D%2235%22%20y%3D%2228%22%20width%3D%223%22%20height%3D%2210%22%20fill%3D%22%23E97627%22%20opacity%3D%220.7%22%2F%3E%3C%2Fsvg%3E`

### Power BI
- **Color**: #F2C811
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Crect%20x%3D%224%22%20y%3D%224%22%20width%3D%2240%22%20height%3D%2240%22%20rx%3D%226%22%20fill%3D%22%23F2C811%22%2F%3E%3Crect%20x%3D%2210%22%20y%3D%2226%22%20width%3D%226%22%20height%3D%2214%22%20rx%3D%221%22%20fill%3D%22white%22%2F%3E%3Crect%20x%3D%2221%22%20y%3D%2218%22%20width%3D%226%22%20height%3D%2222%22%20rx%3D%221%22%20fill%3D%22white%22%2F%3E%3Crect%20x%3D%2232%22%20y%3D%2210%22%20width%3D%226%22%20height%3D%2230%22%20rx%3D%221%22%20fill%3D%22white%22%2F%3E%3C%2Fsvg%3E`

### Looker
- **Color**: #4285F4
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Ccircle%20cx%3D%2222%22%20cy%3D%2222%22%20r%3D%2214%22%20fill%3D%22none%22%20stroke%3D%22%234285F4%22%20stroke-width%3D%224%22%2F%3E%3Cline%20x1%3D%2232%22%20y1%3D%2232%22%20x2%3D%2244%22%20y2%3D%2244%22%20stroke%3D%22%234285F4%22%20stroke-width%3D%225%22%20stroke-linecap%3D%22round%22%2F%3E%3Ccircle%20cx%3D%2222%22%20cy%3D%2222%22%20r%3D%226%22%20fill%3D%22%234285F4%22%20opacity%3D%220.3%22%2F%3E%3C%2Fsvg%3E`

### Fivetran
- **Color**: #0073FF
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpolygon%20points%3D%2224%2C2%2046%2C17%2038%2C42%2010%2C42%202%2C17%22%20fill%3D%22%230073FF%22%2F%3E%3Cpath%20d%3D%22M16%2018h16M16%2024h12M16%2030h8%22%20stroke%3D%22white%22%20stroke-width%3D%223%22%20stroke-linecap%3D%22round%22%2F%3E%3C%2Fsvg%3E`

### Databricks
- **Color**: #FF3621
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M24%204l20%2012v4L24%2032%204%2020v-4z%22%20fill%3D%22%23FF3621%22%2F%3E%3Cpath%20d%3D%22M24%2016l20%2012v4L24%2044%204%2032v-4z%22%20fill%3D%22%23FF3621%22%20opacity%3D%220.7%22%2F%3E%3Cpath%20d%3D%22M24%204l20%2012L24%2028%204%2016z%22%20fill%3D%22%23FF6F61%22%20opacity%3D%220.5%22%2F%3E%3C%2Fsvg%3E`

### Sigma
- **Color**: #1B1464
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Crect%20x%3D%224%22%20y%3D%224%22%20width%3D%2240%22%20height%3D%2240%22%20rx%3D%228%22%20fill%3D%22%231B1464%22%2F%3E%3Ctext%20x%3D%2224%22%20y%3D%2234%22%20text-anchor%3D%22middle%22%20font-family%3D%22serif%22%20font-size%3D%2232%22%20font-weight%3D%22bold%22%20fill%3D%22white%22%3E%CE%A3%3C%2Ftext%3E%3C%2Fsvg%3E`

### Streamlit
- **Color**: #FF4B4B
- **Style**: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2048%2048%22%3E%3Cpath%20d%3D%22M6%2016l18%2010%2018-10%22%20stroke%3D%22%23FF4B4B%22%20stroke-width%3D%224%22%20stroke-linecap%3D%22round%22%20fill%3D%22none%22%2F%3E%3Cpath%20d%3D%22M6%2024l18%2010%2018-10%22%20stroke%3D%22%23FF4B4B%22%20stroke-width%3D%224%22%20stroke-linecap%3D%22round%22%20fill%3D%22none%22%20opacity%3D%220.7%22%2F%3E%3Cpath%20d%3D%22M6%2032l18%2010%2018-10%22%20stroke%3D%22%23FF4B4B%22%20stroke-width%3D%224%22%20stroke-linecap%3D%22round%22%20fill%3D%22none%22%20opacity%3D%220.4%22%2F%3E%3C%2Fsvg%3E`

## Fallback: color-coded shapes

When SVG icons don't render (e.g. draw.io web import), use colored rounded rectangles with white bold text instead. Assign colors by **tool category** and include a **dynamic color key** — only list categories that actually appear in the diagram.

| Category | Fill Color | Tools |
|----------|-----------|-------|
| Ingestion | `#0073FF` | Fivetran, Airbyte, Stitch |
| Orchestration | `#017CEE` | Airflow, Prefect, Dagster |
| Transform | `#FF694B` | dbt, Spark, Python scripts |
| Analytics / BI | `#E97627` | Tableau, Power BI, Looker, Sigma |
| Streaming | `#231F20` | Kafka, Kinesis, Snowpipe Streaming |
| Cloud / CSP | `#0089D6` | AWS S3, Azure, GCP |
| ML / AI | `#FF3621` | Databricks, SageMaker, Snowpark ML |
| App Framework | `#FF4B4B` | Streamlit, Dash, Gradio |
| Data Platform | `#29B5E8` | Snowflake |

Style for color-coded shape:
```
rounded=1;whiteSpace=wrap;fillColor=#COLOR;fontColor=#FFFFFF;strokeColor=#COLOR;fontStyle=1;fontSize=12;
```

**Dynamic color key**: Add a small swimlane legend in the diagram corner listing only the categories used. For example, if the diagram has Fivetran, dbt, and Tableau, the key shows only Ingestion, Transform, and Analytics/BI.

## Adding new icons

To add a new icon to this library:

1. Create a clean SVG (48x48 viewBox recommended)
2. URL-encode it: `python3 -c "import urllib.parse; print(urllib.parse.quote(open('icon.svg').read(), safe=''))"`
3. Add an entry above with the name, color, and full style string
4. The style string format is always: `shape=image;verticalLabelPosition=bottom;verticalAlign=top;imageAspect=0;aspect=fixed;image=data:image/svg+xml,URL_ENCODED_SVG`
5. **Do NOT use base64** - the `;` in `data:image/svg+xml;base64,` breaks draw.io's style parser
