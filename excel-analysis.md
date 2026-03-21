**Retail Territory Margin Analysis | Excel**
Tools: Microsoft Excel (PivotTable, Conditional Formatting) | Dataset: 9,995 orders across US states

**What I built**
An interactive Excel dashboard summarising average net margin by US state, with automatic colour coding to flag underperforming territories at a glance.

**Steps taken:**
Imported merged retail CSV (9,995 rows, 3 source files) into Excel
Built a PivotTable summarising average Net_Margin_pct by State
Applied conditional formatting:

**Red** — states below 10% average margin (critical)
**Green** — states above 30% average margin (healthy)

Sorted by margin ascending to surface problem states immediately

**Key findings**
Texas, Illinois, Ohio, Florida Below 10% — highest risk
Pennsylvania, Colorado, Arizona Below 10% — needs review
District of Columbia, Iowa, Arkansas Above 30% — best performers

**Business value**
A manager can open this file and immediately see which territories need pricing or cost structure attention — no SQL, no Python needed. Designed for non-technical stakeholders.
