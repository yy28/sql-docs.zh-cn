---
title: CrossProduct 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07e34958589bd9366cda6b42207c289bfda72453
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含有关每个层次结构中的成员列表的有序集之间的叉积[轴](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)用元素[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)返回的数据类型[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[轴](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|子元素|[成员](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|Size|所需**整数**属性。 指示由跨产品中包含的元组的数目**CrossProduct**元素。|  
  
## <a name="remarks"></a>注释  
 当客户端应用程序设置**AxisFormat**属性*ClusterFormat*，每个轴上的成员被划分到其中的每个群集都表示之间有序集的叉积的群集从每个层次结构的成员。 每个群集都由**CrossProduct**元素。 每个**CrossProduct**元素包含**成员**在轴上的每个层次结构的元素。 A **CrossProduct**元素可以包含来自单一层次结构的成员。  
  
## <a name="example"></a>示例  
 下面的示例演示的结构**CrossProduct**元素时客户端指定*ClusterFormat*为**AxisFormat**给定的 XMLA 属性轴的以下成员：  
  
||||||  
|-|-|-|-|-|  
|**时间**层次结构|1999|1999|2000|2001|  
|**类别**层次结构|Actual|Budget|Budget|Budget|  
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
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
