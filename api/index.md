## How can I fetch anomalies through the API?

BoostKPI provides programmatic access to anomalies. They can be fetched via a GET request to the following endpoint `dashboard.boostkpi.com/anomalies/json`.

The endpoint supports the following query parameters:

- `anomalyWindowStart` and `anomalyWindowEnd` - Returns anomalies whose duration overlap the provided window, inclusive on the start and exclusive on the end. The timestamps should be provided in milliseconds form, e.g., `Sun Jan 01 2023 00:00:00` is `1672531200000`.
- `createTimeStart` and `createTimeEnd` - Returns anomalies that were created between the two timestamps, inclusive on the start and exclusive on the end. The timestamps should be provided in milliseconds form, e.g., `Sun Jan 01 2023 00:00:00` is `1672531200000`.
- `anomalyIds` - Returns only the anomalies with the provided ids. The ids should be provided as a comma delimited list of anomaly ids, e.g., `1,2,3`.

At least one of the filters is required.

Anomalies are returned grouped by detection in the following json format:

```
[
  {
    alertName: "foo", // The name of the detection
    kpi: "kpi1", // The kpi the detection watches
    desc: "Detects changes in kpi1", // A brief description of the detection's behavior
    anomalies: [
      {
        id: 1, // The id of the anomaly
        start: 1672531200000, // The timestamp when the anomaly began
        end: 1672617600000, // The timestamp when the anomaly ended
        type: "DEVIATION", // The type of the anomaly
        current: 100, // The value of the kpi during the anomaly
        baseline: 200, // The expected baseline kpi value
        dimensions: { // The dimension slice that the anomaly occurred in
          dimension_name: [ // Name of the dimension, e.g., platform, country, etc.
            "dimension_value" // Value of the dimension, e.g., iOS, US, etc.
          ]
        }
      },
      {
        id: 2,
        ...
      },
      ...
    ]
  },
  {
    alertName: "bar",
    kpi: "kpi1",
    ...
  },
  {
    alertName: "baz",
    kpi: "kpi2",
    ...
  },
  ...
]
```

## How can I fetch the drilldown data through the API?

The data in the drilldown table can be fetched by a GET request to 'dashboard.boostkpi.com/dashboard/summary/autoDimensionOrder'.

The endpoint has the following required query parameters:

- 'metricId' - the metric id, this can be found in the url by opening an investigation of the metric
- 'currentStart' and 'currentEnd' - the investigation time range endpoints in milliseconds, takes an inclusive start and an exclusive end
- 'baselineStart' and 'baselineEnd' - the comparison time range endpoints in milliseconds, takes an inclusive start and an exclusive end
- 'summarySize' - controls the analysis complexity, a higher number will take longer to return, we recommend using 25

The endpoint supports the following optional query parameters:

- 'depth' - the number of dimensions to breakdown by (default value: 3)
- 'dimensions' - dimensions to use in the breakdown (defaults to an automated dimensional analysis and selection)
- 'excludedDimensions' - dimensions to exclude as options from the automated analysis and selection

The endpoint will respond with data in the following json format:

```
{
  datasetId: 2, // The id of the dataset for the provided metric
  metricId: 1, // The metric id from the request
  currentTotal: 100, // Total metric value during the current time range
  baselineTotal: 150, // Total metric value during the baseline time range
  dimensions: [ // The dimensions the summary information will be broken down by, comes either from automatic analysis or the query param in the request
    'dim1",
    "dim2",
    "dim3"
  ],
  responseRows: [
    {
      currentValue: 20,
      baselineValue: 30,
      percentageChange: "-33.333%",
      contributionChange: "5%",
      contributionToOverallChange: "10%",
      names: [ // The dimension values for this row
        "foo", // Dimension values match in order with the dimensions
        "(ALL)", // "ALL" represents that the summary rolled up the row along this dimension
        "(ALL)-" // "(ALL)-" represents all of the values not present in any other row, e.g., it might represent the rollup of a long tail of dimension values
      ],
      otherDimensionValues: [ // The dimension values for any "(ALL)-" entries in the row, may be blank or incomplete for dimensions with high numbers of values
        "bar",
        "baz"
      ],
      cost: 1000 // An estimate of the importance of the change in a row, higher is more important
    },
    ...
  ],
  gainer: [
    ... // A summary of the cost for high importance single dimension values
  ],
  loser: [
    ...
  ],
  dimensionCost: [ // Costs associated with including particular dimensions in the summary, higher is more important
    {
      dimensionName: "dim1",
      cost: 1000
    },
    ...
  ]
}
```

## How can I fetch the breakdown or heatmap data through the API?

The data in the breakdown or heatmap table can be fetched by a POST request to 'dashboard.boostkpi.com/rootcause/metric/breakdown'.

The request should have a json body containing:

```
{
  metric: {
    id: 1, // The id of the metric, this can be found in the url for an investigation of the metric
    dims: [ // Optional dimension filters to use
      {
        label: "country", // The dimension name to filter
        included: [ // Can be an include or an exclude filter
          "US", "CA", ... // The dimension values to filter
        ]
      },
      ...
      {
        label: "platform",
        excluded: [
          "iOS"
        ]
      }
    ]
  },
  start: 1682899200000, // The inclusive start of the investigation range as a timestamp in milliseconds, this timestamp is May 1st, 2023
  end: 1683417600000, // The exclusive end of the investigation range as a timestamp in milliseconds, this timestamp is May 7th, 2023
  offset: "wo1w", // A string representing the offset for comparison: "wo1w" to compare to the previous week, "mo3m" to compare to three months prior
  limit: 50 // The number of top dimension values to return for each dimension, values past the limit will be rolled up into other
}
```

The endpoint will respond with breakdown data in the following json format:

```
{
  result_complete: {
    dimension_name1: {
      dimension_value1: {
        current: 10, // The metric value for dimension_value1 during the start to end time range
        offset: 8 // The metric value for dimension_value1 during the offset comparison time range
      },
      ...
      dimension_value50: {
        current: 1,
        offset: 2
      }
    },
    dimension_name2: {
      ...
    },
    ...
  },
  totals: { // The overall metric totals, these values can be used to compute the tail metric values past the requested limit
    current: 100, // The value of the metric between the start and end time
    offset: 90  // The value of the metric during the offset comparison time range
  },
  performanceId: 1 // An id for internal BoostKPI use
}
```


## How do I authenticate when using the API?

To authenticate to BoostKPI, grab your te_auth cookie while logged into dashboard.boostkpi.com and include it with any requests. See screenshot below on how to grab the te_auth cookie.
![Finding your auth cookie](../../images/auth_cookie.jpg) 

With the cookie set, here is an example request using the tool curl that can be executed on a Mac Terminal.

```
curl --cookie te_auth=665ceb3c7272adddfa9f54fd603a6ebed0033a4b5b8391344ab47e756dd59935 https://dashboard.boostkpi.com/anomalies/json\?anomalyWindowStart\=1683717689000\&anomalyWindowEnd\=1683917689000
```


