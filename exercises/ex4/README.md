### [OPTINAL] 2.1.2 - Command: "Restart App" in SAP Automation Pilot 

**IMPORTANT:** This command is an optional one. It can be triggered manually via CALM only in case the command for temp app storage deletion fails. 

1. Access your SAP Automation Pilot via SAP BTP cockpit  .
![](/exercises/ex2/images/01-accessing-automation-pilot.png)
2.	Once you access the SAP Automation Pilot navigate to `Comands` section and look for a command named `RestartCfApp`
![](./images/02-automation-pilot.png)
   
3.	Access the command and clone it by adding it to the respective catalog `Welcome` as shown on the screenshot and name it as per this guidance `{your session ID}.(user ID).RestartCfAppDemo`, e.g. `XP270.001.RestartCfAppDemo" ,  "XP270.002.RestartCfAppDemo`, etc.
![](/exercises/ex2/images/03-automation-pilot.png)
![](/exercises/ex2/images/04-automation-pilot.png)
  	
4.	Explore the setup of your BTP Technical User that is already made for you in SAP Automation Pilot. To do so - click on the “Inputs” section within the leftsidebar, then look for the inputs named `btpTechnicalUser` 
![](/exercises/ex2/images/05-03-automation-pilot.png)

> [!NOTE]
> Do not modify the inputs for the Technical user. Password for the BTP Technical user is not visible for you as it was added in advance as a senstive string. 

5.	Now you are good to go and navigate back to the command you have created so that you can add all the needed input keys so that the command can be triggered and executed successfully. To provide the needed command input keys please follow the guidance below and review the screenshots as well:
   - region: `cf-eu10-004`
   - identityProvider: keep the default value - `sap.ids`
   - resourceGroup: your unique `Application ID` (see the screenshots below on how to find it) 
   - resourceName: your unique `Space ID `associated to your CF environment (see the screenshots below on how to find it) 
   - subAccount: your unique `Org Name ID` associated to your CF environment (see the screenshots below on how to find it) 
   - password: `btpTechnicalUser` added as a default value from type string to btpTechnicalUse pointing to the `password` input (see below)
   - user: `btpTechnicalUser` added as a default value from type string to btpTechnicalUse pointing to the `user` input
   - useAdditionalInstance: keep the default value `false`
   - rollingRestart: keep the default value `false`

This is an example of the inputs to be filled in: 
![](/exercises/ex2/images/input-keys-1.png)
![](/exercises/ex2/images/input-keys-2.png)

**TIP:** **How to work with command's inputs and provide the correct input values following the previous screenshots**. 

**- Working with static inputs**: To provide static inputs for your command (e.g. to provide the value `cf-eu10-004` for the input `region`) fist you need to slide the toggle for the required input (see screenshot below)
![](/exercises/ex2/images/before-toggle.png)

Once that is done - the "Default Value Source" should be set to `Static` and you can provide the needed static value within the field `Value`
![](/exercises/ex2/images/after-toggle.png)

- **BTP Technical user:** to add the needed inputs for your BTP Technical user you need to follow these steps for both "user" and "password" (as the steps are identical):
![](/exercises/ex2/images/inputKeys_2.1.png)
![](/exercises/ex2/images/inputKeys_2.2.png)
![](/exercises/ex2/images/inputKeys_2.3.png)
![](/exercises/ex2/images/inputKeys_2.4.png)

**- Org Name ID:** to find out Org Name ID for your CF environment: navigate to your BTP Subaccount overview (in the BTP Cockpit) and take it from there (see the screenshot below): 
![](/exercises/ex2/images/inputKeys_2.8.png)

**- Space ID**:  to find out the Space ID and App ID you can use this hint:
![](/exercises/ex2/images/inputKeys_2.5.png)

Once you are done with adding the correct values for your input keys you can proceed further to model the command and specify which exact action to be triggered by the command.

7.	To specify the exact action for the command, you need to add a comand executor.
7.1. To do so , navigate down to the command section named "Executors" and click on the "Add" button (see the screenshot below): 
![](/exercises/ex2/images/04-02-automation-pilot.png)

7.2. Now Click on the button `Here` as per the screenshot below and add the alias `restartApp` (it can be whaever alias which makes sense to you) and from the dropdown "Command" use the autocomplete form and search for this specific command out of the provided commands' catalog: `applm-sapcp:RestartCfApp:1`
![](/exercises/ex2/images/04-03-automation-pilot.png)
![](/exercises/ex2/images/04-04-automation-pilot.png)

NOTE: Keep the "Automap parameters" toggle enabled so that your inputs can be mapped to the command automatically.  

8.	Now your command should be ready and you can see the following paramters being mapped to the command executors:
![](/exercises/ex2/images/05-automation-pilot.png)

10.	Commands outputs values  – it is a good practice to prepare the needed command outputs so that you can check out what was the output after rinning the command. By default these are set to "none" but you can follow the guidance and create few:
- previousDesiredState (string): `$(.restartApp.output.previousDesiredState)`
- previousResourceInstancesState (array): `$(.restartApp.output.previousResourceInstancesState)`
- previousResourceInstancesStates (array): `$(.restartApp.output.previousResourceInstancesStates)`
- resourceInstancesStates (array): `$(.restartApp.output.resourceInstancesStates)`
- summary (string): `$(.restartApp.output.summary)`

Once you are done with providing the output vlaues you should be able to see this screen:     
![](/exercises/ex2/images/06-automation-pilot.png)

Note: Once the command gets triggered , the command output keys will be printed here:
![](/exercises/ex2/images/2.1.2-pic-10.png)

Now you are ready to trigger the command manually or automatically via SAP Cloud ALM. 
