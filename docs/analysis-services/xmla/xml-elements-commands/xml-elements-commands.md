---
title: "命令 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c6a16dfc9dd0ff1c58edcc18c69c1d2f2709145a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="xml-elements---commands"></a>XML 元素的命令
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]此参考部分包含 XML 用于 Analysis (XMLA) 元素，可以在用**命令**期间元素**执行**方法调用。  
  
|元素|Description|  
|-------------|-----------------|  
|[Alter 元素 (XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法，以便更改对象的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[Backup 元素](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|备份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]到备份文件的数据库。|  
|[Batch 元素](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|针对 Analysis (XMLA) 命令作为批处理操作，执行一个或多个 XML，按顺序或并行，实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[BeginTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|利用 Analysis Services 实例，在当前会话上开始一个事务。|  
|[取消元素](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|取消 Analysis Services 实例上当前正在运行的命令。|  
|[ClearCache 元素](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|清除 Analysis Services 实例上的指定对象的内存缓存。|  
|[CommitTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|在 Analysis Services 实例的当前会话中提交事务。|  
|[创建元素](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|包含所使用的 Analysis Services 脚本语言 (ASSL) 元素[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法来创建的 Analysis Services 实例上的对象。|  
|[删除元素](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|删除 Analysis Services 实例的对象。|  
|[DesignAggregations 元素](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|Analysis Services 实例上创建的聚合设计的聚合。|  
|[删除元素](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|删除维度的属性成员。|  
|[插入元素](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|在维度中插入属性成员。|  
|[锁定元素](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|锁定 Analysis Services 实例的指定对象。|  
|[撰写 MergePartitions 元素](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|将一个或多个源分区的数据合并到目标分区，，然后删除源分区。|  
|[NotifyTableChange 元素](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|通知 Analysis Services 实例指定数据源中的表发生了更改。|  
|[Process 元素](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|处理 Analysis Services 实例的对象。|  
|[Restore 元素](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|从备份文件还原 Analysis Services 数据库。|  
|[RollbackTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|在 Analysis Services 实例的当前会话中回滚事务。|  
|[语句元素](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|包含查询或语句发送使用[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)到的 Analysis Services 实例的方法。|  
|[Subscribe 元素](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|订阅跟踪，并返回包含来自 Analysis Services 实例的跟踪事件的行集。|  
|[同步元素](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|利用另一个现有数据库同步 Analysis Services 数据库。|  
|[解除锁定元素](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|取消锁定 Analysis Services 实例上的指定锁。|  
|[Update 元素](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|更新维度中的属性成员。|  
|[UpdateCells 元素](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|更新启用写操作的多维数据集中的单元。|  
  
  
