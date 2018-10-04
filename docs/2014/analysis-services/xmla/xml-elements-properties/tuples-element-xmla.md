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
- Tuples Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords:
- Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36f29edb149ab6a5c7c22dfe87c4d630289f29cd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128017"
---
# <a name="tuples-element-xmla"></a>Tuples 元素 (XMLA)
  包含一套[元组](tuple-element-xmla.md)对象的[轴](axis-element-xmla.md)使用的元素[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)返回的数据类型[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Axis>  
   ...  
   <Tuples>  
      <Tuple>...</Tuple>  
   </Tuples>  
   ...  
</Axis>  
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
|父元素|[Axis](axis-element-xmla.md)|  
|子元素|[元组](tuple-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 当客户端应用程序设置`AxisFormat`属性设置为*TupleFormat*，则轴将表示为一组元组。 每个 `Axis` 元素都包含一个表示该轴上的元组集的 `Tuples` 元素。 每个元组通过使用表示`Tuple`元素，其中包含[成员](member-element-xmla.md)在轴上每个层次结构中的元素。  
  
## <a name="example"></a>示例  
 下面的示例演示了结构`Tuples`时客户端指定的元素*TupleFormat*或*CustomFormat*为`AxisFormat`XML for Analysis (XMLA) 属性给轴成员如下：  
  
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
  
  
