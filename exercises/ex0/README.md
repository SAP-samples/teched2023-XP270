# Exercise 0 - Getting Started

A custom-developed Java application “perfumeStore” was deployed in SAP BTP in a space “prod” in subaccount “XP270-XXX”. You are responsible for operations of this application.  In this exercise you will verify that all prerequisites for the monitoring of the subaccount and the application are fulfilled and you will start the application.                                       

> [!IMPORTANT]
> Please replace the XXX in the exercises always with your assigned number to avoid conflicts with other participants. You can find your assigned number on the sign on your table.

## Login Information
Please replace the XXX in the user name with your assigned number (e.g. XP270-001@education.cloud.sap).
| Application | User ID | Password | URL |
|---|---|---|---|
| SAP BTP Cockpit | XP270-**XXX**@education.cloud.sap | coming soon | https://emea.cockpit.btp.cloud.sap/cockpit/?idp=tdct3ched1.accounts.ondemand.com#/globalaccount/e2a835b0-3011-4c79-818a-d7767c4627cd/accountModel&//?section=SubaccountsSection&view=TreeTableView |

## Connect to SAP BTP CF subaccount and start your app

1.	Select the SAP  BTP cockpit URL. Enter user name and password and flag “Keep me signed in”. Select Continue.
<br>![](/exercises/ex0/images/001.png)
3.	Select subaccount XP270-XXX (replace XXX with your number).
<br>![](/exercises/ex0/images/002.png)
3.	Select Destinations. Select destination CALM_datacollector_prod.
<br>![](/exercises/ex0/images/003.png)
4.	Review the destination configuration.  Please do not change anything here.
<br>![](/exercises/ex0/images/004.png)
Explanation:
This destination points to the SAP Cloud ALM tenant responsible for monitoring. Without this destination, SAP Cloud ALM cannot receive monitoring metrics from the space.
5. Select Check Connection. Verify that you receive a success message “Connection to "CALM_datacollector_prod " established. Response returned: "404: Not Found"”. Return code 404 is expected and does not indicate that something is wrong .
<br>![](/exercises/ex0/images/005.png)
6. Select Close.
7.	Select Spaces after choosing Cloud Foundry from the left side menu. 
8.	Navigate to  the space by clicking on the space name.
<br>![](/exercises/ex0/images/006.png)
9. Double click on the space name prod and check that there is an application “perfumestoreXX” deployed in the space . The application is currently in status stopped. <br>![](/exercises/ex0/images/007.png)
10.	Click on the application name ‘perfumestoreXX’ .
11.	Select User Provided Variables. Check the variable JBP_CONFIG_JAVA_OPTS
<br>![](/exercises/ex0/images/008.png)

7.	
``` abap
 DATA(params) = request->get_form_fields(  ).
 READ TABLE params REFERENCE INTO DATA(param) WITH KEY name = 'cmd'.
  IF sy-subrc <> 0.
    response->set_status( i_code = 400
                     i_reason = 'Bad request').
    RETURN.
  ENDIF.
```

## Summary

Now that you have ... 
Continue to - [Exercise 1 - Exercise 1 Description](../ex1/README.md)
