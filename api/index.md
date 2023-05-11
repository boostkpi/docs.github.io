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

To authenticate to BoostKPI, grab your te_auth cookie while logged into dashboard.boostkpi.com and include it with any requests.
