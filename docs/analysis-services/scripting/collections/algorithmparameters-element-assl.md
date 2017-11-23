---
title: "AlgorithmParameters 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AlgorithmParameters Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AlgorithmParameters
helpviewer_keywords: AlgorithmParameters element
ms.assetid: 240cbb60-7fa3-46ef-b5be-cd14c9ec10de
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1470ce42b2dada9d96c61e34716800b71fb63f26
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="algorithmparameters-element-assl"></a>AlgorithmParameters 元素 (ASSL)
  包含的使用的算法的参数集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel>  
   ...  
   <AlgorithmParameters>  
      <AlgorithmParameter>...</AlgorithmParameter>  
   </AlgorithmParameters>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|子元素|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 **AlgorithmParameters**集合包含一组可扩展的参数，表示为名称/值对，挖掘模型算法。 适用的参数集依赖于算法。 有关给定算法的算法参数的详细信息，请参阅该算法的相应文档。  
  
 可用算法参数（包括验证和显示信息）可从 DMSCHEMA_MINING_SERVICE_PARAMETERS 架构行集中检索。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [算法元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [DMSCHEMA_MINING_SERVICE_PARAMETERS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
