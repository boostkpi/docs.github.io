---
layout: default
title: Data import
description: Navigate through our FAQs on data import, covering supported data sources, IP address white-listing, differences between scheduled and one-off imports, CSV file import details, various supported CSV import types, the import process, and methods for refreshing already imported data on a scheduled basis 
has_children: true
nav_order: 4
---

# Data import
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Supported data sources

BoostKPI can connect to many different data sources that support a SQL interface. The current list of supported data sources includes:
- AlloyDB
- Amazon Athena
- Amazon Redshift
- Apache Pinot
- Apache Drill
- Google BigQuery
- Cassandra
- ClickHouse
- Cloud SQL
- CrateDB
- Databricks
- DuckDB
- Microsoft SQL Server
- MySQL
- PostgreSQL
- PrestoDB
- Snowflake
- Trino
- Vertica

We just require read only access to the right table in the data source. For each integration, we use SQL to access the underlying data.

![Data sources list: image](../images/data-sources-list.png)

## IP address white-listing

Please whitelist the following 4 IP addresses:
- 34.73.45.207
- 34.75.196.63
- 35.231.217.127
- 35.237.13.9

## Scheduled vs. one-off imports

A “**one-off**” import is for data that need not be re-pulled. For example, if you want to do an ad-hoc
analysis on the last month's data, you can use “one-off” to pull the result of the sql query.

A “**scheduled**” import is for data that is periodically updated, say every hour or every day. BoostKPI
can pull such data at scheduled intervals. It also automatically updates the date range to pull the
most recent data. See [Importing data into BoostKPI](/docs/data-import/guide/#importing-data-into-boostkpi) for details.

Many of our users start with one-off imports to do some ad-hoc analysis. They then iteratively add or
remove dimensions and repeat the analysis. Once they are happy with the data-set, they can set up a scheduled import.

## CSV file import

BoostKPI also supports one-off import of CSV file. To import the file, go to Import page -> Upload CSV.

![Upload CSV: image](../images/upload-csv.png)

### Types of supported csv imports

BoostKPI supports two types of csv imports: a time-series csv and a lookup csv.

A time-series csv is one that contains at least one time-series column (date or timestamp) and has one or
more KPIs grouped by one or more dimension values and the time bucket. For example, a csv file containing
the hourly breakdown of revenue broken down by the brand, country, and platform.

A lookup csv is one where existing dimension values are mapped to a new dimension value. For example,
a csv file containing a mapping from a country to a continent. This csv file results in a lookup
dataset, which can then be joined with an existing time-series dataset.

## Import process

The document [Importing data into BoostKPI](/docs/data-import/guide/#importing-data-into-boostkpi)
provides more information about the import process.

## Refreshing already imported data (scheduled)

```
Q: For scheduled imports, can BoostKPI refresh old data in addition to pulling new data?
For example, I’m importing Facebook Ads spend and conversions.
The conversion data does not finalize until 7 days later.
```

Yes, you can configure your data import to refresh a previous time range on the "Import diagnostics" tab. This tab is currently only available *after* creating the import.

1. Navigate to the "Dashboard" at the top of the page and then select the dataset you wish to update in the left hand column.
2. Select "Import diagnostics" and then to the right click the "Edit import" button.
3. Under "Refresh data on import" enter the number of timepoints you wish to update on each import. E.g., in the Facebook Ads example, enter 7 so that the last seven days of data are refreshed on each import.
4. Click the "Update" button and a success message should briefly display at the bottom of the screen.

![Edit import menu](../images/edit-import-menu.png)
