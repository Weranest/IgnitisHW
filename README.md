### Documentation is included in the Documentation folder ###


### REFrameWork Template ###
**Robotic Enterprise Framework**

* Built on top of *Transactional Business Process* template
* Uses *State Machine* layout for the phases of automation project
* Offers high level logging, exception handling and recovery
* Keeps external settings in *Config.xlsx* file
* Takes screenshots in case of system exceptions


### How It Works ###

1. **INITIALIZE PROCESS**
 + ./Framework/*InitiAllSettings* - Load configuration data from Config.xlsx file and from assets
 + ./Framework/*GetAppCredential* - Retrieve credentials from Orchestrator assets or local Windows Credential Manager
 + ./Framework/*InitiAllApplications* - Open and login to applications used throughout the process
 + ./Framework/*SetupWorkFolder* - Sets up an isolated work folder to handle the files ised in the process


2. **GET TRANSACTION DATA**
 + ./Framework/*GetTransactionData* - Fetches transactions from the queue which is loaded from the selected excel file in the configs

3. **PROCESS TRANSACTION**
 + *Process* - Process trasaction and invoke other workflows related to the process being automated 
 + ./Framework/*WordCreator* - Downloads the images from the input bands and builds both the word documents and the zip files
 + ./Framework/*BrowserParser* - Uses youtube to get the required information about videos that were displayed by the selected search terms

4. **END PROCESS**
 + ./Framework/*CloseAllApplications* - Logs out and closes applications used throughout the process
 + ./Framework/*SendEmail* - Sends the email with the requested zip folders to the specified email adress using Outlook


### Known issues ###

* Project currently only supports Chrome for browsing youtube
* Issues with possible hangups when parsing image urls 