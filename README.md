# High level architecture for single File upload process
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

![image](https://github.com/arvind-dhariwal/offline-data-collection/media/arch.png)

# File upload flow  using Logic App

![image](https://github.com/arvind-dhariwal/offline-data-collection/media/logicAppFlow.png)

# Sample Email approval request
Body, Subject in email can be customized.
![image](https://github.com/arvind-dhariwal/offline-data-collection/media/SampleApprovalEmail.png)

# Sample Success Notification email to business user.
![image](https://github.com/arvind-dhariwal/offline-data-collection/media/NotificationEmailToBusinessUser.png)
