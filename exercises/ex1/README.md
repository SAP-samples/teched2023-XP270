# Exercise 1 - Configure Monitoring and Alerting in SAP Cloud ALM

In this exercise you will configure and use health monitoring for the perfumestore app.

## Exercise 1.1 Login to SAP Cloud ALM
| Application | User ID | Password | URL |
|---|---|---|---|
| SAP Cloud ALM URL | XP270-**XXX**@education.cloud.sap | Acce$$teched23 | [SAP Cloud ALM](https://ad263-ptnlz9xc.eu10.alm.cloud.sap/launchpad) |

Please replace the XXX in the user name with your assigned number (e.g. XP270-001@education.cloud.sap).
1. Select the SAP  Cloud ALM URL
2. Select tdct3ched1.accounts.ondemand.com
<br>![](/exercises/ex1/images/001.png)
3. Enter user name and password and flag “Keep me signed in”. Select Continue.
<br>![](/exercises/ex1/images/002.png)
## Exercise 1.2 Configure Health Monitoring
4.	Select Health Monitoring.
<br>![](/exercises/ex1/images/003.png)
5.	Select the scope selector. 
<br>![](/exercises/ex1/images/004.png)
6. Select Toggle Filter Bar.
7. Select Service Status All. Select Go.
<br>![](/exercises/ex1/images/01a.png)
8.	Search for cloud service XP270-XXX (replace XXX with your number example: XP270-001) . Select the cloud service. Select Apply.
<br>![](/exercises/ex1/images/005.png) 
Explanation: 
Cloud service “XP270-XXX” of type “SAP BTP, Cloud Foundry” is the representation of the SAP BTP subaccount XP270-XXX in SAP Cloud ALM. The steps above restrict the view in health monitoring to the subaccount assigned to you.
9.	Select Configuration.
<br>![](/exercises/ex1/images/04c.png) 	
11.	Check that data collection is already switched on. (Please do not change anything here).
<br>![](/exercises/ex1/images/06a.png)
12.	Click on the service name to see the details of the configuration.
<br>![](/exercises/ex1/images/06c.png)
13.	The Metrics section shows available metrics for custom applications deployed in a SAP BTP Cloud Foundry space. By default all metrics have no threshold.
Select metric type “Disk Utilization”
<br>![](/exercises/ex1/images/010.png)
14.	Read through the description to familiarize. 
15.	Select threshold type “Numeric”.
16.	Select Field “Usage”.
17.	Select Condition “Above”.
18.	Select threshold 70% for warning and 90% for critical. Select save.
<br>![](/exercises/ex1/images/011.png)
19.	Optional: Define thresholds for other metrics.

## Exercise 1.3 Configure Alerting
20.	Select Events tab.
21.	Select the event type “High Disk Utilization”. 
<br>![](/exercises/ex1/images/012.png)
22.	Switch on event action “Create Alert”. Select Save. 
<br>![](/exercises/ex1/images/013.png)
23.	Select Close on the ‘Configuration for Services’.

## Exercise 1.3 Configure email notification (optional)
You can also configure email notifications. This requires that you enter yourself as recipient in notification management. As you are working in a shared SAP Cloud ALM, other participants will be able to see your e mail address. If you are not ok with this you can skip this part of the exercise.

24.	Select Notification Management from the SAP Cloud ALM Launchpad.
<br>![](/exercises/ex1/images/014.png)
25.	Select Add.
26.	Enter your email address ( which you can access during the course of this exercise)and select save.
<br>![](/exercises/ex1/images/015.png)
 Your e mail address will appear in Notification management with status “Pending”.
27.	Open your e mail inbox. You should have received a mail “Welcome to SAP Cloud ALM”. Open the mail.
28.	Select the link in the mail to consent that you want to receive notifications from SAP Cloud ALM. After clicking on the link, a web page opens showing “You are subscribed to SAP Cloud ALM Notifications”. 
29.	 Close and re-open the Notification Management browser window. Your e mail address should change to  status “Verified”.
<br>![](/exercises/ex1/images/016.png)
30.	Navigate to Health Monitoring app and go to Event Configuration screen for service XP270-XXX.
<br>![](/exercises/ex1/images/016d.png)
<br>![](/exercises/ex1/images/016e.png)
31.	Switch on event action “Send Email To”.
32.	Select Add button. Select your email address. Select Save.
<br>![](/exercises/ex1/images/017.png)
33.	Select Close on the ‘Configuration for Services’.
34.	Close the configuration pane if it is still open.

## Exercise 1.4 Use health monitoring to check the health of your custom application

35.	Close the configuration pane if it is still open.
 <br>![](/exercises/ex1/images/018.png)
36.	Select Monitoring.
37.	Select service “XP270-XXX”.
Click on the row to check the metric overview.  
<br>![](/exercises/ex1/images/019.png)
Depending on how much time passed since perfumestore app start, the metric Disk
 utilization might already have a yellow or red rating. 
<br>![](/exercises/ex1/images/020.png)
38.	Select metric “Disk Utilization”
39.	Click on “History”.
<br>![](/exercises/ex1/images/021.png)
40.	Select “Time Frame” and then choose ‘Last 1 hour’ and Resolution as ‘1 minute.’ Select Apply.
<br>![](/exercises/ex1/images/022.png)
 You will notice that the Disk utilization of the perfumestore app increases continuously towards the limit of 1 GB. 
<br>![](/exercises/ex1/images/023.png)
41.	Optionally: Check other metrics
## Summary

You've now configured monitoring of your custom app and detected the first problem that it consumes excessively disk space . As a next step you will configure an automated action to resolve this problem in [Exercise 2 - Build Clean Disk Command](../ex2/README.md)
