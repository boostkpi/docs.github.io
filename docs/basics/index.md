---
layout: default
title: Basics
nav_order: 3
---

# Basics
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## What is a dataset / KPI?

A dataset represents a time-series of metrics or KPIs broken down by 
multiple dimensions of interest. For example, an e-commerce marketplace’s revenue dataset may be 
an hourly data of view products, orders and revenue broken down by:
Platform (that the user is using to make the purchase)
- Brand
- Country
- Continent
- Product category

For example, the table below shows a dataset that is suitable for 
analysis by BoostKPI.

![Dataset preview table](../images/dataset-preview.png)

A KPI is an important metric that the business uses to make important 
decisions. In the above example, revenue, orders, and view_products 
are example KPIs.

## Managing datasets

You can add new datasets by clicking on the “Add dataset” button. You can then upload 
a csv or setup a dataset as a result of a sql query. 

If you no longer plan to use a dataset, you can click on “Edit dataset” (in the schemas tab) and hit “Delete” to delete the dataset.

![Edit dataset: image](../images/edit-dataset.png)

You can also use the search bar (above the list of datasets) to search for a specific dataset.


## Creating a derived KPI

Derived KPIs can be added to a dataset on the Schemas page by selecting the “Add derived KPI” button
on the right hand side. In the menu that opens, you can either select a derived KPI to copy from an
existing dataset or create a new one by dragging and dropping metric names.

Currently BoostKPI only supports derived KPIs that are a ratio (of the form X / Y) or a percentage (of the form X*100/Y).

![Derived KPI button: image](../images/derived-kpi.png)

You can then create a new KPI such as views-to-purchases-ratio defined as 
the ratio of the number of purchases to the number of views by doing a 
drag and drop.

![Derived KPI modal: image](../images/derived-kpi-modal.png)

## Marking KPI as Inverse (or a cost KPI)
On the dataset’s Schemas page, KPIs can be marked as “Inverse”. This indicates that an increase in
the KPI should be reflected as a bad change while a decrease should be reflected as a good change.
When set, an inverse KPI will use red numbers for increases and blue numbers for decreases (the
opposite coloring of normal KPIs). This is useful for interpreting change when viewing cost or spend
metrics that you want to minimize.

Marking a KPI as a cost metric reverses the colors in the heatmap, the 
drilldown, and the alerts.  Examples of cost metrics are CPC (cost per click) or CPL (cost per lead).

![Inverse KPI : image](../images/inverse-kpi.png)



## Raw data preview

You can see raw data used for analysis on Dashboard -> Schemas > Preview dataset.

![Preview dataset - raw data: image](../images/preview-dataset-raw.png)

## Dashboard-view

A dashboard-view enables users to customize the way they view KPIs in 
BoostKPI. For example, a manager at an online retailer might want to 
see the revenue and AOV in the US at a weekly level. To do so, she 
can click on the revenue KPI, add the appropriate country filter, update 
the charts, add the AOV chart, and then save it as a dashboard-view.

The dashboard-view is then present on the dataset page. She can also get 
a daily update of the latest data emailed to her by clicking on “notify” 
when viewing the contents of a dashboard-view. (The url includes a viewId 
when a dashboard-view is being displayed).

![Creation of dashboard view: image](../images/dashboard-view.png)

## Lookup datasets

A lookup dataset is a mapping dataset that specifies the mapping of 
existing column values from a (time-series) dataset to a new column. 
Lookup datasets can currently only be added via a csv import. 
[See this FAQ on how to create a lookup dataset.](/docs/data-import/#csv-file-import)
