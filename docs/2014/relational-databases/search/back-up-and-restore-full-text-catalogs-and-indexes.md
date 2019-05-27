---
title: 备份和还原全文目录和索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 28ab36c2f9f500df89b1d936ec60871c0904bc1a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012822"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>备份和还原全文目录和索引
  本主题说明如何备份和还原在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中创建的全文索引。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，全文目录是一个逻辑概念，并不驻留在文件组中。 因此，若要备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的全文目录，必须识别包含属于该目录的全文索引的每个文件组。 然后您必须逐个备份这些文件组。  
  
> [!IMPORTANT]  
>  可以在升级 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库时导入全文目录。 每个导入的全文目录在其自身的文件组中都是一个数据库文件。 若要备份导入的目录，只需备份其文件组即可。 有关详细信息，请参阅 [联机丛书中的](https://go.microsoft.com/fwlink/?LinkID=121052)备份和还原全文目录 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
##  <a name="backingup"></a> 备份全文目录的全文索引  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> 查找全文目录的全文索引  
 你可以通过使用以下 [SELECT](/sql/t-sql/queries/select-transact-sql) 语句检索全文索引的属性，此语句将从 [sys.fulltext_indexes](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql) 和 [sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) 目录视图选择一些列。  
  
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
>  有关创建全文索引的详细信息，请参阅[创建和管理全文索引](create-and-manage-full-text-indexes.md)和 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)。  
  
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
  
-   [备份文件和文件组 (SQL Server)](../backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)  
  

  
##  <a name="Restore_FTI"></a> 还原全文索引  
 还原备份的文件组将还原全文索引文件，以及此文件组中的其他文件。 默认情况下，文件组将还原至该文件组在备份时所在的磁盘位置。  
  
 如果在创建备份时全文索引表处于联机状态并且正在运行填充，则在还原之后将继续填充。  
  
 **还原文件组**  
  
-   [还原文件和文件组 (SQL Server)](../backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [在现有文件上还原文件和文件组 (SQL Server)](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [将文件还原到新位置 (SQL Server)](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)  
  

  
## <a name="see-also"></a>请参阅  
 [管理和监视服务器实例的全文搜索](manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [升级全文搜索](upgrade-full-text-search.md)  
  
  
