---
title: 轴元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c4f7b48d02a7dd923c6882f96227f52d404390f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="axis-element-xmla"></a>Axis 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一组用于表示单个坐标轴中包含的多维数据集的元组[轴](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)用元素[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)返回的数据类型[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[轴](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)|  
|子元素|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)或[元组](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 内容**轴**元素而异的值**AxisFormat** XMLA 属性由**执行**方法。  
  
## <a name="tupleformat"></a>TupleFormat  
 如果客户端应用程序将 **AxisFormat** 属性设置为 TupleFormat，则轴将表示为元组集。 每个**轴**元素包含**元组**元素，表示该轴上的元组的集。 每个元组都是通过使用 **Tuple** 元素来表示的，该元素包含轴上每个层次结构中的 **Member** 元素。  
  
## <a name="clusterformat"></a>ClusterFormat  
 当客户端应用程序设置**AxisFormat**属性*ClusterFormat*，每个轴上的成员被划分到其中的每个群集都表示之间有序集的叉积的群集从每个层次结构的成员。 每个**轴**元素包含一个或多个**CrossProduct**元素。 每个**CrossProduct**元素包含**成员**在轴上的每个层次结构的元素。  
  
## <a name="customformat"></a>CustomFormat  
 当客户端应用程序设置**AxisFormat**属性*CustomFormat*，值被视为相同*TupleFormat* Analysis Services 实例的值。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例演示的结构**轴**元素时客户端指定*TupleFormat*或*CustomFormat*为**AxisFormat** XMLA 属性，为轴提供的以下成员：  
  
|||||  
|-|-|-|-|  
|**时间**层次结构|1999|1999|2000|  
|**类别**层次结构|Actual|Budget|Budget|  
  
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
 下面的示例演示的结构**轴**元素时客户端指定*ClusterFormat*为**AxisFormat**给定以下 XMLA 属性轴的成员：  
  
||||||  
|-|-|-|-|-|  
|**时间**层次结构|1999|1999|2000|2001|  
|**类别**层次结构|Actual|Budget|Budget|Budget|  
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
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
