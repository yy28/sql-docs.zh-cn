---
title: 在批量导入中按最小方式记录日志的前提条件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99572edbc477999a1ccc8f6c1fff89b5e04521d6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "70910831"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Prerequisites for Minimal Logging in Bulk Import
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  对于完整恢复模式下的数据库，大容量导入执行的所有行插入操作都会完整地记录在事务日志中。 如果使用完整恢复模式，大型数据导入会导致填充事务日志的速度很快。 相反，对于简单恢复模式或大容量日志恢复模式，大容量导入操作的最小日志记录减少了大容量导入操作填满日志空间的可能性。 另外，最小日志记录的效率也比按完整方式记录日志高。  
  
> [!NOTE]  
>  大容量日志恢复模式旨在于大容量操作期间临时替换完整的恢复模式。  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>在大容量导入操作中最小日志记录的表要求  
 最小日志记录要求目标表满足下列条件：  
  
-   当前没有复制表。  
  
-   指定了表锁定（使用 TABLOCK）。 
  
    > [!NOTE]  
    >  尽管在最小日志记录的大容量导入操作过程中，数据插入操作没有记录在事务日志中，但每当为表分配新区时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 仍会记录区分配信息。  
  
-   表不是内存优化表。  
  
 对于某个表，是否进行最小日志记录还取决于该表是否有索引，如果有，则还取决于该表是否为空：  
  
-   如果表没有索引，则按最小方式记录数据页。  
  
-   如果表没有聚集索引但是有一个或多个非聚集索引，则始终按最小方式记录数据页。 但是，记录索引页的方式取决于该表是否为空：  
  
    -   如果该表为空，则按最小方式记录索引页。  如果您以空表开始并分多批大容量导入数据，则对于第一批，将按最小方式记录索引页和数据页，但从第二批开始，将只按最小方式记录数据页。 
  
    -   如果该表不为空，则按完整方式记录索引页。    

-   如果表有聚集索引且为空，则按最小方式记录数据页和索引页。 相反，如果表有基于 btree 的聚集索引且不为空，则无论采用何种恢复模式，均按完整方式记录数据页和索引页。 如果以空表和行存储表开始并批量导入数据，对于第一批，将按最小方式记录索引页和数据页，但从第二批开始，将只按批量方式记录数据页。

- 有关记录群集列存储索引 (CCI) 的信息，请参阅[列存储索引数据加载指南](../indexes/columnstore-indexes-data-loading-guidance.md#plan-bulk-load-sizes-to-minimize-delta-rowgroups)。
  

  
> [!NOTE]  
>  启用事务复制时，将完全记录 BULK INSERT 操作，即使处于大容量日志恢复模式下。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [查看或更改数据库的恢复模式 (SQL Server)](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
  
## <a name="see-also"></a>另请参阅  
 [恢复模式 (SQL Server)](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)  
  
  
