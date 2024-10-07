# Description

You inform the developer of the `perfumeStore` app of the disk utilization problem. He advises to set couple of possible remediation actions and build automated flows for these such as: 
- clear the diskspace as soon as it has exceeded a certain limit;
- restart the app (in case the issue occurs over again) - **OPTIONAL**

During this exercise you will create a command to clean the disk space using SAP Automation Pilot and register the command as operation flow in SAP Cloud ALM. 

## Define commands for an automated remediations via SAP Automation Plot   

### Command: "Delete App Temp Storage" in SAP Automation Pilot 

1. Access your SAP Automation Pilot via SAP BTP cockpit  .
![](./images/01-accessing-automation-pilot.png)

2.	Once you access the SAP Automation Pilot navigate to “Comands” section search for a command named `HttpRequest`
![](./images/command_search.png)
![](./images/2.1.2-pic-01.png)

   
3.	Access the command and clone by adding it to the `Welcome` catalog as shown on the screenshot and name it “{your session ID}.(user ID).deleteAppTemStorageDemo”, e.g. "XP270.001.deleteAppTemStorageDemo" ,  "XP270.002.deleteAppTemStorageDemo", etc.
![](./images/2.1.2-pic-02.png)
![](./images/2.1.2-pic-03.png)

4.	Add the needed input keys so that the command can be triggered and executed successfully.

**TIP:** **How to work with command's inputs and provide the correct input values following the previous screenshots**. 

**- Working with static inputs**: To provide static inputs for your command (e.g. to provide the value `cf-eu10-004` for the input `region`) fist you need to slide the toggle for the required input (see screenshot below)
![](/exercises/ex2/images/before-toggle_2.png)

Once that is done - the "Default Value Source" should be set to `Static` and you can provide the needed static value within the field `Value`
![](/exercises/ex2/images/after-toggle_2.png)

What you need to specify within the commands input keys are just two inputs:
- `method` to be set to `GET` (as a static imput)
![](./images/2.1.2-pic-06.png)
- `url` - that is `{app_url}/delete-file` resulting in athe  app endpoint which can be called in order to delete the temp storage.
![](./images/2.1.2-pic-05.png)

> [!NOTE]
> App endpoint to be called in order to delete the temp app storage is: `{app_url}/delete-file`

**HINT:** `{app_url}` can be found via SAP BTP Cockpit as explained here: "BTP Cockpit" --> "Spaces" --> click on the desired space (in your use case you should be able to see just one space, so click on the spacenamed "prod") --> clik on the app name (e.g. `perfumeStore`) and you shall see the Applicaiton Overview scree. Check out the "Application Routers" URL - this is your App URL that shall be copied and used. 
![](./images/2.1.2-pic-04.png)

Once you are done with adding the correct values for your input keys you can proceed further to model the command and specify which exact action to be triggered by the command.

5.	Add the needed executors to the command.
To specify the exact action for the command, you need to add a comand executor.

5.1. To do so , navigate down to the command section named "Executors" and click on the "Add" button (see the screenshot below):
![](./images/04-02-automation-pilot.png)


5.2.  Now Click on the button `Here` as per the screenshot below and add the alias `deleteAppTempStorage` (it can be whaever alias which makes sense to you) and from the dropdown "Command" use the autocomplete form and search for this specific command out of the provided commands' catalog: `http-sapcp:HttpRequest:1`
![](./images/04-03-automation-pilot.png)
![](./images/2.1.2-pic-07.png)

**NOTE**: Keep the "Automap parameters" toggle enabled so that your inputs can be mapped to the command automatically. Click on the button `Add` to save your changes.

6.	Now your command should be ready and you can see the following paramters being mapped to the command executors:
![](./images/2.1.2-pic-08.png)

7. Commands outputs values  – it is a good practice to prepare the needed command outputs so that you can check out what was the output after running the command. Please follow the guidance shared below:
- body (string): `$(.deleteAppTempStorage.output.body)`
- headers (object): `$(.deleteAppTempStorage.output.headers)`
- method (string): `$(.deleteAppTempStorage.output.method)`
- size (number): `$(.deleteAppTempStorage.output.size)`
- status (number): `$(.deleteAppTempStorage.output.status)`
- time (number): `$(.deleteAppTempStorage.output.time)`
- url (string): `$(.deleteAppTempStorage.output.url)`

Once you are done with providing the output vlaues you should be able to see this screen:
![](./images/2.1.2-pic-09.png)

Note: Once the command gets triggered , the command output keys will be printed here:
![](./images/2.1.2-pic-10.png)

Now you are ready to trigger the command manually or automatically via SAP Cloud ALM. 



## Exercise - Register command as Operation Flow in SAP Cloud ALM  

The previously defined command "Delete App Temp Storage"needs to be registered in SAP Cloud ALM so that SAP Cloud ALM can trigger it. 

1. Logon to SAP Cloud ALM.

2. Select “Operations Automation”.
![](./images/2.2-pic-01.png)

3. Select “Register Operation Flow”. Select “SAP Automation Pilot”.
![](./images/2.2-pic-02.png)

4. Type  XP270_XXX (replace XXX with your number ) in field endpoint.

5. Select the F4 help in the ID field. Select the command you created earlier (XP270.XXX.deleteAppTemStorageDemo.)

6. Leave input reference empty.

7. Optionally enter a description.

8. Select Use Case “Health Monitoring”.

9. Select Ok.
![](./images/2.2-pic03.png)

10. Now the command should appear in the list of operation flows. 

## Summary

You've now all commands for automated remediations modeled and stored in SAP Automation Pilot and also have integrated your SAP Cloud ALM to SAP Automation Pilot. Now the commands in questions can be triggered automatically or manually via Cloud ALM. 

Continue to - [Exercise 3 - Check alert and resolve problem ](../ex3/README.md)
