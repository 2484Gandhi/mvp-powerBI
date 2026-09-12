# SNOW MVP

SNOW MVP is a Power BI report for ServiceNow incident operations. It provides views for first-time resolution, mean time to resolve, backlog monitoring, employee support, and incident-level backlog investigation.

## Contents

- `SNOW_MVP.pbip` - Power BI Project entry point.
- `SNOW_MVP.Report/` - Report pages, visuals, themes, and registered image resources.
- `SNOW_MVP.SemanticModel/` - Semantic model, Power Query definition, relationships, and measures.
- `SNOW_MVP.pbix` - Packaged Power BI Desktop version of the report.

## Open the project

1. Install a recent version of Power BI Desktop with Power BI Project (PBIP) support.
2. Open `SNOW_MVP.pbip` from Power BI Desktop.
3. Select **Refresh** to load the included synthetic incident data.

The `.pbix` file can be used as an alternative when working with the packaged report format.

## Report pages

| Page | Purpose |
| --- | --- |
| Landing | Entry page for the report. |
| FTR | First-time resolution analysis. |
| MTTR(WITH PRB) | Mean time to resolve for incidents involving problem records. |
| MTTR(WITHOUT PRB) | Mean time to resolve for incidents without problem records. |
| BACKLOG | Backlog monitoring and aging analysis. |
| EMPLOYEE_CENTER | Employee support view. |
| BACKLOG DRILLTHROUGH | Incident details filtered from the backlog context. |
| Duplicate of BACKLOG | Additional backlog report view. |

## Data model

The model uses imported data and contains:

- `RAW DATA` - Incident records with number, dates, priority, state, assignment group, assignee, description, hold reason, reopen count, reassignment count, incident age, and age bands.
- `MEASURES (2)` - Measures for incident count, FTR, MTTR, backlog count, backlog aging, and display text.
- Date tables - Local date tables are used for the `Created` and `Updated` date columns.

The Power Query transformation also derives age bands, team names, assignment-group sort order, priority labels, and a business-hours flag.

## Refresh the data

The `RAW DATA` query now generates a deterministic synthetic incident dataset inside the semantic model. It does not require an external workbook or local file path. Replace the mock rows in the Power Query definition only when you are intentionally creating a different public test dataset.

The dataset is synthetic and must not be replaced with production or personal data before publishing this repository.

## Development notes

- The project is stored in PBIP developer mode, so report and model definitions are version-control-friendly text files.
- Report definitions use the `CY23SU11` shared base theme.
- Measures and calculated columns are written in DAX; source shaping is written in Power Query M.
- There is no automated test suite. Validate changes by opening the report, refreshing the model, and checking affected visuals and filters in Power BI Desktop.

## License

No license has been specified for this project.