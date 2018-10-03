---
title: 命令 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e51d1989b3c492814f5958bacd82bbc01ef76d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105377"
---
# <a name="commands-xmla"></a>命令 (XMLA)
  本参考部分包含 `Command` 方法调用期间可在 `Execute` 元素中使用的 XML for Analysis (XMLA) 元素。  
  
|元素|Description|  
|-------------|-----------------|  
|[Alter 元素 (XMLA)](alter-element-xmla.md)|包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md)方法，以便更改对象的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[Backup 元素](backup-element-xmla.md)|备份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库添加到备份文件。|  
|[Batch 元素](batch-element-xmla.md)|一个或多个 XML for Analysis (XMLA) 命令就会以执行批处理操作，按顺序或并行情况下，实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[BeginTransaction 元素](begintransaction-element-xmla.md)|利用 Analysis Services 实例，在当前会话上开始一个事务。|  
|[Cancel 元素](cancel-element-xmla.md)|取消 Analysis Services 实例上当前正在运行的命令。|  
|[ClearCache 元素](clearcache-element-xmla.md)|清除 Analysis Services 实例上的指定对象的内存缓存。|  
|[CommitTransaction 元素](committransaction-element-xmla.md)|在 Analysis Services 实例的当前会话中提交事务。|  
|[Create 元素](create-element-xmla.md)|包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md)方法来创建对象的 Analysis Services 实例上。|  
|[Delete 元素](delete-element-xmla.md)|删除 Analysis Services 实例的对象。|  
|[DesignAggregations 元素](designaggregations-element-xmla.md)|Analysis Services 实例上创建的聚合设计的聚合。|  
|[Drop 元素](drop-element-xmla.md)|删除维度的属性成员。|  
|[Insert 元素](insert-element-xmla.md)|在维度中插入属性成员。|  
|[Lock 元素](lock-element-xmla.md)|锁定 Analysis Services 实例的指定对象。|  
|[MergePartitions 元素](mergepartitions-element-xmla.md)|将一个或多个源分区的数据合并到目标分区，然后删除源分区。|  
|[NotifyTableChange 元素](notifytablechange-element-xmla.md)|通知 Analysis Services 实例指定数据源中的表发生了更改。|  
|[Process 元素](process-element-xmla.md)|处理 Analysis Services 实例的对象。|  
|[Restore 元素](restore-element-xmla.md)|从备份文件还原 Analysis Services 数据库。|  
|[RollbackTransaction 元素](rollbacktransaction-element-xmla.md)|在 Analysis Services 实例的当前会话中回滚事务。|  
|[Statement 元素](statement-element-xmla.md)|包含查询或要发送的语句使用[Execute](../xml-elements-methods-execute.md)到的 Analysis Services 实例的方法。|  
|[Subscribe 元素](subscribe-element-xmla.md)|订阅跟踪，并返回包含来自 Analysis Services 实例的跟踪事件的行集。|  
|[Synchronize 元素](synchronize-element-xmla.md)|利用另一个现有数据库同步 Analysis Services 数据库。|  
|[Unlock 元素](unlock-element-xmla.md)|取消锁定 Analysis Services 实例上的指定锁。|  
|[Update 元素](../xml-elements-commands/update-element-xmla.md)|更新维度中的属性成员。|  
|[UpdateCells 元素](updatecells-element-xmla.md)|更新启用写操作的多维数据集中的单元。|  
  
  
