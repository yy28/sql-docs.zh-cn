---
title: 绑定元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Bindings Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.bindings
- urn:schemas-microsoft-com:xml-analysis#Bindings
- http://schemas.microsoft.com/analysisservices/2003/engine#Bindings
helpviewer_keywords:
- Bindings element
ms.assetid: caa34cab-f61f-4f39-b800-af1601714daa
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: c630f6f5992c528ee89099c44d2ea69a9e352f5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125923"
---
# <a name="bindings-element-xmla"></a>Bindings 元素 (XMLA)
  包含一套[绑定](binding-element-xmla.md)父元素[批处理](../xml-elements-commands/batch-element-xmla.md)或[过程](../xml-elements-commands/process-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <Bindings>  
      <Binding>...</Binding>  
   </Bindings>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../xml-elements-commands/batch-element-xmla.md)，[过程](../xml-elements-commands/process-element-xmla.md)|  
|子元素|[绑定](binding-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  