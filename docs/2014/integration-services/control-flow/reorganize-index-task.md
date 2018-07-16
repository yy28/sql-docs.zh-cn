---
title: “重新组织索引”任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.reorganizeindextask.f1
helpviewer_keywords:
- reorganizing indexes
- Reorganize Index task [Integration Services]
- indexes [Integration Services]
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4a05f0a6e43ff36258d665c351b32565f89bd492
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314207"
---
# <a name="reorganize-index-task"></a>“重新组织索引”任务
  “重新组织索引”任务重新组织 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库表和视图中的索引。 有关管理索引的详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
 通过使用“重新组织索引”任务，包可以重新组织单个数据库或多个数据库中的索引。 如果此任务仅重新组织单个数据库中的索引，则可以选择任务要重新组织其索引的视图或表。 “重新组织索引”任务还包含压缩大型对象数据的选项。 大型对象数据是具有`image`， `text`， `ntext`， `varchar(max)`， `nvarchar(max)`， `varbinary(max)`，或`xml`数据类型。 有关详细信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)。  
  
 “重新组织索引”任务封装了 Transact-SQL ALTER INDEX 语句。 如果选择压缩大型对象数据，则该语句使用 REORGANIZE WITH (LOB_COMPACTION = ON) 子句，否则 LOB_COMPACTION 将设置为 OFF。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
  
> [!IMPORTANT]  
>  此任务创建其运行的 Transact-SQL 语句所需的时间与任务重新组织的索引数成正比。 如果配置此任务来重新组织具有大量索引的数据库中所有表和视图中的索引，或重新组织多个数据库中的索引，则任务将花费相当长的时间来生成 Transact-SQL 语句。  
  
## <a name="configuration-of-the-reorganize-index-task"></a>“重新组织索引”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题：  
  
-   [“重新组织索引”任务（维护计划）](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请参阅 [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
