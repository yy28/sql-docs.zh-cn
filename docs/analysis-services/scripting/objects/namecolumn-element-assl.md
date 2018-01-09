---
title: "NameColumn 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NameColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NameColumn
helpviewer_keywords: NameColumn element
ms.assetid: 9ff79f2e-26d7-4ab9-a166-14c2c2d1fc07
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2440e8e9456121c0da6d57f6498933c6eb6d53cd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="namecolumn-element-assl"></a>NameColumn 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]标识提供父元素的名称的列。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <NameColumn xsi:type="DataItem">...</NameColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|默认值|请参阅下表。|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
|祖先或父级|默认值|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|不定（请参阅“备注”）|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|InclusionThresholdSetting|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 如果[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)集合**DimensionAttribute**包含单个[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)元素表示与字符串数据类型相同的键列**DataItem**值用作默认值**NameColumn**元素。  
  
 有关详细信息**DataItem**类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表**DataItem**类型，请参阅[DataItem 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 对应的父级的元素**NameColumn**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
