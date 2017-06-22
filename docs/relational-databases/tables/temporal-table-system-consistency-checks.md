---
title: "临时表系统一致性检查 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ec081d42-57e4-43c7-9e1c-317ba8f23437
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb67454080657b99983e33e4c46858124b735433
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="temporal-table-system-consistency-checks"></a>临时表系统一致性检查
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用临时表时，系统将执行若干一致性检查以确保架构符合临时要求，而且数据一致且将始终一致。 此外，已将临时检查添加到 **DBCC CHECKCONSTRAINTS** 语句。  
  
## <a name="system-consistency-checks"></a>系统一致性检查  
 在将 **SYSTEM_VERSIONING** 设置为 **ON**之前，系统将对历史记录表和当前表执行一系列检查。 如果历史记录表不为空，则这些检查分为架构检查和数据检查。 此外，系统还会执行运行时一致性检查。  
  
### <a name="schema-check"></a>架构检查  
 创建表或将表更改为临时表时，系统将验证其是否满足这些要求：  
  
1.  当前表和历史记录表中的列名和列数相同。  
  
2.  当前表与历史记录表中每一列的数据类型都一致。  
  
3.  将期间列设置为 **NOT NULL**。  
  
4.  当前表有主键约束，而历史记录表没有主键约束。  
  
5.  历史记录表中未定义任何 **IDENTITY** 列。  
  
6.  历史记录表中未定义任何触发器。  
  
7.  历史记录表中未定义任何外键。  
  
8.  历史记录表中未定义任何表或列约束。 但是，允许使用历史记录表上的默认列值。  
  
9. 不会将历史记录表置于只读文件组中。  
  
10. 历史记录表未配置更改跟踪或更改数据捕获。  
  
### <a name="data-consistency-check"></a>数据一致性检查  
 将 **SYSTEM_VERSIONING** 设置为 **ON** 并作为任何 DML 操作的一部分之前，系统将执行以下检查： **SysEndTime** ≥**SysStartTime**  
  
 创建现有历史记录表的链接时，可以选择执行数据一致性检查。 此数据一致性检查可确保现有记录不重叠，并且每个单独的记录都满足临时要求。 系统默认执行数据一致性检查。 通常，每当当前表和历史记录表之间的数据可能失去同步时（如纳入已填充历史数据的现有历史记录表时），建议执行数据一致性检查。  
  
> [!WARNING]  
>  手动更改系统时钟可能会导致系统意外失败，原因是为防止出现重叠情况（即记录的结束时间不晚于其开始时间）而进行的运行时数据一致性检查将失败。  
  
## <a name="dbcc-checkconstraints"></a>DBCC CHECKCONSTRAINTS  
 **DBCC CHECKCONSTRAINTS** 命令包括临时数据一致性检查。 有关详细信息，请参阅 [DBCC CHECKCONSTRAINTS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)。  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 我们洗耳恭听  
 你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20System%20Consistency%20Checks%20page)  
  
## <a name="see-also"></a>另请参阅  
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [系统版本控制临时表入门](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [临时表分区](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [临时表注意事项和限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [临时表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系统版本控制临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

