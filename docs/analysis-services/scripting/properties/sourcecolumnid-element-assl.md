---
title: SourceColumnID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 247c00954b5922a5bbaaabb0e33b388d3a8041fb
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="sourcecolumnid-element-assl"></a>SourceColumnID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含在祖先的源挖掘结构列的标识符 (ID) [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <SourceColumnID>...</SourceColumnID>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**SourceColumnID**元素与中的挖掘结构列的标识符匹配[列](../../../analysis-services/scripting/collections/columns-element-assl.md)的父集合**MiningStructure**。  
  
 对应于的父元素**SourceColumnID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningModelColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
