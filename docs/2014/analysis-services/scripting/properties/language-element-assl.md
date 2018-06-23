---
title: 语言元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LANGUAGE
helpviewer_keywords:
- Language element
ms.assetid: 4d745d23-6b1f-4a85-97cf-d034cc41356f
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 09a51320df0cf5d4246fbc14307f488c2d754e3c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129774"
---
# <a name="language-element-assl"></a>Language 元素 (ASSL)
  包含父元素的语言标识符。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Database, Dimension, MiningModel, MiningStructure, Translation -->  
   ...  
   <Language>...</Language>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|InclusionThresholdSetting|  
  
 **基数**  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[转换](../objects/translation-element-assl.md)|1-1：出现一次且仅出现一次的必需元素。|  
|其他|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../objects/cube-element-assl.md)，[数据库](../objects/database-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[转换](../objects/translation-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Language` 元素包含父元素使用的默认语言标识符或 `Translation` 元素的特定语言标识符。 该语言应该通过使用区域设置标识符 (LCID) 代码进行定义。 例如，LCID 1033 用于表示英语（美国）语言。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Language` 元素的父级对应的元素为 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MiningModel>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  