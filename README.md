# SNOW MVP

SNOW MVP is a Power BI report for ServiceNow incident operations. It provides views for first-time resolution, mean time to resolve, backlog monitoring, employee support, and incident-level backlog investigation.

## Contents

- `SNOW_MVP.pbip` - Power BI Project entry point.
- `SNOW_MVP.Report/` - Report pages, visuals, themes, and registered image resources.
- `SNOW_MVP.SemanticModel/` - Semantic model, Power Query definition, relationships, and measures.
- `SNOW_MVP.SemanticModel/SERVICENOW_RD_POC_VERSION_CONTROL_MOCK.xlsx` - Synthetic workbook preserving the source schema and `Table1` name.
- `SNOW_MVP.pbix` - Packaged Power BI Desktop version of the report.

> **Public-release status:** The PBIP definitions now use synthetic incident data. The existing `SNOW_MVP.pbix` must still be opened, refreshed, and saved again in Power BI Desktop before it is published because a PBIX can retain imported data internally.

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

The `RAW DATA` query now generates a deterministic synthetic incident dataset inside the semantic model. The repository also includes `SERVICENOW_RD_POC_VERSION_CONTROL_MOCK.xlsx` as a source-shaped reference dataset; it preserves the original 11-column schema and `Table1` name but is not required by the current inline query.

The dataset is synthetic and must not be replaced with production or personal data before publishing this repository.

## Public-release checklist

Before pushing this project to a public repository:

- Refresh the PBIP project in Power BI Desktop and replace `SNOW_MVP.pbix` with the refreshed file.
- Inspect incident detail and drillthrough pages for mock IDs, users, descriptions, dates, and team names.
- Confirm all eight pages, filters, navigation, measures, and drillthrough actions work.
- Search tracked files and Git history for real incident IDs, people, internal team names, local paths, source workbook names, and corporate email addresses.
- Do not commit source workbooks, exports, Power BI caches, backups, or the old PBIX.

## Development notes

- The project is stored in PBIP developer mode, so report and model definitions are version-control-friendly text files.
- Report definitions use the `CY23SU11` shared base theme.
- Measures and calculated columns are written in DAX; source shaping is written in Power Query M.
- There is no automated test suite. Validate changes by opening the report, refreshing the model, and checking affected visuals and filters in Power BI Desktop.

## License

No license has been specified for this project.