<properties
   pageTitle="Learn about SQL Database backups | Microsoft Azure" 
   description="Learn about SQL Database automatic database backups that enable you to restore an Azure SQL Database to a previous point in time or copy a database to a new database in an geographic region up to 35 days."
   services="sql-database"
   documentationCenter=""
   authors="CarlRabeler"
   manager="jhubbard"
   editor="monicar"/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="10/18/2016"
   ms.author="carlrab;barbkess"/>

<!------------------
This topic is annotated with guidelines for FEATURE TOPICS.

TEMPLATE GUIDELINES for feature topics

The Feature Topic is a one-pager (ok, sometimes longer) that explains a capability of the product or service. It explains what the capability is and characteristics of the capability.  

It is a "learning" topic, not an action topic.

DO explain this:
	• Definition of the feature terminology.  i.e., What is a database backup?
	• Characteristics and capabilities of the feature. (How the feature works)
	• Common uses with links to overview topics that recommend when to use the feature.
	• Reference specifications (Limitations and Restrictions, Permissions, General Remarks, etc.)
	• Next Steps with links to related overviews, features, and tasks.

DON'T explain this:
	• How to steps for using the feature (Tasks)
	• How to solve business problems that incorporate the feature (Overviews)
------------------->

<!------------------
GUIDELINES for the H1 title
	
	The H1 title should answer the question "What is in this topic?" Write the title in conversational language and use search key words as much as possible. Since this is a learning topic, make sure the title indicates that and doesn't mislead people to think this will tell them how to do tasks.  
	
	To help people understand this is a learning topic and not an action topic, start the title with "Learn about ... "
-------------------->

# Learn about SQL Database backups

<!------------------
	GUIDELINES for introduction
	
	The introduction 2-3 sentences.  It is optimized for search and sets proper expectations about what to expect in the article. It should contain the top key words that you are using throughout the article.The introduction should be brief and to the point of what the feature is, what it is used for, and what's in the article. 

	In this example:
	
Sentence #1 explains the purpose of having backups
	Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion. 

Sentence #2 summarizes how backups work in SQL Database
	SQL Database automatically creates a local database backup every five minutes and uses Azure read-access geo-redundant storage (RA-GRS) to provide geo-redundancy. 

Sentence #3 gives links to articles that explain how to use backups. This raises CSAT if the customer was looking for a how to instead of a learn article.

	Use local database backups to restore a database to a point in time on the same server. Use geo-redundant backups to restore the database to a different geographical region. 
-------------------->


Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion. SQL Database automatically creates a local database backup every five minutes and uses Azure read-access geo-redundant storage (RA-GRS) to provide geo-redundancy. Use local database backups to [restore a database to a point in time](sql-database-point-in-time-restore-portal.md) on the same server. Use geo-redundant backups to [restore the database to a different geographical region](sql-database-geo-restore-portal.md).  


<!-- This image needs work, so not putting it in right now.

This diagram shows SQL Database running in the US East region. It creates a database backup every five minutes, which it stores locally to Azure Read Access Geo-redundant Storage (RA-GRS). Azure uses geo-replication to copy the database backups to a paired data center in the US West region.

![geo-restore](./media/sql-database-geo-restore/geo-restore-1.png)

-->

<!---------------
GUIDELINES for the first ## H2.

	The first ## describes what the feature encompasses and how it is used. It points to related task articles.
	
	For consistency, being the heading with "What is ... "
----------------->

## What is a SQL Database backup?  

<!-- 
	Explains what a SQL Database backup is and answers an important question that people want to know.
-->

A SQL Database backup includes both local database backups and geo-redundant backups. These backups are created automatically and at no additional charge. You don't need to do anything to make them happen.

<!----------------- 
	Explains first component of the backup feature
------------------>

