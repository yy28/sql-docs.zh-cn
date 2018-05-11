---
title: OrderByAttributeID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 08414e3c5ccd3806ba8b77ad8b39fb636c92b775
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="orderbyattributeid-element-assl"></a>OrderByAttributeID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识所依据的成员进行排序的另一个属性[维度](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)属性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderByAttributeID>...</OrderByAttributeID>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **OrderByAttributeID**元素是时才使用的值[OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md)元素**DimensionAttribute**设置为*AttributeKey*或*AttributeName*。  
  
 对应于的父元素**OrderByAttributeID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
