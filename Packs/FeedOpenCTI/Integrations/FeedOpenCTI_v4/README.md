Ingest indicator feeds from OpenCTI. 
This integration was integrated and tested with version v4.0.7 of OpenCTI Feed.
Compatible with OpenCTI v4 instances. For v3.* and lower OpenCTI versions use the OpenCTI Feed v3 integration.
## Configure OpenCTI Feed v4 on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for OpenCTI Feed v4.
3. Click **Add instance** to create and configure a new integration instance.

    | **Parameter** | **Description** | **Required** |
    | --- | --- | --- |
    | Base URL |  | True |
    | API Key |  | True |
    | Indicators Type to fetch | The indicator types to fetch. Out of the box indicator types supported in XSOAR are: "Account", "Domain", "Email", "File", "Host", "IP", "IPv6", "Registry Key", and "URL". The rest will not cause automatic indicator creation in XSOAR. The default is "ALL". | True |
    | Max. indicators per fetch |  | False |
    | Fetch indicators |  | False |
    | Indicator Reputation | Indicators from this integration instance will be marked with this reputation | False |
    | Source Reliability | Reliability of the source providing the intelligence data | True |
    | Traffic Light Protocol Color | The Traffic Light Protocol \(TLP\) designation to apply to indicators fetched from the feed | False |
    |  |  | False |
    |  |  | False |
    | Feed Fetch Interval |  | False |
    | Tags | Supports CSV values. | False |
    | Bypass exclusion list | When selected, the exclusion list is ignored for indicators from this feed. This means that if an indicator from this feed is on the exclusion list, the indicator might still be added to the system. | False |
    | Trust any certificate (not secure) |  | False |
    | Use system proxy settings |  | False |

4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### opencti-get-indicators
***
Gets indicators from the feed.


#### Base Command

`opencti-get-indicators`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| limit | The maximum number of indicators to return per fetch. The default value is "50". Maximum value is "500". | Optional | 
| indicator_types | The indicator types to fetch. Out of the box indicator types supported in XSOAR are: "Account", "Domain", "Email", "File", "Host", "IP", "IPv6", "Registry Key", and "URL". The rest will not cause automatic indicator creation in XSOAR. The default is "ALL". Possible values are: ALL, Account, Domain, Email, File, Host, IP, IPv6, Registry Key, URL. Default is ALL. | Optional | 
| last_run_id | The last ID from the previous call from which to begin pagination for this call. You can find this value at OpenCTI.IndicatorsList.LastRunID context path. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| OpenCTI.Indicators.IndicatorsList.type | String | Indicator type. | 
| OpenCTI.Indicators.IndicatorsList.value | String | Indicator value. | 
| OpenCTI.Indicators.IndicatorsList.id | String | Indicator id. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.createdBy | Unknown | The creator of indicator. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.score | Number | Indicator score. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.description | String | Indicator Description. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.objectLabel | Unknown | Indicator labels. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.objectMarking | Unknown | Indicator marking definitions. | 
| OpenCTI.Indicators.IndicatorsList.rawJSON.externalReferences | Unknown | Indicator external references. | 
| OpenCTI.Indicators.LastRunID | String | the id of the last fetch to use pagination. | 


#### Command Example
```!opencti-get-indicators limit=2 indicator_types="IP"```

