# WA SOC Overwatch - BETA - 

**WA SOC Overwatch** is a live external passive monitoring service based on [Shodan Monitor](https://monitor.shodan.io/) that the WA SOC Threat Intelligence Team uses to track for changes of key internet facing assets. The goal of this service is to detect for high risk and potential threats that are associated to the following **Overwatch Factors** and to share this threat intelligence to our customers:

> Overwatch Factors
- [x] verfied compromised or malware detected services
- [x] unverfied compromised or malware detected services
- [x] exposed databases
- [x] iot services detection
- [x] restricted ports detected
- [x] uncommon ports detected
- [x] vulnerable and unverfied services
- [x] new service detected
- [x] industrial control system detected
- [x] internet scanner activity
- [x] expired ssl certifciation detected

# Onboarding and Installation

## Prerequisite 

> Azure Permissions
- Resource Group Owner
- Azure Sentinel Contributor

> Files

As part of the **beta** the following files will be required.

|Steps | File  | Description |
|----------- | ------------- | ------------- |
| **Workflow** | _overwatch_workflow.json_ | The webhook logic app work flow **_template_** to pull WA SOC Overwatch detection into your Azure Tenant - This flow will proceed to push the detection into a MS Sentinel Workspace |
| **Rules** | _sentinel_rule_v1.json_ | The pre-made Microsft Sentinel Rule that will trigger an incident based upon a new overwatch detected |

## Onboarding

> **_NOTE:_** This service is for WA SOC Customers **only**.

To get access to the WA SOC Overwatch service - Please fill in the following application form and we will provide a link with further details. 

Once your onboarding application form has been approved and finalised. Proceed with the _**Installation Steps**_ 

## Installation Steps

### Workflow

1. Deploy the **Workflow** template to your Azure Tenant ([**Azure portal**](https://portal.azure.com/) login required).

    > Easy Deploy

    Click on the following **Deploy to Azure** buttom to deploy the cusom template.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fwagov%2Foverwatch%2Fmain%2Fdeployment%2Foverwatch_workflow.json)

    > Manual Deployment 

    [Follow the manual deployment guides](https://github.com/wagov/azure-guides/blob/main/guides/azure-custom-templates.md)

2. Once the [Template](/deployment/overwatch_workflow.json) has been deployed, select the **Basic** Tab, and fill the following parameters to complete the deployment of the playbook.

 | Parameters  | Description |
| ------------- | ------------- |
| **Resource Group** | Select a Resource Group to host the logic app  |
| **Location** | Select a Azure region to host the logic app  |
| **Playbook Name** | The name of the Logic App Playbook -- _Default Name: WASOCOverwatchWorkflow_  |
| **Log Analytics Connection Name** | The connection name of the permission field for connection the logic app to log analytics. -- _Default Name: WASOCOverwatchConnection_ |
| **Log Analytics Workspace ID** | The workspace ID of the log analytic workspace connection. Further information found [here](https://github.com/wagov/azure-guides/blob/main/guides/log-analytic-ID-and-keys.md)  |
| **Log Analytics Workspace Key** | The workspace key of the log analytic workspace connection. Further information found [here](https://github.com/wagov/azure-guides/blob/main/guides/log-analytic-ID-and-keys.md) |
| **Authentication Key** | The authentication key to prevent unauthorised ingest from webhook endpoint. |

3. Once the parameters has been filled, proceed to _**Review + Create**_ step for azure to verify the template, and once the verify is completed, then _**Create**_ the finalise the Logic App Workflow.

### Rules

To detect the WA SOC Overwatch events to Microsoft Sentinel. Deploy this [Rule template](/deployment/sentinel_rule_v1.json) using the [guide](https://docs.microsoft.com/en-us/azure/sentinel/import-export-analytics-rules#import-rules) to import rules.

> **_NOTE:_** This step should be completed once a WA SOC Overwatch event has been initially ingested into the Log Analytics Workspace. Initial ingested data may take an hour or more to appear as a querable table.

# Support

For any inquires about the beta - Please foward your questions to `cybersecurity@dpc.wa.gov.au`


