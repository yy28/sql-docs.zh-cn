---
title: Batch 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d402c1f6c35370a506ed57c43b8fbc05d0b6bef7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178137"
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
  一个或多个 XML for Analysis (XMLA) 命令就会以执行批处理操作，按顺序或并行情况下，实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[绑定](../xml-elements-properties/bindings-element-xmla.md)，[数据源](../xml-elements-properties/source-element-xmla.md)， [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md)，[并行](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> 一个或多个以下的 XMLA 命令： [Alter](alter-element-xmla.md)，[备份](backup-element-xmla.md)， [BeginTransaction](begintransaction-element-xmla.md)， [ClearCache](clearcache-element-xmla.md)， [CommitTransaction](committransaction-element-xmla.md)，[创建](create-element-xmla.md)，[删除](delete-element-xmla.md)， [DesignAggregations](designaggregations-element-xmla.md)，[删除](drop-element-xmla.md)， [插入](insert-element-xmla.md)，[锁](lock-element-xmla.md)， [MergePartitions](mergepartitions-element-xmla.md)， [NotifyTableChange](notifytablechange-element-xmla.md)，[过程](process-element-xmla.md)， [还原](restore-element-xmla.md)， [RollbackTransaction](rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[语句](statement-element-xmla.md)，[订阅](subscribe-element-xmla.md)，[同步](synchronize-element-xmla.md)，[解锁](unlock-element-xmla.md)，[更新](update-element-xmla.md)， [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|（可选的 `Boolean` 属性）指示是否对需要重新处理的所有对象进行处理。<br /><br /> 如果设置为 True，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例会处理需要重新处理的所有对象，作为处理 `Batch` 命令中包含的对象的处理结果。<br /><br /> 如果设置为 `false`，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例仅处理 `Batch` 命令中包含的对象。|  
|事务|（可选的 `Boolean` 属性）指示将 `Batch` 命令中包含的命令视为单个整体事务还是一些单独的事务。<br /><br /> 如果设置为 True，则 `Batch` 命令中包含的所有命令视为单个整体事务。 如有任何命令失败，则将回滚失败的命令之前执行的命令，并且 `Batch` 命令停止，不执行后续命令。<br /><br /> 如果设置为 `false`，则 `Batch` 命令尝试执行每个命令，并提交成功完成的每个命令的结果。|  
  
## <a name="remarks"></a>备注  
  
> [!WARNING]  
>  批处理操作当前不支持 Command/Execute/Statement。  
  
 有关在 XMLA 执行批处理操作的详细信息，请参阅[执行批处理操作&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
