### [OPTINAL] 2.1.2 - Command: "Restart App" in SAP Automation Pilot 

**IMPORTANT:** This command is an optional one. It can be triggered manually via CALM only in case the command for temp app storage deletion fails. 

1. Access your SAP Automation Pilot via SAP BTP cockpit  .
![](/exercises/ex2/images/01-accessing-automation-pilot.png)
2.	Once you access the SAP Automation Pilot navigate to “Comands” section and look for a command named “RestartCfApp”
![](./images/02-automation-pilot.png)
   
3.	Access the command and clone by adding it to the respective catalog as shown on the screenshot and name it “{your session ID}.(user ID).RestartCfAppDemo”, e.g. "XP270.001.RestartCfAppDemo" ,  "XP270.002.RestartCfAppDemo", etc.
![](./images/03-automation-pilot.png)
![](./images/04-automation-pilot.png)
  	
4.	Explore the setup of your BTP Technical User that is already made for you in SAP Automation Pilot. To do so - click on the “Inputs” section within the leftsidebar, then look for the inputs named `btpTechnicalUser` 
![](./images/05-03-automation-pilot.png)

> [!NOTE]
> Do not modify the inputs for the Technical user. Password for the BTP Technical user is not visible for you as it was added in advance as a senstive string. 

5.	Now you are good to go and navigate back to the command you have created so that you can add all the needed input keys so that the command can be triggered and executed successfully.
![](./images/input-keys-1.png)
![](./images/input-keys-2.png)

**NOTE:** How to work with command's inputs and provide the correct input values following the previous screenshots. 

- for identiryProvider you need to add `sap.ids` which is the  IDS for the technical user already set for you.

- to add the needed inputs for your BTP Technical user you need to follow these steps for both "user" and "password" (as the steps are identical):
![](./images/inputKeys_2.1.png)
![](./images/inputKeys_2.2.png)
![](./images/inputKeys_2.3.png)
![](./images/inputKeys_2.4.png)

- to find out Org Name ID for your CF environment: navigate to your BTP Subaccount overview and take it from there (see the screenshot below): 
![](./images/inputKeys_2.8.png)

- to find out the Space ID and App ID you can use this hint:
![](./images/inputKeys_2.5.png)

Once you are done with adding the correct values for your input keys you can proceed further. 

7.	Add the needed execution as shown below
![](./images/04-02-automation-pilot.png)
![](./images/04-03-automation-pilot.png)
![](./images/04-04-automation-pilot.png)

9.	Map the input keys to the execution you have created in the previous step:
![](./images/05-automation-pilot.png)

10.	Commands outputs values  – it is a good practice to prepare the needed command outputs so that you can check out what was the output after rinning the command. Please follow the guidance shared below: 
![](./images/06-automation-pilot.png)

12.	Command output keys will be printed here:
![](./images/2.1.2-pic-10.png)

Now you are ready to trigger the command manually or automatically via SAP Cloud ALM. 
