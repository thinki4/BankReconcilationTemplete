[Nuummite Starter Templete Documentation](https://source.cloud.google.com/rpapoc-260115/Nuummite_starter_templete?authuser=0)

### Nuummite Starter Templete ###

* Built as a started templete for *all type of business requirement*
* Keeps external settings,orchestrator assets and credential in *Config.xlsx*.
* Use config dictionary to access all the configuration from config file
* Pulls credentials from Orchestrator assets and *Windows Credential Manager*
* Use credentials dictioanry to access all the credential username and passwords
* Uses *State Machine* layout for the phases of automation project
* In the case of a system exception, the process can be automatically retried.
* Once retry exceed max retry count then the process will move to exception state
* Offers high level logging, exception handling and recovery
* Takes screenshots and send email to SME in case of system exceptions


### How It Works ###

1. **INITIALIZE PROCESS**
 + ./Initialization/InitConfig.xaml - Load configuration data, assets and credentials from Config.xlsx file ,Retrieve credentials from Orchestrator or Windows Credential Manager
 + ./Initialization/InitHistory.xaml - Add process id, start time, end time, temporary folder and status to history log excel sheet
 + ./Initialization/InitTempFolder.xaml - Create sub folder for every run inside the temporary folder path 
 + ./Initialization/GetInputData.xaml - Get input data from argument or orchestrator,add input data to config
 + ./Initialization/FixInitialization.xaml - Steps to fix any possible exception that may occure in production
 + ./Initialization/KillAllProcesses.xaml - Kill processes that used in the project

2. **Exception**
 + ./Exception/TakeScreenshot.xaml - Take screen shot and save it to temporary folder
 + ./Exception/SendEmailToSME.xaml - Send email to SME with exception details

3. **Process**
 + ./Process/Process.xaml - Process workflows related to the process being automated.
 + ./Process/InitProcess.xaml - Include workflows to initialize applications ,create folders that will be used in the state.
 + ./Process/FixException.xaml - Steps to fix any possible exception that may occure in production
+ ./Process/CloseApplication.xaml - Logs out and closes applications used in the state.

4. **Success**
 + ./End Process/CloseAllApplications.xaml - Logs out and closes applications used throughout the process
 + ./End Process/UpdateHistory.xaml - Select the row contains the start log,updated the end time and status

### For New Project ###

1. Place config file in shared folder.
2. Add config file path in orchestrator asset.
3. Check the Config.xlsx file and add/customize any required fields and values.
4. Place history excel file in shared folder.
5. Add history file path in orchestrator asset.
6. Split the process into multiple state.
7. Create folder for each state and include three workflows, process.xaml,fix.xaml,init.xaml.
8. Follow the *Process* state life cycle to extend the your process to multible states.
