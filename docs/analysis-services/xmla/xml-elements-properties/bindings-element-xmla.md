---
title: 绑定元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd8f84446aa44aa6686adefc1cfac54786db3a95
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="bindings-element-xmla"></a>Bindings 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一套[绑定](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)父元素[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)，[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|[绑定](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
