﻿﻿﻿﻿﻿﻿# Octopus Deployment Steps Configuration and Variables

## Process Details:

![](/ODSCVImages/image001.png)

**Step 1: SQL Script Deployment** - PowerShell script to deploy SQL scripts in the TeamCity package located in the coordinating source control folder that shares the github branch name.

Ex: DTV-Release-2017.14 branch 
> /SourceCode/DatabaseScripts/DTV-Release-2017.14/IBIS
> /SourceCode/DatabaseScripts/DTV-Release-2017.14/IBISLogs
> /SourceCode/DatabaseScripts/DTV-Release-2017.14/OrderStatusArchive

Currently the script folders are defined with the Database names that the SQL script should be executed against (IBIS, IBISLogs, and OrderStatusArchive). The database names are aliased and defined in further detail in the Octopus Variables section below.

Scripts should be prefixed with a three digit number to indicate sequence of execution and contain the story number that they pertain to for information purposes.
> 001-DTV-9999_Story_Desc
> 002-DTV-7878_Story_Desc
> etc...

The PowerShell script that is executed in this step resides in source in the following location:
> /Deploy/SQLAutomation.ps1

**Step 2: Deploy Package to Server** - Standard TeamCity package pull and deployment to Octopus Tentacles filtered on DTVWeb role.

**Step 3/4: Notify (Success and Failure)** - Imbedded PowerShell script in the Octopus step for building details of the deployment and sending them to Slack for notification of the team. Step 3 executes when all previous steps are successful and Step 4 executes if any prior steps have failed. These scripts are manually copied into the step on the Octopus server, however, the PowerShell scripts in their current state should always be updated in source as well. They are located in the following source location:

>/Deployment/Powershell Scripts/OctopusSlackNotifySuccess.ps1
>/Deployment/Powershell Scripts/OctopusSlackNotifyFailure.ps1

## Variable Definitions
##### Screenshot of Variable List:

![](/ODSCVImages/image003.png)

##### Definitions:

|Variable Name|Steps|Definition|
|--------------------|:-------:|-------------|
|BranchNamePrefixMatch|1|Used to build the path for the SQL scripts to be executed. Dynamic to be able to adjust for other project names outside the main "DTV-Release-XXXX.XX" model.|
|GitHubRepo|3,4|Bridgevine Organization repository name that details will need to be acquired from.|
|GitHubToken|3,4|Github generated Person Access Token for the same user defined in the TeamCity user variable.|
|IBISDBName|1|Actual SQL Server database name that corresponds with the DTVIBIS database functionality.|
|IBISInstanceName|1|Actual SQL Server instance name that corresponds with the DTVIBIS database functionality.|
|IBISLogsDBName|1|Actual SQL Server database name that corresponds with the DTVIBISLogs database functionality.|
|IBISLogsInstanceName|1|Actual SQL Server instance name that corresponds with the DTVIBISLogs database functionality.|
|OrderStatusArchiveDBName|1|Actual SQL Server database name that corresponds with the OrderStatusArchive database functionality.|
|OrderStatusArchiveInstanceName|1|Actual SQL Server instance name that corresponds with the OrderStatusArchive database functionality.|
|OctopusDeployPackageFolder|2|Tentacle folder deployment location for the code deployment process.|
|SlackHookFooterIcon|3,4|Used to add TeamCity graphic to final signature of the Slack notifications.|
|SlackHookUrl|3,4| Defines which Slack channel to send the notification. |
|SQLPassword|1| SQL Server password to be used in SQL Authentication for running the SQL scripts.|
|SQLUserName|1| SQL Server user name to be used in SQL Authentication for running the SQL scripts.|
|TeamCityProjectId|1,3,4| Project ID as defined inside of TeamCity on the General Settings tab of Project Settings.|
|TeamCityPwd|1,3,4| Password to authenticate against TeamCity API requests. This is not domain account integrated.|
|TeamCityUrl|1,3,4| Base URL of the TeamCity server to execute constructed API calls.|
|TeamCityUser|1,3,4| User name to authenticate against TeamCity API requests. This is not domain account integrated.|

**Please note the duplication in the variables are given a specific scope in the final column. This allows for us to use specific locations and notification endpoints based on the environment that we are deploying too.**

