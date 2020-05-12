# Problem statements -
1. There are data silos with different business units.
2. There is no control on data provided by business monthly / quartely and business user is allowed to modify data after uploading file.
3. Data are collected manaually and uploaded to datalake, no automation on communication and approval side.
4. As head of business user not able to view what all monthly and quarterly data file is ready and processed so that i can expect those data in reporting dashboard.
5. Sometime ETL is failed while processing data file provided by business user because they have provided same data in different schema(adding one more column) or duplicate file.

# Requirement
1. **As** a buseinss user, **i want** to combine my monthly and/or quartely data available on my laptop with existing dataware house tables **so that** i can report and perform analysis with bigger scope. My data sits in silo.
2. **As** a data architect, **i want** to facilate my business user to upload file with set of guidelines(like they upload data in predefined file tempalte ,  files goes for approval over email and file is uploaded on given frequency) and automated flow **so that** collect and store data in central location datalake and datawarehouse company wide , make it available to everyone and file upload should be rejected in case of not following guidelines.
3. **As** a head of business,**i want** file upload process reporting **so that** i can see what all monthly and quaretly files has been prepared by my department and shared with Enterprise data team to process it for reporting, also want to see the link of file in metadata reproting in case i wwant to open the file.


# High level architecture for single file upload process
A solution for creating centralized offline data collection with control

This is high level end to end single file upload flow with control from SharePoint to azure datalake.
A Business user can upload file in [SharePoint online](https://docs.microsoft.com/en-us/sharepoint/introduction "SharePoint online") as well as [Microsoft Team](https://docs.microsoft.com/en-us/microsoftteams/teams-overview "Microsoft Team"). Each business unit has separate folder. Level of access permission for each business user/unit can be managed at folder level.

![image](https://github.com/arvind-dhariwal/offline-data-collection/blob/master/media/SharePointScreenShot.png)

[Azure logic App](https://docs.microsoft.com/en-us/azure/logic-apps/ "Azure logic App") product builds automated scalable workflows, business processes, and enterprise orchestrations to integrate your apps and data across cloud services and on-premises systems. Azure Logic apps has hundreds of connectors. Azure logic app can be connected to SharePoint for given Site address and folder path using [SharePoint Connector](https://docs.microsoft.com/en-us/connectors/sharepoint/ "SharePoint Connector"). Workflow is can be triggered on scheduled time as well as event basis. Trigger can be like When new file is created at given Site address and folder path. In automated scalable workflow, Various SharePoint action can be invoked e.g. Get file Metadata and Get File Properties to collect info as well as set action on SharePoint side for particular file and folder level. Logic app can be [monitored](https://docs.microsoft.com/en-us/azure/logic-apps/monitor-logic-apps "monitored") and alert to operation team regarding any failure after initial configuration.

[Office365 outlook connector](https://docs.microsoft.com/en-us/azure/connectors/connectors-create-api-office365-outlook "Office365 outlook connector") of Logic app is used here to notify the business user in case of file upload rejection. This can be used to take approval of process by sending email and approver can simply click on Approve or Reject button.

At least following file metadata can be captured for Metadata catalogue and reporting.
- file_name
- file_size
- full_path
- file_link
- version
- media_type
- created_at
- modified_at
- created_by
- modified_by
- comments

Following info can be parameterized for each file upload flow-
1. SharePoint Site Address
2. Folder Path
3. List of Approver’s email Id.
4. Template of File for schema validation
5. IsEmailApprovalRequried – Yes/No
6. Expected File upload time

![image](https://github.com/arvind-dhariwal/offline-data-collection/blob/master/media/arch.png)

# File upload flow  using logic App

![image](https://github.com/arvind-dhariwal/offline-data-collection/blob/master/media/logicAppFlow.png)

# Sample email approval request
Body, Subject in email can be customized.
![image](https://github.com/arvind-dhariwal/offline-data-collection/blob/master/media/SampleApprovalEmail.png)

# Sample success notification email to business user.
![image](https://github.com/arvind-dhariwal/offline-data-collection/blob/master/media/NotificationEmailToBusinessUser.png)
