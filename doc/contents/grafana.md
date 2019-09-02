# Grafana

||||
|---|---|---|
| **Type** | Dashboards/Monitoring ||
| **Auth** | API token ||
| **Method** | HTTP Header injection ||
| **Chrome extension** | Requestly ||

## Introduction

Grafana can use an API key to authenticates. You can create an API token on `Configuration` > `API Keys`.

## Steps

1. Create an API Key: `Configuration` > `API Keys` in the Grafana settings

2. Give a `Key name` (screens for ex.) and role `Viewer` and set the `Time to live` between one month and one year, depending of your company policy.

3. Save your `Key` into a safe place (1Password for ex.) 

4. Launch the Google profile created for your screens to add a new Requestly Rule and sync it with all your screens.

5. Launch the Requestly Chrome extension

6. Click on `New Rule` > `Modify Headers`

7. Set a `Rule Name` (Grafana)

8. In the `Header` field, add `Authorization`

9. On the `Value` field, set: `Bearer {put your API token here}`

10. Set the last field with the URL of your Grafana instance to add this HTTP header only when the screens call your Grafana instance
