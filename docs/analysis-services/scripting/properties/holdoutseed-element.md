---
title: "HoldoutSeed 元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HoldoutSeed
helpviewer_keywords: HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c018e11960726554b2f02a0ec7aaa537d599a6d0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="holdoutseed-element"></a>HoldoutSeed 元素
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]指定包含的测试集的可重复维持分区的种子[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。 此种子可确保模型内容在处理过程中保持不变。 如果未指定或设置为 0，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]创建挖掘结构名称使用哈希算法的种子。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|0|  
|基数|0-1：可出现一次并仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 首次创建挖掘结构时，ID 和名称是相同的。 但是，您可以更改挖掘结构的名称。 因此，若要确保分区可重复使用，则不应依赖基于名称创建的种子，而应对种子进行显式设置。  
  
 此外，当你创建挖掘结构的副本使用**导出**语句，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将保留新的挖掘结构的名称，但将自动生成新的 id。 因此，两个挖掘结构可以共享相同的名称但具有不同的 ID。 任何两个名称相同的挖掘结构都将具有相同的种子。 但是，由于数据的分区还依赖于源数据，因此每个结构中分区的实际内容可能不同。  
  
 新属性**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**仅在中可用[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]及更高版本。 因此，你必须对语法说明中所示前缀这些属性与新的命名空间或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将返回错误。  
  
 **请注意**中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]挖掘结构不支持使用维持分区。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含维持参数的脚本语言 (ASSL) 语句**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**不能在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中将这些维持参数之一用于 ASSL 语句，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
 对应于的父元素**HoldoutSeed**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutActualSize 元素](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutMaxCases 元素](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)  
  
  
