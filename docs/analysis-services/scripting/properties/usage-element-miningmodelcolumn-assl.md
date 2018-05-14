---
title: 使用情况元素 (MiningModelColumn) (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fbe265861a16e28e9244261a26a253f78adc9dba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage 元素 (MiningModelColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述如何关联的列的父代中[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)使用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Key*|该列为键列。|  
|*输入*|该列为输入列。|  
|*Predict*|该列为预测列。|  
|*PredictOnly*|该列仅为预测列。|  
|*InclusionThresholdSetting*|模型不使用该列。<br /><br /> **\*\* 警告\* \*** 时使用的值为"None"，Analysis Services 不任何将值发送到服务器默认情况下; 因此，使用情况属性不包含在请求/响应。|  
  
 对应于的允许值为枚举**用法**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningModelColumnUsages>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
