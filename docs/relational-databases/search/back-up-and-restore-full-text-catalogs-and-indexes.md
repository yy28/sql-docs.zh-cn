---
title: 备份和还原全文目录和索引 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 51ab502a0b4aa1c0740a41fee15bee098bddfd5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024436"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>备份和还原全文目录和索引
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题说明如何备份和还原在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中创建的全文索引。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，全文目录是一个逻辑概念，并不驻留在文件组中。 因此，若要备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的全文目录，必须识别包含属于该目录的全文索引的每个文件组。 然后您必须逐个备份这些文件组。  
  
> [!IMPORTANT]  
>  可以在升级 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库时导入全文目录。 每个导入的全文目录在其自身的文件组中都是一个数据库文件。 若要备份导入的目录，只需备份其文件组即可。 有关详细信息，请参阅 [联机丛书中的](https://go.microsoft.com/fwlink/?LinkID=121052)备份和还原全文目录 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
##  <a name="backingup"></a> 备份全文目录的全文索引  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> 查找全文目录的全文索引  
 你可以通过使用以下 [SELECT](../../t-sql/queries/select-transact-sql.md) 语句检索全文索引的属性，此语句将从 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) 和 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 目录视图选择一些列。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  
  
###  <a name="Find_FG_of_FTI"></a> 查找包含全文索引的文件组或文件  
 创建全文索引时，该全文索引将放在以下某个位置：  
  
-   用户指定的文件组。  
  
-   与基表或视图相同的文件组（对于未分区表而言）。  
  
-   主文件组（对于分区表而言）。  
  
> [!NOTE]  
>  有关创建全文索引的详细信息，请参阅[创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)和 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
 若要查找表或视图的全文索引所属的文件组，请使用以下查询，其中 *object_name* 为表或视图的名称：  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  
  
###  <a name="Back_up_FTIs_of_FTC"></a> 备份包含全文索引的文件组  
 在找到包含全文目录索引的文件组后，您需要备份找到的每个文件组。 在备份过程中，不会删除或添加全文目录。  
  
 文件组的首次备份必须是完整文件备份。 在创建文件组的完整文件备份之后，您可以仅备份文件组中的更改，方法是：创建一系列基于完整文件备份的一个或多个差异文件备份。  
  
 **备份文件和文件组**  
  
-   [备份文件和文件组 (SQL Server)](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
  
  
##  <a name="Restore_FTI"></a> 还原全文索引  
 还原备份的文件组将还原全文索引文件，以及此文件组中的其他文件。 默认情况下，文件组将还原至该文件组在备份时所在的磁盘位置。  
  
 如果在创建备份时全文索引表处于联机状态并且正在运行填充，则在还原之后将继续填充。  
  
 **还原文件组**  
  
-   [还原文件和文件组 (SQL Server)](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [在现有文件上还原文件和文件组 (SQL Server)](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [将文件还原到新位置 (SQL Server)](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视服务器实例的全文搜索](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [升级全文搜索](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
