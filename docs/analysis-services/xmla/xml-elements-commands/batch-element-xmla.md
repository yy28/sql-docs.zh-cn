---
title: 批处理元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4644b8775212eae0cb6d912df9bc415c5fc96ec7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34573939"
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  执行一个或多个 XML Analysis (XMLA) 命令作为批处理操作，按顺序或并行，Analysis Services 实例上。  
  
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[绑定](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)，[数据源](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)， [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)，[并行](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> 一个或多个以下的 XMLA 命令： [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)， [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)， [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，[创建](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)，[删除](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)，[删除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)， [插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[锁](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)，[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)， [还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[语句](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)，[订阅](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)，[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)，[解锁](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)， [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|(可选**布尔**属性) 该值指示是否将处理需要重新处理的所有对象。<br /><br /> 如果设置为 true，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例处理需要重新处理作为处理中包含的对象的任何对象**批处理**命令。<br /><br /> 如果设置为**false**、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例处理这些对象包括在**批处理**命令。|  
|事务|(可选**布尔**属性) 指示该命令包含在**批处理**命令将被视为单个事务或个别的事务。<br /><br /> 如果设置为 true 的所有命令中包含**批处理**命令被视为单个事务。 如果任何命令失败，在失败的命令之前执行的命令回滚，和**批处理**命令停止而不执行后续的命令。<br /><br /> 如果设置为**false**、**批处理**命令尝试执行每个命令，并提交成功完成每个命令的结果。|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  批处理操作当前不支持 Command/Execute/Statement。  
  
 有关在 XMLA 执行批处理操作的详细信息，请参阅[执行批处理操作&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。  
  
## <a name="see-also"></a>另请参阅
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
