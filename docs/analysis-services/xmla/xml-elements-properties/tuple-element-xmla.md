---
title: "元组元素 (XMLA) |Microsoft 文档"
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
- Tuple Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11a9d3b633e680154787615c04ee1f08b65b8139
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="tuple-element-xmla"></a>Tuple 元素 (XMLA)
  包含一组 [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 元素，这些元素包含在父 [Tuples](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md) 元素中。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
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
|父元素|[元组](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
|子元素|[成员](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 如果客户端应用程序将 **AxisFormat** 属性设置为 TupleFormat，则轴将表示为元组集。 每个 **Axis** 元素都包含一个表示该轴上的元组集的 **Tuples** 元素。 每个元组都是通过使用 **Tuple** 元素来表示的，该元素包含轴上每个层次结构中的 **Member** 元素。  
  
## <a name="example"></a>示例  
 下例说明了客户指定 **AxisFormat** XMLA 属性的 TupleFormat 或 CustomFormat 时**Tuple** 元素的结构，给出的轴成员如下：  
  
|||||  
|-|-|-|-|  
|**时间**层次结构|1999|1999|2000|  
|**类别**层次结构|Actual|Budget|Budget|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
