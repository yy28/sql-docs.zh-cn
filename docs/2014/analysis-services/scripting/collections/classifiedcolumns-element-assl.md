---
title: ClassifiedColumns 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ClassifiedColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClassifiedColumns
helpviewer_keywords:
- ClassifiedColumns element
ms.assetid: f16b4f51-c38d-4601-98b8-1497dbf12d02
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 95c00f4863223caaacfb7cc7554ec9b48a82922d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028224"
---
# <a name="classifiedcolumns-element-assl"></a>ClassifiedColumns 元素 (ASSL)
  包含被归类的相关列的集合[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructureColumn xsi:type="ScalarMiningStructureColumn">  
   ...  
   <ClassifiedColumns>  
      <ClassifiedColumnID>...</ClassifiedColumnID>  
   </ClassifiedColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)类型的[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|[ClassifiedColumnID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`ClassifiedColumns`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [MiningStructureColumn 数据类型&#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  