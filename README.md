# Siemplify Integration - Bitdefender GravityZone
## About
This is an integration for the Siemplify SOAR platform that provides playbook actions for most popular and useful API endpoints provided by Bitdefender for their GravityZone solution.
Official docs will be a huge help in general use of, and developing additional capabilities for this integration. Though I will attempt to document the most important information here, your best reference will be their official documentation which is available in PDF here: [Bitdefender Control Center](https://download.bitdefender.com/business/API/Bitdefender_GravityZone_Cloud_APIGuide_forCustomers_enUS.pdf) - Most of this information is extracted from, or already available in that PDF.
## Playbook Actions
All playbook actions that return data should have a JSON Result Sample included
### Blocklist
#### Add Hashes
Use this method to add one or more file hashes to the blocklist.
#### List Items
This method lists all the hashes that are present in the blocklist
#### Remove Item
This method removes an item from the blocklist, identified by its ID
### Policies
#### List All
This method retrieves the list of available policies.
#### Get Details
This method retrieves all information related to a security policy.
### Quarantine
#### Add File
This method creates a new task to add a file to quarantine.
#### Get Items List
This method retrieves the list of quarantined items available for a company. An item can be a file or an Microsoft Exchange object.
The filter fields Threat Name, File Path, and IP Address work with partial matching.
The filter returns the items which are exact match or start with the specified value.
To use the specified value as a suffix, use the asterisk symbol (*). For example:
If filePath is C:\temp, the API returns all items originating from this folder, including sub-folders.
If filePath is *myfile.exe, then the API returns a list of all myfile.exe files from anywhere on the system.
The Exchange filters require a valid license key for Security for Exchange.
#### Remove Items
This method creates a new task to remove items from quarantine.
#### Restore Exchange Items
This method creates a new task to restore items from the quarantine for Exchange Servers.
#### Restore Items
This method creates a new task to restore items from the quarantine.
### Reports
#### Get Download Links
This method returns an Object with information regarding the report availability for download and the corresponding download links.
The instant report is created one time only and available for download for less than 24 hours.
Scheduled reports are generated periodically and all report instances are saved in the GravityZone database.
#### List All
This method returns the list of scheduled reports, according to the parameters received.
### General
#### Create Scan Task
This method creates a task to isolate the specified endpoint.
#### Create Scan Task by MAC Address
Use this method to generate a scan task for managed endpoints identified by their MAC address.
#### Get Custom Groups List
This method retrieves the list of groups under a specified group.
#### Get Endpoints List
Get list of endpoints
#### Get Hourly Usage for EC2 Instances
This method exposes the hourly usage for each Amazon instance category (micro, medium etc.).
#### Get Managed Endpoint Details
This method returns detailed information, such as: details to identify the endpoint and the security agent, the status of installed protection modules.
#### Get Network Inventory Items
This method returns network inventory items. Note - Some filters require a specific license to be active, otherwise they are ignored, resulting in an inaccurate API response. The field name works with partial matching.
The filter returns the items whose names are exact match or start with the specified value. To use the specified value as a suffix, use the asterisk symbol (*).
#### Get Scan Tasks List
This method returns the list of scan tasks.
#### Isolate Endpoint
This method creates a task to isolate the specified endpoint.
#### Restore Isolated Endpoint
This method creates a task to restore the specified endpoint from isolation.
#### Set Endpoint Label
This method sets a new label to an endpoint.
## Manager
### Reports
Additional reports and their mapped ID's can be added to the top of this file, by appending to the default dict:

    REPORTS = {"Antiphishing Activity" : 1,
	    "Blocked Applications": 2,
	    "Blocked Websites": 3,
	    "Data Protection": 5,
	    "Device Control Activity": 6,
	    "Endpoint Modules Status": 7,
	    "Endpoint Protection Status": 8,
	    "Firewall Activity": 9,
	    "Malware Status": 12,
	    "Monthly License Usage": 13,
	    "Network Status": 14,
	    "On demand scanning": 15,
	    "Policy Compliance": 16,
	    "Security Audit": 17,
	    "Security Server Status": 18,
	    "Top 10 Detected Malware": 19,
	    "Top 10 Infected Endpoints": 21,
	    "Update Status": 22,
	    "Upgrade Status": 23,
	    "AWS Monthly Usage": 24,
	    "Endpoint Encryption Status": 30,
	    "HyperDetect Activity": 31,
	    "Network Patch Status": 32,
	    "Sandbox Analyzer Failed Submissions": 33,
	    "Network Incidents": 34,
	    "Email Security Usage": 29
	}
## Connectors?
Unfortunately, Bitdefender only supports a "push" model of alerting. Where by, you tell their API where it should push the alerts to (SIEM, custom syslog) and it sends them to that destination. Therefore you must either use a SIEM or a custom webserver that's set up to monitor for alerts.
[How to integrate GravityZone Cloud Platform with Splunk](https://www.bitdefender.com/support/how-to-integrate-gravityzone-cloud-platform-with-splunk-2152.html)
[Building an Event Push Service API Connector for CEF standard](https://www.bitdefender.com/support/building-an-event-push-service-api-connector-for-cef-standard-2373.html)
