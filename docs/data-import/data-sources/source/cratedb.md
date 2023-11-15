---
layout: default
title: CrateDB
parent: Data import
---

# CrateDB Integration Documentation

## Table of Parameters

| Key        | Description                               | Optional | Data Type |
|------------|-------------------------------------------|----------|-----------|
| `Host`     | Hostname or IP address of the CrateDB instance. |          | Text      |
| `Port`     | Port number on which CrateDB is running.  | Yes      | Number    |
| `Username` | Username for authentication.              |          | Text      |
| `Password` | Password for authentication.              |          | Text      |
| `Use SSL`  | Enable or disable SSL encryption.         | Yes      | Boolean   |

## Setup Information

To integrate CrateDB with our system, follow these steps:

1. **Select the CrateDB Connector:** Select the CrateDB connector on import page in `Connection` modal.

2. **Configure Connection Parameters:** Use the parameters listed above to configure the connection to your CrateDB instance.

3. **Verify Connection:** After configuring the parameters, verify the connection to ensure successful integration.

## Connection modal

![CrateDB Integration](../../../images/integration/cratedb-integration.png)

## Additional Documentation

For more details and advanced configurations, refer to the official [CrateDB Documentation](https://docs.crate.io/).

## Support

If you encounter any issues or have questions, please contact our support team.
