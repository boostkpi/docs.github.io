---
layout: default
parent: Data import
title: Data import guide
description: Our FAQ page on data importing is your comprehensive guide to mastering data management within BoostKPI. Learn the ins and outs of importing data, including valuable tips and tricks. Discover how to model multiple date columns effectively, handle numerical values as dimensions, and incorporate additional time columns as offsets. Dive into techniques for modeling dimensions with null values and KPIs with negative values, and explore the art of creating derived KPIs for enhanced insights. After importing your data, explore how to add, mark, and manage KPIs, as well as fine-tune your datasets with descriptions, dimension and KPI visibility settings. When it is time to clean up, we've got you covered with instructions on deleting datasets. Elevate your data management skills with BoostKPI's data importing FAQs.
nav_order: 1
---

# Data import guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Importing data into BoostKPI

1. Log in to BoostKPI and select **Connect** along the top.
2. Create a connection to your existing data by selecting **Connections** and then **Add connection**.
3. Make sure to test your connection. If the connection fails or times out, ensure BoostKPI’s ip
   addresses are whitelisted.
4. Create a table or view containing the data you would like to use in BoostKPI.
5. Click the **Connect data** button.
  - Select your schema and table name.
  - Enter an appropriate human-readable dataset name. This can be changed later.
  - Select your dataset's data granularity. This represents the lowest time granularity BoostKPI will 
    use when analyzing your data and should match the level of time column aggregation in the data.
  - Click **Load**. This executes a query on your dataset to load column data.
  - BoostKPI will analyze the results of the query and populate a column schema.
  - For each column of the query's results, pick date, timestamp, dimension, or KPI. KPIs should
    all be numeric and you should only have one date/timestamp column. Datasets in BoostKPI must
    have at least one dimension and at least one KPI.
  - Click **Create**!
6. BoostKPI will create a new dataset and after a few seconds you will be redirected to the BoostKPI dashboard.

## Importing tips

1. (**RedShift**) When importing date columns from redshift, please use:

   _to_char(date(original_date), 'YYYY-MM-DD') as date_

   Redshift’s default date output format causes conflicts with our database’s expected date import
   format.

2. Import the most granular data you can along your time and dimension columns. BoostKPI can then
   perform further aggregation either during visualization or when sending out anomaly alerts.

# Data modeling tips

## Modeling multiple date columns

If you have multiple dates or timestamps in the columns of your table, only set your primary
time column to Date/Timestamp in the import selector and set the other time columns to Dimension.

BoostKPI uses a primary time column when displaying time series, comparing data across time, and
detecting anomalies. If you wish to import multiple time columns, any time column beyond the primary
one should be marked as a Dimension. It is useful to import such a time_column as an offset to the
primary time column.

For example, imagine a dataset with the primary time_column as invoice_date and a payment_date
column (that is after the invoice_date). The payment_date could be modeled as payment_offset (
=DATE_DIFF(payment_date, invoice_date)) in days – it is then possible to identify when there is an
increase in late payments.

## Modeling column with numerical value as a dimension

Consider grouping numeric dimension columns or time dimension columns into buckets when they have a
large range.

BoostKPI slices and dices along dimension columns allowing you to gain insight into how KPIs have
changed in subdimensions of your data. If your query includes a simple “Age” column, BoostKPI can
analyze changes in KPI values based on single “Age” values. Unfortunately, if there is a change in a
KPI value among 18-25 year olds, a single “Age” value breakdown will be insufficient. Instead,
import a query where “Age” has been aggregated into “Age_Bucket” with buckets for important age
groups, e.g., 18-24, 25-34, 35-44, 45-54, 55-64, 65+.

Depending on your use-case you might want to keep the original dimension columns around as well.

## Modeling additional time columns as offsets.

Consider replacing time Dimension columns with offsets computed from the primary time column.

When a date column is included as a Dimension in BoostKPI, you will be able to see changes in your
KPI broken down by this date. However if you have a conversion funnel, you might instead want to
track changes in your KPIs broken down by how long people took to move from one stage of the funnel
to another. For example, if you are importing purchase data with “purchase date” and “account
creation date”, you could include the difference of these two columns to enable analyzing purchases
based on account age at time of purchase.

It can also be useful to further bucket these offsets.

## Modeling dimensions with null values.

Only import null dimension values if there is no category label that can be applied to the row.
Consider replacing them with suitable String values like “none”, “missing”, etc.

BoostKPI’s analysis will omit null dimension values when breaking data down by any dimension that
contains nulls. Only include null values when it makes sense for those rows to be left out when
viewing a breakdown by that dimension. This would be appropriate in an instance where a dimension
column only makes sense for a subset of rows as would be the case for buy/sell data: purchase_month
would have a value for buy rows and null for sell rows.

## Modeling KPI with negative values.

Often, negative values such as -1 are used as sentinel values to indicate that a KPI field has not
been updated. In many such cases, it is better to model it as a 0 value (which can be done via a
case statement in the SQL editor).

For many of its analyses, BoostKPI assumes that the KPIs are non-negative.

## Modeling derived KPIs.

Do not directly import a derived KPI. Instead, import the numerator and denominator separately and
then set-up the derived KPI in the BoostKPI dashboard. This will ensure that BoostKPI can correctly
aggregate the derived KPI.

For example, to calculate AOV (Average Order Value), import revenue and num_orders separately. On
the BoostKPI dashboard, set up AOV as revenue/num_orders.

# After importing

After importing a new dataset, you can finish setting up your dataset on the dataset schema page. 
To navigate there, select your dataset on the BoostKPI dashboard and select the **Schemas** tab along 
the top row.

## Add derived KPIs

Derived KPIs can be added to a dataset on the Schemas page by selecting the “Add derived KPI” button
on the right hand side. In the menu that opens, you can either select a derived KPI to copy from an
existing dataset or create a new one by dragging and dropping metric names.

Currently BoostKPI only supports derived KPIs that are a ratio (of the form X / Y) or a percentage (of the form X*100/Y).

## Mark KPIs as inverse

On the dataset’s Schemas page, KPIs can be marked as “Inverse”. This indicates that an increase in
the KPI should be reflected as a bad change while a decrease should be reflected as a good change.
When set, an inverse KPI will use red numbers for increases and blue numbers for decreases (the
opposite coloring of normal KPIs). This is useful for interpreting change when viewing cost or spend
metrics that you want to minimize.

## Add descriptions and show/hide dimensions and KPIs

Also on the Schemas page, you can add short descriptions for the dataset and the dataset’s
dimensions. This is useful to include important dataset context that user’s may not have such as how
KPIs were defined or what kind of values are stored in a dimension.

Dimensions and KPIs can also be hidden (or unhidden) to decrease clutter when performing an
investigation on a dataset.

## Deleting datasets

A dataset can be deleted from the BoostKPI dashboard by selecting “Edit dataset” on the right hand
side of the Schemas page. At the bottom of the edit menu, type “DELETE” into the text box and then
click the delete button.

Note that this only performs a soft delete of the dataset. If a hard delete of the BoostKPI metadata is required,
e.g., due to legal compliance reasons, please contact amit@boostkpi.com.