For local backups, SQL Database uses SQL Server technology to create [full](https://msdn.microsoft.com/library/ms186289.aspx), [differential](https://msdn.microsoft.com/library/ms175526.aspx ), and [transaction log](https://msdn.microsoft.com/library/ms191429.aspx) backups. The transaction log backups happen every five minutes, which allows you to do a point-in-time restore to the same server that hosts the database. When you restore a database, the service figures out which full, differential, and transaction log backups need to be restored.

<!--------------- 
	Explicit list of what to do with a local backup. "Use a ..." helps people to scan the topic and find the uses quickly.
---------------->

Use a local database backup to:

- Restore a database to a point-in-time within the retention period. With a database backup you can restore a database to a point-in-time, restore a deleted database to the time it was deleted, or restore a database to another geographical region. To perform a restore, see [restore a database from a database backup](sql-database-recovery-using-backups.md).

- Copy a database to a SQL server in the same or different region. The copy is transactionally consistent with the current SQL Database. To perform a copy, see [database copy](sql-database-copy.md).

- Archive a database backup beyond the backup retention period. To perform an archive, [export a SQL database to a BACPAC](sql-database-export.md) file. You can then archive the BACPAC to long-term storage and store it beyond your retention period. Or, use the BACPAC to transfer a copy of your database to SQL Server, either on-premises or in an Azure virtual machine (VM).

<!----------------- 
	Explains first component of the backup feature
------------------>

For geo-redundant backups, SQL Database uses [Azure Storage replication](../storage/storage-redundancy.md). SQL Database stores local database backup files in a [Read-Access Geo-Redundant Storage (RA-GRS)](../storage/storage-redundancy.md#read-access-geo-redundant-storage) account. Azure replicates the backup files to a [paired data center](../best-practices-availability-paired-regions.md). 

<!--------------- 
	Explicit list of what to do with a geo-redundant backup. "Use a ..." helps people to scan the topic and find the uses quickly.
---------------->

Use a geo-redundant backup to:

- Restore a database to a different geographical region in case you cannot access the database backup from your primary database region. 

>[AZURE.NOTE] In Azure storage, the term *replication* refers to copying files from one location to another. SQL's *database replication* refers to keeping to multiple secondary databases synchronized with a primary database. 

<!----------------
	The next ## H2's discuss key characteristics of how the feature works. The title is in conversational language and asks the question that will be answered.
------------------->
## How much backup storage is included at no cost?

SQL Database provides up to 200% of your maximum provisioned database storage as backup storage at no additional cost. For example, if you have a Standard DB instance with a provisioned DB size of 250 GB, you have 500 GB of backup storage at no additional charge. If your database exceeds the provided backup storage, you can choose to reduce the retention period by contacting Azure Support. Another option is to pay for extra backup storage that is billed at the standard Read-Access Geographically Redundant Storage (RA-GRS) rate. 

## How often do backups happen?

For local database backups, full database backups happen weekly, differential database backups happen hourly, and transaction log backups happen every five minutes. The first full backup is scheduled immediately after a database is created. It usually completes within 30 minutes, but it can take longer when the database is of a significant size. For example, the initial backup can take longer on a restored database or a database copy. After the first full backup, all further backups are scheduled automatically and managed silently in the background. The exact timing of full and [differential](https://msdn.microsoft.com/library/ms175526.aspx) database backups is determined as it balances the overall system workload. 

For geo-redundant backups, full and differential backups are copied according to the Azure Storage replication schedule.

## How long do you keep my backups?

Each SQL Database backup has a retention period that is based on the [service-tier](sql-database-service-tiers.md) of the database. The retention period for a database in the:

<!------------------

	Using a list so the information is easy to find when scanning.
------------------->

- Basic service tier is seven days.
- Standard service tier is 35 days.
- Premium service tier is 35 days.


If you downgrade your database from the Standard or Premium service tiers to Basic, the backups are saved for seven days. All existing backups older than seven days are no longer available. 

If you upgrade your database from the Basic service tier to Standard or Premium, SQL Database keeps existing backups until they are 35 days old. It keeps new backups as they occur for 35 days.
 
If you delete a database, SQL Database keeps the backups in the same way it would for an online database. For example, suppose you delete a Basic database that has a retention period of seven days. A backup that is four days old is saved for three more days.

If you delete the Azure SQL server that hosts SQL Databases, all databases that belong to the server are also deleted and cannot be recovered. You cannot restore a deleted server.

<!-------------------
OPTIONAL section
## Best practices 
--------------------->

<!-------------------
OPTIONAL section
## General remarks
--------------------->

<!-------------------
OPTIONAL section
## Limitations and restrictions
--------------------->

<!-------------------
OPTIONAL section
## Metadata
--------------------->

<!-------------------
OPTIONAL section
## Performance
--------------------->

<!-------------------
OPTIONAL section
## Permissions
--------------------->

<!-------------------
OPTIONAL section
## Security
--------------------->

<!-------------------
GUIDELINES for Next Steps

	The last section is Next Steps. Give a next step that would be relevant to the customer after they have learned about the feature and the tasks associated with it.  Perhaps point them to one or two key scenarios that use this feature.

	You don't need to repeat links you have already given them.
--------------------->

## Next steps

Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion. To see how database backups into a broader strategy, see [Business continuity overview](sql-database-business-continuity.md).


