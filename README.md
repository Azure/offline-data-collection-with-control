# offline-data-collection
A solution for creating centralized offline data collection with control

This is high level end to end single file upload flow with control from SharePoint to azure datalake.
A Business user can upload file in SharePoint online as well as Microsoft Team. Each business unit has separate folder. Level of access permission for each business user/unit can be managed at folder level.

Azure logic App product builds automated scalable workflows, business processes, and enterprise orchestrations to integrate your apps and data across cloud services and on-premises systems. Azure Logic apps has hundreds of connectors. Azure logic app can be connected to SharePoint for given Site address and folder path using SharePoint Connector. Workflow is can be triggered on scheduled time as well as event basis. Trigger can be like When new file is created at given Site address and folder path. In automated scalable workflow, Various SharePoint action can be invoked e.g. Get file Metadata and Get File Properties to collect info as well as set action on SharePoint side for particular file and folder level. Logic app can be monitored and alert to operation team regarding any failure after initial configuration.

Office365 outlook connector of Logic app is used here to notify the business user in case of file upload rejection. This can be used to take approval of process by sending email and approver can simply click on Approve or Reject button.

At least following file metadata can be captured for Metadata catalogue and reporting.



