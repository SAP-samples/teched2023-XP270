# Exercise 3 - Check alert and resolve problem

In this exercise you will check the alert information and trigger the previously defined operation flow from the alert. Afterwards you will check that this has resolved the problem. 
## Exercise 3.1 Optional : Check e mail notification 

1.	If you configured e mail notification in step 1:
Open your e mail inbox. You should have received a mail “Welcome to SAP Cloud ALM” . Open the mail. It should look similar to below.

## Exercise 3.2 Check alert and trigger operation flow manually
Logon Data
| Application | User ID | Password | URL |
|---|---|---|---|
| SAP Cloud ALM URL | XP270-**XXX**@education.cloud.sap | coming soon | [SAP Cloud ALM](https://ad263-ptnlz9xc.eu10.alm.cloud.sap/launchpad) |

Please replace the **XXX** in the user name with your assigned number, 

2.	Logon to SAP Cloud ALM.
3.	Select “Health Monitoring”.
4.	Select the number besides “Open alerts” to open the alert list or select “alerting” in the left panel.
5.	Select the “High Disk Utilization” alert to open alert details.
Review the alert details and possible actions.
6.	Select “Actions”-->“Start Operation Flow”.
	Now you will probably see many operation flows with similar names. Search for the operation flow name with your number to ensure you select the right one. Select “Start” to trigger it.
7.	Select “Operation Flows”. Verify that the operation flow you started is displayed and has status completed .
8.	Select the Instance id to jump into the operation flow execution in SAP Automation Pilot and review the execution details
10.	Navigate to Health Monitoring and verify that disk utilization has decreased.
11.	Navigate  to the alert and select Actions --> Confirm Alert .
## Exercise 3.3 Configure the automatic triggering of the operation flow
12.	Logon to SAP Cloud ALM
13.	Select Health Monitoring.
14.	Select Configuration.
15.	Select Edit.
16.	Select Service Name “XP270-XXX”. Please replace the **XXX** with your assigned number. 
17.	Select metric type “Disk utilization” and reduce the yellow threshold to 40% to ensure that the threshold is breached earlier.
18.	Select events.
19.	Select event type “High Disk Utilization”.
20.	Switch on “Start Operation Flow”.
21.	Select “Add Operation Flow”.
22.	22.	Now you will probably see many operation flows with similar names. Search for the operation flow with your number and select it.
23.	Close the configuration UI.
24.	Wait until the alert appears again. (Eventually you cloud also restart the application).
25.	Select the “High Disk Utilization” alert to open alert details.
26.	Select Operation Flows . Check that the Operation Flow has been triggered automatically this time. 



