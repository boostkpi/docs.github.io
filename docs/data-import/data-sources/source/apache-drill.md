---
layout: default
title: Apache Drill
description: Easily connect Apache Drill to BoostKPI with our step-by-step guide in our FAQ page. Unlock the potential of your data in Apache Drill by seamlessly integrating it with BoostKPI for in-depth analysis and reporting. Our comprehensive instructions will walk you through the process, ensuring a smooth and efficient connection. Dive into the details and harness the power of data analytics with Apache Drill and BoostKPI combined. 
parent: Data import
---

# Apache Drill Integration Documentation

## Table of Parameters

| Key               | Description                                          | Optional | Data Type |
|-------------------|------------------------------------------------------|----------|-----------|
| `Connection name` | A user-defined name for the connection.              |          | Text      |
| `Host`            | Hostname or IP address of the Apache Drill instance. |          | Text      |
| `Port`            | Port number on which Apache Drill is running.        | Yes      | Number    |
| `Username`        | Username for authentication.                         |          | Text      |
| `Password`        | Password for authentication.                         |          | Text      |
| `Default schema`  | Default schema for queries.                          |          | Text      |
| `Use SSL`         | Enable or disable SSL encryption.                    | Yes      | Boolean   |

## Setup Information

To integrate Apache Drill with our system, follow these steps:

1. **Select the Apache Drill Connector:** Select the Apache Drill connector on import page
   in `Connection` modal.

2. **Configure Connection Parameters:** Use the parameters listed above to configure the connection
   to your Apache Drill instance.

3. **Verify Connection:** After configuring the parameters, verify the connection to ensure
   successful integration.

## Connection modal

![Apache Drill Integration](../../../images/integration/apache-drill-integration.png)

## Additional Documentation

For more details and advanced configurations, refer to the
official [Apache Drill Documentation](https://drill.apache.org/docs/).

## Support

If you encounter any issues or have questions, please contact our support team.
