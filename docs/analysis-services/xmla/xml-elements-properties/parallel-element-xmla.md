---
title: "并行元素 (XMLA) |Microsoft 文档"
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Parallel Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parallel
- http://schemas.microsoft.com/analysisservices/2003/engine#Parallel
- microsoft.xml.analysis.parallel
helpviewer_keywords: Parallel element
ms.assetid: 04726d94-37ee-460b-9744-d62b45f536b9
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ecdec84b7701a849134e8315c27085ea167ac66
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
  指定多少处理作业可以使用父并行运行[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- An XMLA process command -->  
   </Parallel>  
   ....  
</Batch>  
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
|父元素|[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|  
|子元素|[Process 元素](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|maxParallel|可选的 **Integer** 属性。 指示要以并行方式运行命令于其上的最大线程数量。 如果未指定或设置为 0，则 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例将根据计算机上可用的处理器数目来确定最优线程数。|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
