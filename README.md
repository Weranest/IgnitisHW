### Created by Eimantas Bernotavicius ###
### Documentation is included in the Documentation folder ###


### What it does ###
The purpose of this package is to be able to parse an excel list called "Grupės.xlsx" and based on the contents of that list return zip files with information about the videos found by the youtube recommendations of the user using it.

### How to operate it ###
1. * Program uses Chrome, Excel, Word and Outlook as part of required operations, as such the machine the program is used on should have all of those programs
2. * Create a "Grupės.xlsx" file that contains one collumn named "Pavadinimas". Insert the search terms needed inside the collumn.
3. * Change the desired settings and variables inside the "Config.xlsx", found inside the Data folder, for the dollowing settings:

 + MasterfilePath - Path to the "Grupės.xlsx" file
 + WorkFolderPath - Path to the work folder used to store files (the program will create a new folder inside the selected path and will not interact with any other file present in the path)
 + EmailTo - Email address that is to be used as the recipient of the zip files at the end of the process
 + MaxVideoLength - Maximum length of videos to be included in the final output. When parsed, videos with higher values than the one here will not be parsed
 + SongsPerBand - Number of songs to be included in each search results final output


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