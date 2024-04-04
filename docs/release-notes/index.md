---
layout: default
title: Release notes
description: Explore the latest updates in our Release Notes page, featuring new features, enhancements, and bug fixes to improve your user experience and productivity.
nav_order: 99
---

# Release notes
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## March 2024
- We celebrated [the launch of Ada, our AI-powered data analyst, on ProductHunt](https://www.producthunt.com/products/ada-by-boostkpi). This launch generated significant interest, garnering over 110 upvotes and achieving a daily ranking of 21 and a weekly ranking of 82.
- Our [website](https://boostkpi.com) underwent a major makeover in preparation for Ada's launch. We added more content and improved the design.
- To enhance our website's SEO, we transitioned to Static Site Generation.
- Ada received exciting updates this month, including the support for filters and new datasets.
- We integrated LLM-based summaries into the drilldown and dimension overview table reports, making data insights even more accessible and comprehensible.

## February 2024
- Launched natural language prompts to create alert YAML [blog](https://blog.boostkpi.com/natural-language-alerts/)
- Added data connectors for [AlloyDB](https://boostkpi.com/data-sources/alloydb), [Google Cloud SQL](https://boostkpi.com/data-sources/cloud-sql), and [DuckDB](https://boostkpi.com/data-sources/duckdb)
- Updated the layout and styling for the [website](https://boostkpi.com). Made it easier to add [solutions pages](https://boostkpi.com/solutions)
- Fixed a number of pending bugs introduced during the migration to react.

## January 2024
- Added list of anomalies on the dashboard page, for easy access.
- When dimension names are long, the drilldown table showed overlapping text. Fixed the bug.
- Updated chatbots to use the chatgpt4 API.
- SEO updates for the [docs site](https://docs.boostkpi.com)

## December 2023
- Improved the UX by re-implementing the dashboard in react. The dashboard app now flickers less and renders quicker.
- Improved the drilldown results for non-additive KPIs (like CPC, AOV, Conversion rates).
 

## November 2023
- In the KPI breakdown tab, you can now roll up the results by a coarser time granularity. For example, you can get daily or weekly KPIs for hourly dataset.
- The dimension heatmap is now more useful. It will now show a dimension row even if there is an include/exclude filter on it. 
- Improved the chatbot interface by adding a list of suggested questions. We used an LLM to generate this list.
- Made SEO updates on the [website](https://boostkpi.com) (added solution pages, comparison pages, data sources pages) and the [docs site](https://docs.boostkpi.com)


## October 2023
- Renamed pivot heatmap to KPI heatmap. Added support for derived KPIs and dimensions with lots of values. [Blog post.](https://blog.boostkpi.com/KPI-Heatmap/) [Video.](https://www.youtube.com/watch?v=18SxeqDdXXE) 
- Added support for history and internal tools to the chat interface. Whitelisted users can query their data as well as drilldown on changes, using natural language. We leverage LLMs as orchestrators. [Blog post.](https://blog.boostkpi.com/orchestration-llms/) [Video.](https://www.youtube.com/watch?v=KVP3-WwN6Dc) 

## September 2023
- Deployed a pivot heatmap feature that works for additive KPIs.
- Launched an early version that lets users query their data in natural language, using LLMs.

## August 2023
- Allowed pivot calls on a time dimension.
- Added links to partner pages, plus created a [partner page](https://cloud.google.com/find-a-partner/partner/boostkpi-inc) for Google Cloud.

## July 2023
- Enabled pausing imports in the dashboard UI.
- Enabled accepting dataset alias when constructing detections.

## June 2023
- Launched an early version of a chat box to answer a user's query. The chat box leverages generative AI to answer queries in English.
- Launched a feature to let users adjust their import schedule.

## May 2023
- Setup an early version of AWS Athena in production with one customer.
- Added documentation to obtain results from overview and drill-down calls as json.
- Sorted the dataset list.
- Added support for importing CSVs, where the field names contain commas.

## April 2023
- Launched an improved overview table. Now supports sorting based on KPI values and filtering based on dimension names. Implemented in React.
- Implemented a JSON endpoint to query anomalies.
- Moved the root-cause KPI table to react.  Added KPI search for the KPI root-cause table.

## March 2023
- Updated the size of a cell in the heatmap to accurately reflect its contribution. Updated the size of the OTHERS cell accordingly.
- For derived KPIs, the normalized color values now sum to zero, like non-derived KPIs.
- Updated the FAQ and release notes to use this website instead of a plain google doc.
- During import, sanitized column names, allowed the use of reserved SQL words, and allowed uploading the same CSV filename many times.
- Added UI for scheduling backfill.
- Fixed the display issue in the pivot tab for KPIs marked as inverse.

## February 2023
- Updated the schema page. Users can annotate datasets as well as the dimensions in the dataset.
- Added ability to search and filter datasets.
- Added an option to backfill data for any given date range. The backfill smartly chunks the data so that the process completes as soon as possible.
- Added option to size the heatmap by current or baseline values.
- Improved handling of negative values in heatmap and overview.
- Show details when users hover on the OTHER box.
- Added name of the view/snapshot/anomaly when displaying one in the root cause page.

## January 2023
- Added a schema page.
- Added option to download anomaly data as a csv file.
- Replaced KPI table on the dataset page by time-series charts, which can be personalized (choose granularity, KPIs, KPI slices, investigation period, baseline period).
- Added a workaround to import one-off data when the number of rows exceeds 350k.

## December 2022
- Recommend derived KPIs (and identifying KPIs as cost KPIs) for marketing and other verticals. Leverage historical data too.
- Recommend alerts for accounts that do not have alerts set up.
- Add query params to the anomaly page.

## November 2022
- Initial UI support for creating alerts. Previously, it was yaml.
- Certified snowflake integration.
- Users can manually control the order in which charts are displayed. The order is preserved in snapshots.
- Users can exclude/include dimensions for a dataset.
- Added a better, more intuitive datepicker.

## October 2022
- Added support for downloading the cohort predictions as a daily csv.
- Added this release notes doc.
- (Certified) Databricks integration.

## September 2022
- Email alerts when the backfill is complete.
- KPI filters on the pivot table.
- Added support for weekly and monthly datasets.

## August 2022
- One-off imports.
- Import diagnostics.
- Option to type dates in the chart view.
- Customer-verified connection with Databricks.
- FAQs (Frequently Asked Questions) doc.

## July 2022
- Marking a KPI as a cost metric.
- (Alpha) Databricks integration.

## June 2022
- Heatmap shows correctly for derived KPIs.
- Visualize results of query running in the SQL editor.
- Ad-hoc support for alerting on spend and ROAS targets.

## May 2022
- Rolling alerts such as 7-day sliding window.
- Customer-verified connection to ClickHouse.

## April 2022
- Support for time zones and offsets in setting up scheduled imports.
- Invite other users in the organization.
- Customer-verified connection to Snowflake.

## March 2022
- (Alpha) Setting up scheduled imports from the SQL editor.
- Textual description of a report the user is going to see.
- Customer-verified connection to RedShift.

## February 2022
- Online SQL editor for easy connection to SQL-speaking Data Warehouses and databases.
- Customer-verified connection to BigQuery and MySQL.
