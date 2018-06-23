---
title: 排序规则元素 (ASSL) |Microsoft 文档
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
- Collation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Collation
helpviewer_keywords:
- Collation element
ms.assetid: 9b6dbe19-543e-43e6-abe9-1e8b4dfaa275
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a8d457901781b177b860fdc4592cf87a2ab99456
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125460"
---
# <a name="collation-element-assl"></a>Collation 元素 (ASSL)
  确定父元素使用的排序规则。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Collation>...</Collation>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../objects/cube-element-assl.md)，[数据库](../objects/database-element-assl.md)， [DataItem](../data-type/dataitem-data-type-assl.md)，[维度](../objects/dimension-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Collation` 字符串由以下划线字符分隔的区域设置标识符 (LCID) 和比较标志组成。 例如，Latin1_General_CI_AS。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Collation` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataItem>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MiningModel> 和 <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  