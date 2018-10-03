---
title: 元组元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Tuple Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32dc7b75f47acf69a8d16e33bc25ac505b1c9333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061337"
---
# <a name="tuple-element-xmla"></a>Tuple 元素 (XMLA)
  包含一组 [Member](member-element-xmla.md) 元素，这些元素包含在父 [Tuples](tuples-element-xmla.md) 元素中。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[元组](tuples-element-xmla.md)|  
|子元素|[成员](member-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 当客户端应用程序设置`AxisFormat`属性设置为*TupleFormat*，则轴将表示为一组元组。 每个 `Axis` 元素都包含一个表示该轴上的元组集的 `Tuples` 元素。 每个元组都是通过使用 `Tuple` 元素来表示的，该元素包含轴上每个层次结构中的 `Member` 元素。  
  
## <a name="example"></a>示例  
 下面的示例演示了结构`Tuple`时客户端指定的元素*TupleFormat*或*CustomFormat*为`AxisFormat`给出以下 XMLA 属性轴的成员：  
  
|||||  
|-|-|-|-|  
|`Time` 层次结构|1999|1999|2000|  
|`Category` 层次结构|Actual|Budget|Budget|  
  
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
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
