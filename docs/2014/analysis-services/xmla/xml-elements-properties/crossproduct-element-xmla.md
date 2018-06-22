---
title: CrossProduct 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CrossProduct Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1324a3c9449383301242ab6d0e76f94c636d9b5e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016473"
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 元素 (XMLA)
  包含有关每个层次结构中的成员列表的有序集之间的叉积[轴](axis-element-xmla.md)用元素[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)返回的数据类型[执行](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Axis>  
   ...  
   <CrossProduct Size="integer">  
      <Members>...</Members>  
   </CrossProduct>  
   ...  
</Axis>  
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
|父元素|[Axis](axis-element-xmla.md)|  
|子元素|[成员](members-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|Size|所需`Integer`属性。 指示 `CrossProduct` 元素表示的叉积中包含的元组数。|  
  
## <a name="remarks"></a>Remarks  
 当客户端应用程序设置`AxisFormat`属性*ClusterFormat*，每个轴上的成员被划分到其中的每个群集都表示之间的每个层次结构中的成员的有序集的叉积的群集。 每个分类都由 `CrossProduct` 元素表示。 每个 `CrossProduct` 元素都包含轴上每个层次结构中的 `Members` 元素。 `CrossProduct` 元素可包含单一层次结构的成员。  
  
## <a name="example"></a>示例  
 下面的示例演示的结构`CrossProduct`元素时客户端指定*ClusterFormat*为`AxisFormat`XMLA 属性，为轴提供的以下成员：  
  
||||||  
|-|-|-|-|-|  
|`Time` 层次结构|1999|1999|2000|2001|  
|`Category` 层次结构|Actual|Budget|Budget|Budget|  
|Clusters|分类 1|分类 1|分类 1|Cluster 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size="4">  
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
      <CrossProduct Size="1">  
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
  
  