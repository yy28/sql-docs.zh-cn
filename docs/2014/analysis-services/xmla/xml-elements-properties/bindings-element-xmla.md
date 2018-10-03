---
title: Bindings 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55aab8ee9c7a2f45dfd04744457f063f5b784168
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173929"
---
# <a name="bindings-element-xmla"></a>Bindings 元素 (XMLA)
  包含一系列[绑定](binding-element-xmla.md)父元素[Batch](../xml-elements-commands/batch-element-xmla.md)或[过程](../xml-elements-commands/process-element-xmla.md)元素。  
  
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../xml-elements-commands/batch-element-xmla.md)，[过程](../xml-elements-commands/process-element-xmla.md)|  
|子元素|[绑定](binding-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
