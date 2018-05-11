---
title: InstanceSelection 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a3170ebd104d142c74d19c8b0be65f8cada08cf4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="instanceselection-element-assl"></a>InstanceSelection 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供对客户端应用程序建议如何的项列表的提示应显示，基于预期数量的列表中的项。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下列字符串之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|*InclusionThresholdSetting*|不显示选择列表。 允许用户直接输入值。|  
|*下拉列表中*|项数很少，足以在下拉列表中显示。|  
|*列表*|项数太多，不能在下拉列表中显示，但不需要进行筛选。|  
|*FilteredList*|项数太多，需要用户进行筛选才能显示。|  
|*MandatoryFilter*|项数太多，必须一直使用筛选才能显示。|  
  
 对应于的允许值为枚举**InstanceSelection**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.InstanceSelection>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
