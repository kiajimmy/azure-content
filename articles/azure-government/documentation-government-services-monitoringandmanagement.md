<properties
	pageTitle="Azure Government documentation | Microsoft Azure"
	description="This provides a comparison of features and guidance on developing applications for Azure Government."
	services="Azure-Government"
	cloud="gov"
	documentationCenter=""
	authors="ryansoc"
	manager="zakramer"
	editor=""/>

<tags
	ms.service="multiple"
	ms.devlang="na"
	ms.topic="article"
	ms.tgt_pltfrm="na"
	ms.workload="azure-government"
	ms.date="10/14/2016"
	ms.author="ryansoc"/>


#  Azure Government monitoring and management

This article outlines the monitoring and management services variations and considerations that must be to be taken into account in the Azure Government environment.

## Log Analytics

Log Analytics is generally available in Azure Government.

### Variations

The following Log Analytics features and solutions are not currently available in Azure Government. This list is updated when the status of features/solutions changes.

+ Solutions that are in preview in Microsoft Azure, including:
  - Network Monitoring solution
  - Azure Networking Analytics solution
  - Office 365 solution
  - Windows 10 Upgrade Analytics solution
  - Application Dependency Monitoring solution
  - Application Insights solution
  - Azure Activity Logs solution
  - Azure Automation Analytics solution
  - Key Vault Analytics solution
+ Solutions and features that require Azure Automation, including:
  - Update management
  - Change management
  - Alerts that trigger an Azure Automation runbook
+ Solutions and features that require updates to on-premises software, including:
  - Integration with System Center Operations Manager 2016
  - Computers groups from System Center Configuration Manager
  - Surface Hub solution
+ Features that are in preview in public Azure, including:
  - Export of data to Power BI
+ Azure portal integration
  - Azure storage accounts to monitor</br>
	  To select Azure storage accounts to monitor, you must use PowerShell or Resource Manager templates.
  - Virtual machines to enable the Log Analytics Agent</br>To select virtual machines to enable the Log Analytics Agent, you must use PowerShell or Resource Manager templates.
  - Azure metrics and Azure diagnostics
+ Operations Management Suite mobile applications
+ Operations Management Suite Linux Agent virtual machine extension

The following Log Analytics features behave differently in Azure Government:

+ The Windows Agent must be downloaded from the [Log Analytics portal](https://oms.microsoft.us) for Azure Government.
+ To upload data by using the Data Collector API, you must the use the Azure Government URL, https://*workspaceId*.ods.opinsights.azure.us, where *workspaceId* is the workspace ID from the Operations Management Suite portal.
+ To connect your System Center Operations Manager management server to Log Analytics, you need to download and import updated management packs.
  1. Download and save the [updated management packs](http://go.microsoft.com/fwlink/?LinkId=828749).
  2. Unzip the file that you downloaded.
  3. Import the management packs into Operations Manager. For information about how to import a management pack from a disk, see [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx) on the Microsoft TechNet website.
  4. To connect Operations Manager to Log Analytics, follow the steps in [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).


## Frequently asked questions

+ Can I migrate data from Log Analytics in Microsoft Azure to Azure Government?
  - No. It is not possible to move data or your workspace from Microsoft Azure to Azure Government.
+ Can I switch between Microsoft Azure and Azure Government workspaces from the Operations Management Suite Log Analytics portal?
  - No. The portals for Microsoft Azure and Azure Government are separate and do not share information.

For more information, see [Log Analytics public documentation](../log-analytics/log-analytics-overview.md).

## Next steps

For supplemental information and updates, subscribe to the
<a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a>
