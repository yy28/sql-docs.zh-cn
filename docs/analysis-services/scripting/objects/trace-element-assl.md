---
title: 跟踪元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 420150dbdf4910683fc78c8c364d2cf0976adfc3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="trace-element-assl"></a>Trace 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义可查询的跟踪。  
  
## <a name="syntax"></a>语法  
  
```  
  
      Profiler syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LogFileName>...</LogFileName>  
      <LogFileAppend>...</LogFileAppend>  
      <LogFileSize>...</LogFileSize>  
      <Audit>...</Audit>  
      <LogFileRollover>...</LogFileRollover>  
      <AutoRestart>...</AutoRestart>  
      <StopTime>...</StopTime>  
      <Filter>...</Filter>  
      <Events>...</Events>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
```  
  
      Extended Events syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate> 
      <AutoRestart>...</AutoRestart>
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[跟踪](../../../analysis-services/scripting/collections/traces-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[审核](../../../analysis-services/scripting/properties/audit-element-assl.md)， [AutoRestart](../../../analysis-services/scripting/properties/autorestart-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[事件](../../../analysis-services/scripting/collections/events-element-assl.md)，[筛选器](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [LogFileAppend](../../../analysis-services/scripting/properties/logfileappend-element-assl.md)， [LogFileName](../../../analysis-services/scripting/properties/logfilename-element-assl.md)， [LogFileRollover](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md)， [LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[停止时间](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另请参阅  
 [服务器元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
