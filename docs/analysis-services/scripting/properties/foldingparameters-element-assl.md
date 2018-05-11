---
title: FoldingParameters 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f3c631844a71ff43d84c76ba2104a211b7aea039
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="foldingparameters-element-assl"></a>FoldingParameters 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|父元素|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|子元素|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>注释  
 这些属性仅用于内部使用，不支持在 DDL 语句中使用。  
  
 有关如何使用交叉验证中[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]，请参阅[交叉验证报表中的度量值](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
 有关如何执行交叉验证的使用信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]存储的过程，请参阅[数据挖掘存储过程&#40;Analysis Services-数据挖掘&#41;](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
