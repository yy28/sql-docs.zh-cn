---
title: FoldingParameters 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords:
- FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f7f32684686f7b8f12bb147bb4f6b7ea87537e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117408"
---
# <a name="foldingparameters-element-assl"></a>FoldingParameters 元素 (ASSL)
  指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器在执行挖掘模型的交叉验证时使用的参数。  
  
> [!NOTE]  
>  这些参数仅供内部使用。 此处提供的信息仅供参考。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|*FoldIndex*|整数，指示用于交叉验证的分区的起始位置。|  
|*FoldCount*|整数，指示交叉验证后模型中分区的个数。|  
|*MaxCases*|整数，指示有多少模型事例用于交叉验证。<br /><br /> 值为 0，指示将使用所有事例。|  
|*FoldTargetAttribute*|字符串，指示包含可预测属性的模型列的 ID。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>备注  
 这些属性仅用于内部使用，不支持在 DDL 语句中使用。  
  
 有关如何使用交叉验证中的信息[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]，请参阅[交叉验证报表中的度量值](../../data-mining/measures-in-the-cross-validation-report.md)。  
  
 有关如何使用来执行交叉验证的信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]存储的过程，请参阅[数据挖掘存储过程&#40;Analysis Services-数据挖掘&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
