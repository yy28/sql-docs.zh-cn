---
title: 将数据库恢复到数据库快照 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
author: stevestein
ms.author: sstein
ms.openlocfilehash: c636db77ffdf8249cf03814abca031b0897fb4c9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909512"
---
# <a name="revert-a-database-to-a-database-snapshot"></a>将数据库恢复到数据库快照
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果联机数据库中的数据损坏，在某些情况下，将数据库恢复到发生损坏之前的数据库快照可能是一种合适的替代方案，替代从备份中还原数据库。 例如，通过恢复数据库可能会有助于从最近出现的严重用户错误（如删除的表）中恢复。 但是，在该快照创建以后进行的所有更改都会丢失。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要将数据库恢复到数据库快照，请使用：** [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 下列情况不支持恢复：  
  
-   数据库存在多个快照。 还原时，对于计划恢复的数据库，只能存在一个快照。  
  
-   数据库中存在任何只读或压缩的文件组。  
  
-   数据库中有快照创建时联机而现在却脱机的任何文件。  
  
 在恢复数据库之前，请考虑以下限制：  
  
-   恢复并不适用于介质恢复。 数据库快照是不完整的数据库文件副本，因此，如果数据库或数据库快照损坏，则不可能从快照进行恢复。 另外，如果损坏的话，即便可以恢复，也可能无法更正该问题。 因此，定期执行备份并对还原计划进行测试对于保护数据库至关重要。 有关详细信息，请参阅 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
    > [!NOTE]  
    >  如果需要能够将源数据库还原至创建数据库快照的时点，请使用完整恢复模式并实施允许您执行该操作的备份策略。  
  
-   原始的源数据库会被恢复后的数据库覆盖，因此该快照创建后的所有数据库更新都会丢失。  
  
-   恢复操作还会覆盖旧日志文件并重新生成日志。 因此，无法将恢复后的数据库前滚至发生用户错误的点。 所以，建议您在恢复数据库之前备份日志。  
  
    > [!NOTE]  
    >  虽然不能还原原始日志以便将数据库前滚，但是可以使用原始日志文件中的信息来重新构造丢失的数据。  
  
-   恢复操作会打断日志备份链。 因此，必须首先进行完整的数据库备份或文件备份，然后才能够进行恢复后的数据库的日志备份。 建议您进行完整的数据库备份。  
  
-   在执行恢复操作的过程中，快照和源数据库都不可用。 源数据库和快照都将被标记为“正在还原”。 如果在执行恢复操作的过程中出现错误，则当数据库再次启动时，恢复操作将会尝试完成恢复。  
  
-   恢复后的数据库的元数据与创建快照时的元数据相同。  
  
-   恢复操作会删除所有的全文目录。  
  
###  <a name="Prerequisites"></a> 先决条件  
 确保源数据库与数据库快照满足以下先决条件：  
  
-   确认数据库没有损坏。  
  
    > [!NOTE]  
    >  如果数据库已损坏，您将需要从备份中还原它。 有关详细信息，请参阅[完整数据库还原（简单恢复模式）](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)或[数据库还原（完整恢复模式）](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)。  
  
-   标识在发生错误之前新近创建的快照。 有关详细信息，请参阅 [查看数据库快照 (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
-   删除当前数据库中存在的任何其他快照。 有关详细信息，请参阅 [删除数据库快照 (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 任何具有源数据库 RESTORE DATABASE 权限的用户都可以将其恢复至创建数据库快照时的状态。  
  
##  <a name="TsqlProcedure"></a> 如何将数据库恢复到数据库快照（使用 Transact-SQL）  
 **将数据库恢复到数据库快照**  
  
> [!NOTE]  
>  有关此过程的示例，请参阅本节后面的 [示例 (Transact-SQL)](#TsqlExample)。  
  
1.  标识要将数据库恢复到的数据库快照。 你可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的一个数据库上查看快照（请参阅 [查看数据库快照 (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)）。 此外，还可以在 **sys.databases (Transact-SQL)** 目录视图的 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 列中找到某个视图的源数据库。  
  
2.  删除其他任何数据库快照。  
  
     有关删除快照的信息，请参阅 [删除数据库快照 (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md). 如果数据库使用完整恢复模式，则在执行恢复之前，应先备份日志。 有关详细信息，请参阅[备份事务日志 (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md) 或[在数据库损坏时备份事务日志 (SQL Server)](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)。  
  
3.  执行恢复操作。  
  
     恢复操作要求对源数据库具有 RESTORE DATABASE 权限。 若要恢复数据库，请使用下列 Transact-SQL 语句：  
  
     RESTORE DATABASE *database_name* FROM DATABASE_SNAPSHOT **=** _database_snapshot_name_  
  
     其中， *database_name* 是源数据库的名称， *database_snapshot_name* 是要将数据库恢复到的快照的名称。 注意，必须在此语句中指定快照名称而非备份设备。  
  
     有关详细信息，请参阅 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md).  
  
    > [!NOTE]  
    >  在恢复操作过程中，快照和源数据库都不可用。 源数据库和快照都标记为“还原中”。 如果在恢复操作期间发生错误，则数据库在重新启动后，将尝试完成恢复操作。  
  
4.  如果创建数据库快照后数据库所有者发生了变化，您最好更新恢复的数据库的数据库所有者。  
  
    > [!NOTE]  
    >  已恢复的数据库将保留数据库快照的权限和配置（例如，数据库所有者和恢复模式）。  
  
5.  启动数据库。  
  
6.  尤其在使用完整（或大容量日志）恢复模式时，可以选择备份恢复后的数据库。 备份数据库，请参阅[创建完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  

###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 本节包含演示如何将数据库恢复到数据库快照的以下示例：  
  
-   A. [恢复 AdventureWorks 数据库的快照](#Reverting_AW)  
  
-   B. [恢复 Sales 数据库的快照](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. 恢复 AdventureWorks 数据库的快照  
 此示例假定 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库当前只存在一个快照。 有关在此创建数据库要恢复到的快照的示例，请参阅 [创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. 恢复 Sales 数据库的快照  
 此示例假定在 **Sales** 数据库当前存在两个快照： **sales_snapshot0600** 和 **sales_snapshot1200**。 此示例删除了较旧的快照并将数据库恢复到较新的快照。  
  
 有关用于创建此示例所基于的示例数据库和快照的代码，请参阅：  
  
-   有关 **Sales** 数据库和 **sales_snapshot0600** 快照，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md) 中的“使用文件组创建数据库”和“创建数据库快照”。  
  
-   有关 **sales_snapshot1200** 快照，请参阅 [创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [查看数据库快照 (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [删除数据库快照 (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [数据库镜像和数据库快照 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