#### Context Example
```json
{
    "OpenCTI": {
        "Indicators": {
            "IndicatorsList": [
                {
                    "id": "33bd535b-fa1c-41e2-a6f9-80d82dd29a9b",
                    "rawJSON": {
                        "createdBy": {
                            "contact_information": null,
                            "created": "2021-02-14T11:57:57.259Z",
                            "description": "test playbook organization",
                            "entity_type": "Organization",
                            "id": "1e12fe87-db3e-4838-8391-6910547bf60d",
                            "modified": "2021-02-14T11:57:57.259Z",
                            "name": "Test_Organization",
                            "objectLabel": [],
                            "objectLabelIds": [],
                            "parent_types": [
                                "Basic-Object",
                                "Stix-Object",
                                "Stix-Core-Object",
                                "Stix-Domain-Object",
                                "Identity"
                            ],
                            "roles": null,
                            "spec_version": "2.1",
                            "standard_id": "identity--b3d82735-562e-5641-add7-1b45adf8fba2",
                            "x_opencti_aliases": null,
                            "x_opencti_organization_type": null,
                            "x_opencti_reliability": "B"
                        },
                        "createdById": "1e12fe87-db3e-4838-8391-6910547bf60d",
                        "created_at": "2021-02-18T08:04:10.997Z",
                        "entity_type": "IPv4-Addr",
                        "externalReferences": [],
                        "externalReferencesIds": [],
                        "id": "33bd535b-fa1c-41e2-a6f9-80d82dd29a9b",
                        "indicators": [],
                        "indicatorsIds": [],
                        "objectLabel": [
                            {
                                "color": "#7ed321",
                                "createdById": null,
                                "id": "fa57f98e-f2f5-45fd-97f2-bf2c53119044",
                                "value": "devdemisto"
                            },
                            {
                                "color": "#5d0d8a",
                                "createdById": null,
                                "id": "07cfae2d-6cc9-42c5-9fd0-32eff8142404",
                                "value": "test-label-1"
                            }
                        ],
                        "objectLabelIds": [
                            "fa57f98e-f2f5-45fd-97f2-bf2c53119044",
                            "07cfae2d-6cc9-42c5-9fd0-32eff8142404"
                        ],
                        "objectMarking": [
                            {
                                "created": "2021-01-26T11:31:07.317Z",
                                "createdById": null,
                                "definition": "TLP:RED",
                                "definition_type": "TLP",
                                "entity_type": "Marking-Definition",
                                "id": "c9819001-c80c-45e1-8edb-e543e350f195",
                                "modified": "2021-01-26T11:31:07.317Z",
                                "standard_id": "marking-definition--5e57c739-391a-4eb3-b6be-7d15ca92d5ed",
                                "x_opencti_color": "#c62828",
                                "x_opencti_order": 4
                            }
                        ],
                        "objectMarkingIds": [
                            "c9819001-c80c-45e1-8edb-e543e350f195"
                        ],
                        "observable_value": "1.1.1.1",
                        "parent_types": [
                            "Basic-Object",
                            "Stix-Object",
                            "Stix-Core-Object",
                            "Stix-Cyber-Observable"
                        ],
                        "spec_version": "2.1",
                        "standard_id": "ipv4-addr--1d5586d0-4327-5e1c-9317-19c1e0cf8ec0",
                        "updated_at": "2021-02-18T08:04:10.997Z",
                        "value": "1.1.1.1",
                        "x_opencti_description": "test fetch one",
                        "x_opencti_score": 100
                    },
                    "type": "IP",
                    "value": "1.1.1.1"
                },
                {
                    "id": "700c8187-2dce-4aeb-bf3a-0864cb7b02c7",
                    "rawJSON": {
                        "createdBy": {
                            "contact_information": null,
                            "created": "2021-02-14T11:57:57.259Z",
                            "description": "test playbook organization",
                            "entity_type": "Organization",
                            "id": "1e12fe87-db3e-4838-8391-6910547bf60d",
                            "modified": "2021-02-14T11:57:57.259Z",
                            "name": "Test_Organization",
                            "objectLabel": [],
                            "objectLabelIds": [],
                            "parent_types": [
                                "Basic-Object",
                                "Stix-Object",
                                "Stix-Core-Object",
                                "Stix-Domain-Object",
                                "Identity"
                            ],
                            "roles": null,
                            "spec_version": "2.1",
                            "standard_id": "identity--b3d82735-562e-5641-add7-1b45adf8fba2",
                            "x_opencti_aliases": null,
                            "x_opencti_organization_type": null,
                            "x_opencti_reliability": "B"
                        },
                        "createdById": "1e12fe87-db3e-4838-8391-6910547bf60d",
                        "created_at": "2021-02-22T08:45:48.778Z",
                        "entity_type": "IPv4-Addr",
                        "externalReferences": [],
                        "externalReferencesIds": [],
                        "id": "700c8187-2dce-4aeb-bf3a-0864cb7b02c7",
                        "indicators": [],
                        "indicatorsIds": [],
                        "objectLabel": [
                            {
                                "color": "#7ed321",
                                "createdById": null,
                                "id": "fa57f98e-f2f5-45fd-97f2-bf2c53119044",
                                "value": "devdemisto"
                            }
                        ],
                        "objectLabelIds": [
                            "fa57f98e-f2f5-45fd-97f2-bf2c53119044"
                        ],
                        "objectMarking": [
                            {
                                "created": "2021-01-26T11:31:07.238Z",
                                "createdById": null,
                                "definition": "TLP:AMBER",
                                "definition_type": "TLP",
                                "entity_type": "Marking-Definition",
                                "id": "9128e411-c759-4af0-aeb0-b65f12082648",
                                "modified": "2021-01-26T11:31:07.238Z",
                                "standard_id": "marking-definition--f88d31f6-486f-44da-b317-01333bde0b82",
                                "x_opencti_color": "#d84315",
                                "x_opencti_order": 3
                            }
                        ],
                        "objectMarkingIds": [
                            "9128e411-c759-4af0-aeb0-b65f12082648"
                        ],
                        "observable_value": "1.2.3.4",
                        "parent_types": [
                            "Basic-Object",
                            "Stix-Object",
                            "Stix-Core-Object",
                            "Stix-Cyber-Observable"
                        ],
                        "spec_version": "2.1",
                        "standard_id": "ipv4-addr--0198f97b-e65d-5025-87e5-58bc39d4bdb4",
                        "updated_at": "2021-02-22T08:45:48.778Z",
                        "value": "1.2.3.4",
                        "x_opencti_description": "test_desc",
                        "x_opencti_score": 70
                    },
                    "type": "IP",
                    "value": "1.2.3.4"
                }
            ],
            "lastRunID": "YXJyYXljb25uZWN0aW9uOjI="
        }
    }
}
```

#### Human Readable Output

>### Indicators
>|type|value|id|
>|---|---|---|
>| IP | 1.1.1.1 | 33bd535b-fa1c-41e2-a6f9-80d82dd29a9b |
>| IP | 1.2.3.4 | 700c8187-2dce-4aeb-bf3a-0864cb7b02c7 |


### opencti-reset-fetch-indicators
***
WARNING: This command will reset your fetch history.


#### Base Command

`opencti-reset-fetch-indicators`
#### Input

There are no input arguments for this command.

#### Context Output

There is no context output for this command.

#### Command Example
```!opencti-reset-fetch-indicators```

#### Human Readable Output

>Fetch history deleted successfully