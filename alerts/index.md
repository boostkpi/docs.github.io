

## What are alerts?

Our blog post at [BoostKPIs alerting features](https://blog.boostkpi.com/BoostKPIs-alerting-features/) provides an overview of our alerts.

## Setting up alerts with AI assistance

You can receive AI-powered assistance setting up alerts by navigating to [alert creation](https://dashboard.boostkpi.com/app/#/self-serve/create-alert) and clicking on the 'AI-powered alert creation' button in the top left of the page.

Ask the AI to write an alert configuration using natural language. The AI will return to you a YAML configuration that you can copy into the main alert configuration editor.

After copying the alert, remember to add the new alert's name to a subscription to receive a notification when the alert finds an anomaly. An example is provided below:

```
subscriptionGroupName: 'subscription_name'

application: company-name

subscribedDetections:
- 'new_alert_name' # Add your new alert's name here

alertSchemes:
- type: EMAIL
  params:
    recipients:
      to:
      - email@company-name.com
```

## Example alerts

Our blog post at [Sample alerting configurations](https://blog.boostkpi.com/Sample-alerting-configurations/) provides example alerts.

## Support for rolling-7-day alerts

Our blog post at [Sample alerting configurations](https://blog.boostkpi.com/Sample-alerting-configurations/) shows an example of a rolling 7-day alert for a daily dataset.

## Alerts based on target

```
Q: Do you support alerts based on targets? For example, 
if I have monthly (campaign) spend targets by country, 
can BoostKPI alert me when my daily spend is outside 20% 
of the spend required to hit my monthly target?
```

Yes, few of our customers use this feature in production. Please contact us for details.

## Alerts routing to specific email address
```
Q: I want some alerts being routed to one group email address 
and other alerts being routed to another group email. Is that possible?
```

Yes, you can do so by creating two subscription groups. Please ask your BoostKPI account manager. 
