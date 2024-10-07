# Context

As already explaind in lesson "[Observing Your Apps Running](https://learning.sap.com/learning-journeys/discovering-devops-with-sap-btp/observing-your-apps-running-on-sap-btp_b7da3104-1a26-499f-8f02-da0de6917dd8)", you are implementing an integrated monitoring and automated incident response system for a cloud app deployed on SAP BTP, Cloud Foundry. Cloud Foundry Audit Events and app crash events are automatically collected by SAP Alert Notification and sent to SAP Cloud ALM for central problem detection. SAP Cloud ALM triggers alerts to the DevOps team and enables navigation to observability tools like SAP Cloud Logging for issue resolution. It can also trigger SAP Automation Pilot, which gathers logs, stores them in a ticket, and assigns it to the DevOps team for further action.

All the interactions and products' intgerationd are visualised within the diagram shared below: 
![](/exercises/ex5/images/solution-overview.png)

## Steps needed for use case implementation   

To implement an integrated monitoring and automated incident response system for your cloud app in SAP BTP, follow these steps:

1. **Set up the integration between SAP Alert Notification service for SAP BTP and SAP Cloud ALM**
[Integrate SAP Alert Notification with SAP Cloud ALM]([url](https://support.sap.com/en/alm/sap-cloud-alm/operations/expert-portal/health-monitoring/health-monitoring-setup-configuration/health-monitoring-for-sap-btp-cf.html?anchorId=section_322971014_co)): Activate the switch in SAP Cloud ALM for "SAP BTP: Application Crash" to ensure crash events are automatically ingested.

2. **Integrate SAP Automation Pilot with SAP Cloud ALM**: [Connect SAP Automation Pilot with SAP Cloud ALM to automate responses to incidents]([url](https://support.sap.com/en/alm/sap-cloud-alm/operations/expert-portal/operation-automation/automation-pilot.html)).

3. **Configure SAP Alert Notification to Collect Cloud Foundry Audit Events:** [Enable the SAP Alert Notification service to start collecting audit events from your Cloud Foundry app]([url](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/application-events)).

4. **Create an Automation Flow in SAP Automation Pilot**: Design an automated response to app crashes by performing the following:
- Use the commands "GetCfAppState" and "GetCfAppEvents" to retrieve the latest app state and the most recent 20 events for your Cloud Foundry app.
- Create a custom command to fetch the last 100 lines from the app's log file.
- Generate a ticket in your Ticket Management System (e.g., Jira) with the collected app insights for faster troubleshooting.
_Check the [provided content and available commands in SAP Automation Pilot]([url](https://help.sap.com/docs/automation-pilot/automation-pilot/provided-catalogs?version=Cloud))_

5. **Configure SAP Cloud ALM for Health Monitoring**: [In SAP Cloud ALM, enable health monitoring for app crashes]([url](https://community.sap.com/t5/technology-blogs-by-sap/cloud-alm-health-monitoring-for-event-configuration/ba-p/13575560)). Set the following actions:
- Send email notifications to the DevOps team for immediate awareness of the issue.
- Trigger the automation flow in SAP Automation Pilot to gather logs and create a ticket for problem resolution.

By following these steps, you'll set up an integrated system for monitoring and automating responses to app crashes, ensuring quick detection and resolution.


### Define commands for an automated troubleshooting in SAP Automation Plot   
Within this step you could benefit out of a custom command created in SAP Automation Pilot. See the exact command code that you can import directly in your SAP Automation Pilot. 

```
{
  "configuration": {
    "values": [
      {
        "alias": "RegionData",
        "valueFrom": {
          "inputReference": "metadata-sapcp:CfRegionData:1",
          "inputKey": "$(.execution.input.region)"
        }
      }
    ],
    "output": {
      "recentLogs": "$(.CollectLogs.output.output[1:])"
    },
    "executors": [
      {
        "execute": "scripts-sapcp:ExecuteScript:2",
        "input": {
          "stdin": "$(.execution.input.password | toEscapedJson)",
          "environment": "{\"CF_API\":\"$(.RegionData.cfApiUrl)\",\"CF_ORG\":\"$(.execution.input.subAccount)\",\"CF_SPACE\":\"$(.execution.input.resourceGroup)\",\"CF_APP\":\"$(.execution.input.resourceName)\",\"CF_USER\":\"$(.execution.input.user)\",\"CF_IDP\":\"$(.execution.input.identityProvider)\",\"CF_PASSWORD\":\"$(.execution.input.password | toEscapedJson)\"}",
          "script": "set -e\n\n# echo \"Logging in to Cloud Foundry...\"\ncf login -a \"$CF_API\" --origin \"$CF_IDP\" -u \"$CF_USER\" -p \"$CF_PASSWORD\" -o \"$CF_ORG\" -s \"$CF_SPACE\"\n\n# Fetch recent logs for the specified CF app\ncf logs \"$CF_APP\" --recent\n"
        },
        "alias": "CollectLogs",
        "description": null,
        "progressMessage": null,
        "initialDelay": null,
        "pause": null,
        "when": null,
        "validate": null,
        "autoRetry": null,
        "repeat": null,
        "errorMessages": [],
        "dryRun": null
      }
    ],
    "listeners": []
  },
  "id": "welcome-<<<TENANT_ID>>>:CollectRecentCfAppLogs:1",
  "name": "CollectRecentCfAppLogs",
  "description": "Restarts a Cloud Foundry application in a rolling manner or quickly, by stopping all instances simultaneously",
  "catalog": "welcome-<<<TENANT_ID>>>",
  "version": 1,
  "inputKeys": {
    "resourceGroup": {
      "type": "string",
      "sensitive": false,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": "Technical name of a Cloud Foundry Space, e.g.: my-space-demo-1"
    },
    "password": {
      "type": "string",
      "sensitive": true,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": "Cloud Foundry user's password"
    },
    "resourceName": {
      "type": "string",
      "sensitive": false,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": "Technical name of a Cloud Foundry application, e.g.: my-app"
    },
    "region": {
      "type": "string",
      "sensitive": false,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": " Technical name of a Cloud Foundry region (as defined in CfRegionData), e.g. cf-eu10, cf-br10, etc."
    },
    "user": {
      "type": "string",
      "sensitive": false,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": "UserID/Email of the Cloud Foundry user which will be used for authentication"
    },
    "subAccount": {
      "type": "string",
      "sensitive": false,
      "required": true,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": null,
      "defaultValueFromInput": null,
      "description": "Technical name of a Cloud Foundry Organization, e.g.: my-org-name-1"
    },
    "identityProvider": {
      "type": "string",
      "sensitive": false,
      "required": false,
      "minSize": null,
      "maxSize": null,
      "minValue": null,
      "maxValue": null,
      "allowedValues": null,
      "allowedValuesFromInputKeys": null,
      "suggestedValues": null,
      "suggestedValuesFromInputKeys": null,
      "defaultValue": "sap.ids",
      "defaultValueFromInput": null,
      "description": "Identity provider to be used. By default it is SAP ID Service (sap.ids). To use a custom IdP, enter origin key from the CF Org/Space members section"
    }
  },
  "outputKeys": {
    "recentLogs": {
      "type": "array",
      "sensitive": false,
      "description": null
    }
  },
  "tags": {
    "env": "cf"
  }
}
```

## Summary

You have now the command for automated troubleshooting modeled and stored in SAP Automation Pilot and also have integrated your SAP Cloud ALM to SAP Automation Pilot. Now the commands in questions can be triggered automatically or manually via Cloud ALM. 
