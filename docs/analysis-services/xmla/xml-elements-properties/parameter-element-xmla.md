---
title: "参数元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Parameter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parameter
- microsoft.xml.analysis.parameter
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameter
helpviewer_keywords:
- Parameter element
ms.assetid: fe31ac3d-a3e8-4f60-a81a-c43271ddbed4
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7b2305957444f451b11d4522c9a4ace1dd1c53f5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="parameter-element-xmla"></a>Parameter 元素 (XMLA)
  包含的名称和使用的参数的值[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[参数](../../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md)|  
|子元素|[名称](../../../analysis-services/xmla/xml-elements-properties/name-element-parameter-xmla.md)，[值](../../../analysis-services/xmla/xml-elements-properties/value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>注释  
 一些 XML Analysis (XMLA) 命令，如[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令，也可以要求的其他信息。 **参数**元素提供用于提供其他信息，包括 XMLA 命令分块的信息的机制。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

