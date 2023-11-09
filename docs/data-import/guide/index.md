---
layout: default
parent: Data import
title: Data import guide
---

# Data import guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Importing data into BoostKPI

1. Log in to BoostKPI and select Import along the top.
2. Create a connection to your existing data by selecting “Connections” and then “Add connection”.
3. Make sure to test your connection. If the connection fails or times out, make sure BoostKPI’s ip
   addresses are whitelisted.
4. Write your query:
    - For testing and one-off analysis, write a query that returns the exact results you wish to see
      in BoostKPI.
    - For a dataset you wish to see continually updated, write a query that includes two timestamps
      which imports data between those two timestamps. Your query should include data for the
      earlier timestamp and exclude data for the later timestamp. E.g.,
    ```sql
    SELECT date, dimension, kpi FROM table 
    WHERE date >= "2022-01-01 00:00:00" AND 
          date < "2022-01-02 00:00:00"
    ```

5. Save (Ctrl + S) and run your query to check the results.
6. Select “Import”.
    - Select your import type “**SCHEDULED**” or “**ONE-OFF**"
    - Enter an appropriate dataset name.
    - Select your data’s time granularity. This setting controls how BoostKPI will display your data
      and for scheduled imports, it controls the import frequency.
    - For scheduled imports:
        - Select the timezone your data finalizes in.
        - Set the offset for scheduling the data import. This should be the time duration it takes
          the data to finalize. So if your daily data for the prior day finalizes at 1:00 am, set an
          offset of 1 hour.
        - Verify that the template query was created correctly. BoostKPI will replace
          **{{start_time}}** and **{{end_time}}** with new timestamps each time we import new data.
    - For each column of your query's results, pick date, timestamp, dimension, or KPI. KPIs should
      all be numeric and you should only have one date/timestamp type. Datasets in BoostKPI must
      have at least one dimension and at least one KPI.
    - Click import!
    - Based on the query and your selections, BoostKPI will create a new dataset and begin a data
      import.
        - For one-off imports, your query will be executed as is and the results will be imported
          into BoostKPI.
        - For scheduled queries, timestamps will be substituted into your query to backfill an
          initial time range based on the data granularity. Then going forward your query will be
          executed according to a schedule based on the data granularity to import new data into
          BoostKPI with new timestamps substituted each time.
    - When the data is finished importing, you will receive an email letting you know that your
      dataset is ready.

## Importing tips

1. For scheduled imports, your query should contain a filter on your date/timestamp column that has
   exactly two timestamps strings of the form “**YYYY-MM-DD HH:mm:ss**”.

   When importing data, BoostKPI dynamically updates your query by replacing these timestamps
   strings. When importing the example query, BoostKPI first saves a template query by replacing the
   two timestamp strings:
   ```sql
   SELECT date, dimension, kpi 
   FROM table 
   WHERE date >= "{{startTime}}" AND date < "{{endTime}}"
   ```

   And then fills in the template when importing the data. For example, when importing the data for
   January 2nd, 2022, BoostKPI executes:
   ```sql
   SELECT date, dimension, kpi 
   FROM table 
   WHERE date >= "2022-01-02 00:00:00" AND date < "2022-01-03 00:00:00"
   ```

   Without exactly two timestamps strings, BoostKPI will be unable to properly template and schedule
   your query.

2. Make sure your query is inclusive on the start timestamps and exclusive on the end timestamps.

   BoostKPI runs an updated version of your query on a schedule. If the endpoints of the scheduled
   queries overlap, this can result in duplicate data being uploaded into BoostKPI. As an example,
   if you imported the query:
   ```sql
   SELECT date, dimension, kpi 
   FROM table 
   WHERE date BETWEEN "2022-01-01 00:00:00" AND "2022-01-02 00:00:00"
   ```

   Then because BETWEEN is inclusive, data for January 2nd, 2022 would be imported when BoostKPI
   attempts to import the data for January 1st, 2022.

3. (**RedShift**) When importing date columns from redshift, please use:

   _to_char(date(original_date), 'YYYY-MM-DD') as date_

   Redshift’s default date output format causes conflicts with our database’s expected date import
   format.

4. Import the most granular data you can along your time and dimension columns. BoostKPI can then
   aggregate it either during visualization or when sending out anomalies.

# Data modeling tips

#### Modeling multiple date columns

If you have multiple dates or timestamps in the columns of your query results, only set your primary
time column to Date/Timestamp in the import selector and set the other time columns to Dimension.

BoostKPI uses a primary time column when displaying time series, comparing data across time, and
detecting anomalies. If you wish to import multiple time columns, any time column beyond the primary
one should be marked as a Dimension. It is useful to import such a time_column as an offset to the
primary time column.

