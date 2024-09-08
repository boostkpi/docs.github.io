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

## August 2024
### Features
- **Google Authentication**: Users from enterprises using Google Workspace can now sign in to BoostKPI with their Google accounts, eliminating the need for a BoostKPI-specific password.
- **ADA Updates**: Users can now view all conversations within an enterprise, not just the ones they created.
- **Key-pair Authentication for Snowflake**: Key-pair authentication is now supported, allowing Snowflake accounts with two-factor authentication (2FA) to connect with BoostKPI.

### UI Updates
- **General Improvements**: CSV uploads now support blank cells and cells containing new lines.
- **ADA Updates**: Added the ability to duplicate a workspace and updated CSS styles in the FAQ modal.

### Backend Updates
- **ADA Conversation Management**: A copy of a conversation will be automatically created if a user wishes to continue in a conversation that they did not originally start.


## July 2024
### Features
- **AI Data Analyst Enhancements**: Added support for stored SQL queries in workspace as a way to provide more context. Improved function logging in Python and backend for better traceability and debugging.

### UI Updates
- **General Improvements**: Added loading animations to the workspace editor to enhance user feedback during data loading processes. Updated FAQ history list styling and maximized width for FAQ/Alert chat for a more streamlined user experience. Introduced an 'unsaved changes' notification to alert users to save modifications, preventing data loss.
- **Workspace Management**: Implemented enhancements in the SQL editor within the AI chat, including fixes for query appending and execution feedback. Updated workspace UI components, such as adjusting the SQL editor width and improving icon button sizing.

### Backend Updates
- **Functionality and Performance Enhancements**: Enhanced the logging of functions within the backend and Python environments to include more detailed and structured logs.
Removed unnecessary try-catch blocks for cleaner code and improved error handling on Google Cloud Functions.
- **System Enhancements**: Fixed issues with message formatting and updated 'function' naming conventions for consistency and clarity.


## June 2024
### New Features
- **ADA (AI Data Analyst) Enhancements**: Added support for workspaces and custom
  prompts, so that the AI Data Analyst can be personalized.  Improved AI chat
functionalities to include more detailed workspace resources and better error
handling.
- **Data Management**: Introduced a new feature for downloading CSVs from
  drill-down analysis, ensuring data portability and user convenience.

### UI Improvements
- **General Improvements**: Added a help link to the "no workspace" message,
  enhancing user guidance.  Updated AI chat button to improve interaction in
specific modules. Redesigned baseline text handling and updated drawer visuals
to maintain consistency across the website.
- **Workspace Management**: Implemented numerous fixes and updates in the chat
  workspace frontend, improving UX and data handling.  Separated imported
datasets from live ones using distinct icons to enhance data organization.
Disabled the old import button when external connections are allowed,
streamlining the interface.

### Backend Updates
- **Dependency Updates**: Updated various libraries and dependencies across the
  system to enhance performance and security, including pymysql,
io.github.classgraph, ws, @azure/msal-node, mssql, braces, @grpc/grpc-js,
org.apache.avro, com.google.code.gson, and mysql2.
- **SQL and Query Handling**: Standardized SQL query labels and removed redundant
  properties to optimize query performance.  Addressed issues with SQL BETWEEN
clause and ensured consistent handling across different datasets.
- **System Performance**: Fixed issues with parsing in the tool picker to prevent
  errors and improve system reliability.  Made critical updates to handle
undefined values and improve the display of charts and data ranges.


## May 2024
### New Features
- 🚀 Game-Changing Zero-Copy Feature! BoostKPI now runs directly on your cloud data warehouse without any data copying. Experience enhanced security, privacy, and governance, plus lightning-fast POCs and deployment! Currently supporting BigQuery, Redshift, ClickHouse, Snowflake, Databricks, and DuckDB.
- **DuckDB and Iceberg Support**: Expanding our compatibility to give you more flexibility and power.

### UI Improvements
- **UI Enhancements**: Sleeker, more intuitive interface for a seamless user experience.
- **Pivot First Load Fix**: No more issues when the selected dimension isn't set.
- **Anomaly Row Dataset Name Handling Update**: Improved accuracy in dataset names.
- **Pivot Heatmap Fix**: Heatmaps now work perfectly even when data is missing.
- **Edit Modal Enhancement**: Easily change dataset granularity.
- **External Links from Root Cause Page**: Navigate seamlessly to external resources.
- **Visual Consistency**: Baseline text handling and drawer visuals now match the rest of the site for a cohesive look.

### Backend Updates
- **40% Cloud Cost Reduction**: Significant savings on your cloud expenses.
- **Faster Detection Runs**: Reduced waiting time, speeding up your insights.

## April 2024
### New Features
- **Google Cloud Certifications:** BoostKPI is now Google Cloud Ready for BigQuery, AlloyDB, and CloudSQL! For more details on what this means for you, check out our [partners page](https://boostkpi.com/partners).
- **AI Chat Prototype:** We've prototyped the first version of our AI Chat that operates directly on the data warehouse, enabling insights without the need to create separate BoostKPI datasets.
- **UI Updates:**
  - New Integrations page added. Explore it [here](https://boostkpi.com/integrations).
  - Reworked Pricing page for clearer, more accessible information. See the new pricing structure [here](https://boostkpi.com/pricing).
  - Our AI chat interface now utilizes websockets, significantly improving interaction speeds and overall user experience.

### Improvements
- **BigQuery Integration:** Resolved an issue with schema loading in the BigQuery connection, enhancing stability and reliability.
- **Backend Enhancements:**
  - Streamlined API paths for more efficient backend operations.
  - Implemented admin privileges requirement for accessing the api/raw endpoint to enhance security and control.

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
