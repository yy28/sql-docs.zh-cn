---
title: "轴元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Axes Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords: Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d8e1f992cd7cf9a6aceb1490d78aa0fba49b7758
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="axes-element-xmla"></a>Axes 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含一套[轴](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)元素表示包含的轴数据[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)用元素[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 下**轴**元素，**轴**元素中发生的数据集，从零开始的顺序列出。 **AxisFormat** XMLA 属性设置将决定如何**轴**元素的格式。 有关详细信息**AxisFormat**属性，请参阅[支持 XMLA 属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 轴表示一个元组集，其中的所有元组都具有相同的维数。 元组集可采用各具优势的不同方式来表示。 例如，以下由 4 个元组组成的元组集可表示为二维元组的集合或两个一维元组集的笛卡尔积。  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|Actual|Budget|Actual|Budget|  
  
 此元组集可表示为二维元组的集合：  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 此元组集还可表示为两个一维元组集的笛卡尔积：  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 第一种表示形式（二维元组）更易于客户端工具使用。 第二种表示形式（一维元组集的笛卡尔积）占用的空间更少，并能保留元组集的多维特性。  
  
 下表列出了可用于定义轴的结构和成员并描述其结构特征的操作。  
  
|运算|Description|  
|---------------|-----------------|  
|成员|表示维度层次结构成员的轴的最小单位。|  
|成员|集合**成员**对象来自同一维度层次结构。|  
|Tuple|来自不同维度层次结构的成员的集合。|  
|元组|集合**元组**具有相同维数的对象。|  
|Union|多个集的并集。|  
|CrossJoin|集的笛卡尔积。|  
  
 这些操作如下所示转换二维元组和一维元组集的笛卡尔积。  
  
## <a name="two-dimensional-tuples"></a>二维元组  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>一维元组集的笛卡尔积  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 客户端可以使用**AxisFormat**属性来请求特定的表示形式。  
  
## <a name="see-also"></a>另请参阅  
 [MDDataSet 数据类型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