For example, imagine a dataset with the primary time_column as invoice_date and a payment_date
column (that is after the invoice_date). The payment_date could be modeled as payment_offset (
=DATE_DIFF(payment_date, invoice_date)) in days – it is then possible to identify when there is an
increase in late payments.

#### Modeling column with numerical value as a dimension

Consider grouping numeric dimension columns or time dimension columns into buckets when they have a
large range.

BoostKPI slices and dices along dimension columns allowing you to gain insight into how KPIs have
changed in subdimensions of your data. If your query includes a simple “Age” column, BoostKPI can
analyze changes in KPI values based on single “Age” values. Unfortunately, if there is a change in a
KPI value among 18-25 year olds, a single “Age” value breakdown will be insufficient. Instead,
import a query where “Age” has been aggregated into “Age_Bucket” with buckets for important age
groups, e.g., 18-24, 25-34, 35-44, 45-54, 55-64, 65+.

Depending on your use-case you might want to keep the original dimension columns around as well.

#### Modeling additional time columns as offsets.

Consider replacing time Dimension columns with offsets computed from the primary time column.

When a date column is included as a Dimension in BoostKPI, you will be able to see changes in your
KPI broken down by this date. However if you have a conversion funnel, you might instead want to
track changes in your KPIs broken down by how long people took to move from one stage of the funnel
to another. For example, if you are importing purchase data with “purchase date” and “account
creation date”, you could include the difference of these two columns to enable analyzing purchases
based on account age at time of purchase.

It can also be useful to further bucket these offsets.

#### Modeling dimensions with null values.

Only import null dimension values if there is no category label that can be applied to the row.
Consider replacing them with suitable String values like “none”, “missing”, etc.

BoostKPI’s analysis will omit null dimension values when breaking data down by any dimension that
contains nulls. Only include null values when it makes sense for those rows to be left out when
viewing a breakdown by that dimension. This would be appropriate in an instance where a dimension
column only makes sense for a subset of rows as would be the case for buy/sell data: purchase_month
would have a value for buy rows and null for sell rows.

#### Modeling KPI with negative values.

Often, negative values such as -1 are used as sentinel values to indicate that a KPI field has not
been updated. In many such cases, it is better to model it as a 0 value (which can be done via a
case statement in the SQL editor).

For many of its analyses, BoostKPI assumes that the KPIs are non-negative.

#### Modeling derived KPIs.

Do not directly import a derived KPI. Instead, import the numerator and denominator separately and
then set-up the derived KPI in the BoostKPI dashboard. This will ensure that BoostKPI can correctly
aggregate the derived KPI.

For example, to calculate AOV (Average Order Value), import revenue and num_orders separately. On
the BoostKPI dashboard, set up AOV as revenue/num_orders.

# After importing

After importing a new dataset, BoostKPI will begin an automatic backfill of your data. When the
backfill is complete, you will receive an email notification. While the data is importing, you can
finish setting up your dataset on the dataset schema page. To navigate there, select your dataset on
the BoostKPI dashboard and select the “Schemas” tab along the top row.

#### Add derived KPIs

Derived KPIs can be added to a dataset on the Schemas page by selecting the “Add derived KPI” button
on the right hand side. In the menu that opens, you can either select a derived KPI to copy from an
existing dataset or create a new one by dragging and dropping metric names.

Currently BoostKPI only supports derived KPIs that are a ratio (of the form X / Y) or a percentage (of the form X*100/Y).

#### Mark KPIs as inverse

On the dataset’s Schemas page, KPIs can be marked as “Inverse”. This indicates that an increase in
the KPI should be reflected as a bad change while a decrease should be reflected as a good change.
When set, an inverse KPI will use red numbers for increases and blue numbers for decreases (the
opposite coloring of normal KPIs). This is useful for interpreting change when viewing cost or spend
metrics that you want to minimize.

#### Add descriptions and show/hide dimensions and KPIs

Also on the Schemas page, you can add short descriptions for the dataset and the dataset’s
dimensions. This is useful to include important dataset context that user’s may not have such as how
KPIs were defined or what kind of values are stored in a dimension.

Dimensions and KPIs can also be hidden (or unhidden) to decrease clutter when performing an
investigation on a dataset.

#### Deleting datasets

A dataset can be deleted from the BoostKPI dashboard by selecting “Edit dataset” on the right hand
side of the Schemas page. At the bottom of the edit menu, type “DELETE” into the text box and then
click the delete button.

Note that this only performs a soft delete of the data. If a hard delete of the data is required,
e.g., due to legal compliance reasons, please contact amit@boostkpi.com.

