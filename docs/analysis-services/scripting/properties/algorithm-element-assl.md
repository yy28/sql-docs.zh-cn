---
title: "算法元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Algorithm Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Algorithm
helpviewer_keywords: Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7ad1fed7c000a978c096692fa4f4c59d655132e9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="algorithm-element-assl"></a>Algorithm 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义使用的算法[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值**算法**元素是一个字符串，标识的算法。 例如，可以是字符串*Microsoft_Naive_Bayes*， *Microsoft_Decision_Trees*，或*Microsoft_Clustering。* 字符串可标识由提供的算法[!INCLUDE[msCoName](../../../includes/msconame-md.md)]和自定义算法的用户提供的。 可用值**算法**元素可以从 SERVICE_NAME 列中检索[DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)架构行集。  
  
 对应于的父元素**算法**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningModel>。 在 AMO 对象模型中，紧密相关的元素为 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>。  
  
## <a name="see-also"></a>另请参阅  
 [AlgorithmParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
