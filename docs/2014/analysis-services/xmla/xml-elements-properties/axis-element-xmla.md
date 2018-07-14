---
title: Axis 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Axis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3e68903dc828f4b14ac60892d1b6fc2baed2f30
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263223"
---
# <a name="axis-element-xmla"></a>Axis 元素 (XMLA)
  包含一组用于表示在多维数据集中所包含的单个轴的元组[轴](axes-element-xmla.md)使用的元素[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)返回的数据类型[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Axes>  
   ...  
   <Axis> <!-- when AxisFormat XMLA property is set to ClusterFormat -->  
      <CrossProduct>...</CrossProduct>  
   </Axis>  
   <Axis> <!-- when AxisFormat XMLA property is set to TupleFormat or CustomFormat -->  
      <Tuples>...</Tuples>  
   </Axis>  
   ...  
</Axes>  
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
|父元素|[轴](axes-element-xmla.md)|  
|子元素|[CrossProduct](crossproduct-element-xmla.md)或[元组](tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Axis` 元素的内容因 `AxisFormat` 方法所使用的`Execute` XMLA 属性的值而异。  
  
## <a name="tupleformat"></a>TupleFormat  
 当客户端应用程序设置`AxisFormat`属性设置为*TupleFormat*，则轴将表示为一组元组。 每个 `Axis` 元素都包含有一个表示该轴上的元组集的 `Tuples` 元素。 每个元组都是通过使用 `Tuple` 元素来表示的，该元素包含轴上每个层次结构中的 `Member` 元素。  
  
## <a name="clusterformat"></a>ClusterFormat  
 当客户端应用程序设置`AxisFormat`属性设置为*ClusterFormat*，每个轴上的成员被划分到其中的每个群集表示之间的每个层次结构中成员的有序集的叉积的群集。 每个 `Axis` 元素都包含一个或多个 `CrossProduct` 元素。 每个 `CrossProduct` 元素都包含轴上每个层次结构中的 `Members` 元素。  
  
## <a name="customformat"></a>CustomFormat  
 当客户端应用程序设置`AxisFormat`属性设置为*CustomFormat*，处理值与相同*TupleFormat* Analysis Services 实例的值。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例演示了结构`Axis`时客户端指定的元素*TupleFormat*或*CustomFormat*为`AxisFormat`给出以下 XMLA 属性轴的成员：  
  
|||||  
|-|-|-|-|  
|`Time` 层次结构|1999|1999|2000|  
|`Category` 层次结构|Actual|Budget|Budget|  
  
### <a name="code"></a>代码  
  
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
  
### <a name="description"></a>Description  
 下面的示例演示了结构`Axis`时客户端指定的元素*ClusterFormat*为`AxisFormat`XMLA 属性的以下成员的轴：  
  
||||||  
|-|-|-|-|-|  
|`Time` 层次结构|1999|1999|2000|2001|  
|`Category` 层次结构|Actual|Budget|Budget|Budget|  
|Clusters|分类 1|分类 1|分类 1|Cluster 2|  
  
### <a name="code"></a>代码  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size = "1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
