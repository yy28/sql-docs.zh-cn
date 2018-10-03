---
title: Members 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1a418c0dc131f02c1afc2f2dd67810ebf90ea2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083489"
---
# <a name="members-element-xmla"></a>Members 元素 (XMLA)
  包含一系列[成员](member-element-xmla.md)包含由父元素[CrossProduct](crossproduct-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
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
|父元素|[CrossProduct](crossproduct-element-xmla.md)|  
|子元素|[成员](member-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|层次结构|所需`String`属性。 `Members` 元素包含的成员所属的层次结构的名称。|  
  
## <a name="remarks"></a>备注  
 当客户端应用程序设置`AxisFormat`属性设置为*ClusterFormat*，每个轴上的成员被划分到其中的每个群集表示之间的每个层次结构中成员的有序集的叉积的群集。 每个 `Axis` 元素都包含一个或多个 `CrossProduct` 元素。 每个 `CrossProduct` 元素都包含轴上每个层次结构中的 `Members` 元素。 而对叉积中包括的指定层次结构的每个成员，`Members` 元素又包含一个 `Member` 元素。  
  
## <a name="example"></a>示例  
 下面的示例演示了结构`Members`时客户端指定的元素*ClusterFormat*为`AxisFormat`XMLA 属性的以下成员的轴：  
  
||||||  
|-|-|-|-|-|  
|`Time` 层次结构|1999|1999|2000|2001|  
|`Category` 层次结构|Actual|Budget|Budget|Budget|  
|Clusters|分类 1|分类 1|分类 1|Cluster 2|  
  
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
  
  
