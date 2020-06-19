---
title: “重新生成索引”任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 602f2f1065de7be8e1f18eafdd9d5e3cf0ff0a98
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918487"
---
# <a name="rebuild-index-task"></a>“重新生成索引”任务
  “重新生成索引”任务重新生成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库表和视图中的索引。 有关管理索引的详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
 通过使用“重新生成索引”任务，包可以重新生成单个数据库或多个数据库中的索引。 如果任务仅重新生成单个数据库中的索引，则可以选择任务要重新生成其索引的视图和表。  
  
 此任务封装 ALTER INDEX REBUILD 语句并提供下列索引重新生成选项：  
  
-   指定 FILLFACTOR 百分比或使用原始的 FILLFACTOR 量。  
  
-   设置 PAD_INDEX = ON，以将 FILLFACTOR 所指定的可用空间分配给索引的中间级别页。  
  
-   设置 SORT_IN_TEMPDB = ON，以存储用于重新生成 tempdb 中索引的中间排序结果。 当中间排序结果被设置为 OFF 时，结果和索引存储在同一数据库中。  
  
-   设置 IGNORE_DUP_KEY = ON，以便允许多行插入操作（包含违反唯一约束的记录）插入不违反唯一约束的记录。  
  
-   设置 ONLINE = ON 以便不保持表锁，这样，将可以在重建索引期间对基础表进行查询或更新。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的各版本中均不提供联机索引操作。 有关各个版本支持的功能列表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 有关 ALTER INDEX 语句和索引重新生成选项的详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
  
> [!IMPORTANT]  
>  此任务创建它所运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句花费的时间与它重新生成的索引数成正比。 如果配置此任务来重新生成具有大量索引的数据库中所有表和视图中的索引，或重新生成多个数据库中的索引，则任务将花费相当长的时间来生成 Transact-SQL 语句。  
  
## <a name="configuration-of-the-rebuild-index-task"></a>“重新生成索引”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
 [“重新生成索引”任务（维护计划）](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的更多信息，请参阅 [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
