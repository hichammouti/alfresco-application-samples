The project contains a couple of Alfresco ECM solution showcases and code samples.
Please follow the links to the project specific documentation:

### Purchase Request ###
The PurchaseRequestSamples project demonstrates how to easily map a typical business procedure like the creation of a simplified procurement approval process to Alfresco Share.

### Password Extensions ###
The PasswordExtensions project demonstrates how to enforce custom password hardening policies on a repository level.
The PasswordExtensions module hooks into the AuthenticationService by using AOP and enforces a number of policy constraints to prevent the creation of unsecure passwords and to prevents that the same password is used multiple times in a row.

### Download As Zip ###
The DownloadAsZip project provides additional  bulk download capabilities for Alfresco Share's web UI. The DownloadAsZip project contains a toolbar action that triggers the download of multiple files within a folder at once, by compressing them into a zip and streaming down the zip file.

### Bulk Node Creator ###
The BulkNodeCreator should ease the creation of large demo and test repositories.
It creates a defined number of nodes below an Alfresco folder. The nodes are either pushed all into a single folder or distributed among a folder dynamically created folder hierarchy.
The tool is intended to be used for the preparation of load test repos and to ease the testing of customizations on a bigger repository.
It created 500000 nodes in less then 1 hour on a i7 test laptop.