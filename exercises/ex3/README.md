# Exercise 3 - Check alert and resolve problem

In this exercise you will check the alert information and trigger the previously defined operation flow manually from the alert. Afterwards you will check that this has resolved the problem. Afterwards you will configure that the operation flow is triggered automatically the next time.
## Exercise 3.1 Optional : Check e mail notification 
1.	If you configured e mail notification in exercise 1:
Open your e mail inbox. You should have received a mail “Welcome to SAP Cloud ALM” . Open the mail. It should look similar to below.
<br>![](/exercises/ex3/images/001.png)

## Exercise 3.2 Check alert and trigger operation flow manually
In this exercise you will review the alert details and trigger the operation flow you defined in exercise 2.
Logon Data
| Application | User ID | Password | URL |
|---|---|---|---|
| SAP Cloud ALM URL | XP270-**XXX**@education.cloud.sap | Acce$$teched23 | [SAP Cloud ALM](https://ad263-ptnlz9xc.eu10.alm.cloud.sap/launchpad) |

Please replace the **XXX** in the user name with your assigned number.

2.	Logon to SAP Cloud ALM.
3.	Select “Health Monitoring”.
4.	Select the number besides “Open alerts” to open the alert list or select “alerting” in the left panel.
<br>![](/exercises/ex3/images/002.png)
5.	Select the “High Disk Utilization” alert to open alert details.
<br>![](/exercises/ex3/images/003.png)
Review the alert details and possible actions.
6.	Select “Actions”-->“Start Operation Flow”.
<br>![](/exercises/ex3/images/004.png)
	Now you will probably see many operation flows with similar names. Search for the operation flow name with your number to ensure you select the right one. Select “Start” to trigger it.
<br>![](/exercises/ex3/images/006.png)
7.	Select “Operation Flows”. Verify that the operation flow you started is displayed and has status completed .
8.	Select the instance id to jump into the operation flow execution in SAP Automation Pilot.
<br>![](/exercises/ex3/images/007.png)
9.	Review the execution details. Select output values to check the output.
<br>![](/exercises/ex3/images/008.png)
10.	Navigate to Health Monitoring. Select metric Disk Utilization -> History. Verify that disk utilization has decreased.
<br>![](/exercises/ex3/images/009.png)
11.	Navigate  to the alert and select Actions --> Confirm Alert .
<br>![](/exercises/ex3/images/005.png)
## Exercise 3.3 Configure the automatic triggering of the operation flow
You don't want to trigger the operation flow manually whenever the alert occurs so you configure the automated triggering of operation flows from the corresponding monitoring event "High Disk Utilization".
12.	Logon to SAP Cloud ALM.	
14.	Select Health Monitoring.	
16.	Select Configuration.	
18.	Select Edit.	
20.	Select Service Name “XP270-XXX”. Please replace the **XXX** with your assigned number.
21.	Select metric type “Disk utilization” and reduce the yellow threshold to 40% to ensure that the threshold is breached earlier.
<br>![](/exercises/ex3/images/010.png)
23.	Select events.
24.	Select event type “High Disk Utilization”.
25.	Switch on “Start Operation Flow”.
26.	Select “Add Operation Flow”.
27.	22.	Now you will probably see many operation flows with similar names. Search for the operation flow with your number and select it.
<br>![](/exercises/ex3/images/011.png)
28.	Close the configuration UI.
29.	Wait until the alert appears again. (Eventually you could also restart the application).
30.	Select the new “High Disk Utilization” alert to open alert details.
31.	Select Operation Flows . Check that the Operation Flow has been triggered automatically this time. 
<br>![](/exercises/ex3/images/006.png)
## Exercise 3.4 Check IEP event log and event actions (optional).
As the operation flow resolves the critical situation automatically you could also deactivate the alert in the configuration.
But you wonder how you can review the event and automatically triggered actions without alert. This is possible in the Event log in the Intelligent Event Processing.
28. Select Intelligent Event Processing from the launchpad.
<br>![](/exercises/ex3/images/013.png)

29. Open the scope selector and select service XP270-XXX. (Replace XXX with your assigned number). Select Apply.
<br>![](/exercises/ex3/images/014.png)
30. Review the information displayed on the  event log overview page. You see how many event situations were created in the selected time frame for the selected service, how many event situations are in status closed and open, how many event actions were triggered and how many event actions failed. The table at the bottom of the screen lists the single event situations. Select the latest event action to open the action log.
<br>![](/exercises/ex3/images/015.png)
31 Review the event action log.
<br>![](/exercises/ex3/images/016.png)

