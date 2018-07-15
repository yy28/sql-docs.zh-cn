---
title: AggregationPrefix 元素 (ASSL) |Microsoft Docs
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
- AggregationPrefix Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7f7fe7ad16c8949116edb13c7d2c9b5144443dd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293277"
---
# <a name="aggregationprefix-element-assl"></a>AggregationPrefix 元素 (ASSL)
  定义整个关联父元素中聚合名称所用的通用前缀。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
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
|父元素|[多维数据集](../objects/cube-element-assl.md)，[数据库](../objects/database-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 聚合前缀生成中的聚合名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，并在聚合存储在关系 OLAP (ROLAP) 分区中的关系数据库中生成表名称。  
  
 一个完全展开的聚合名称包含以下部分：  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 聚合名称的前 4 个部分组成聚合前缀。 这前 4 个部分由用户提供：  
  
-   *DatabasePrefix*表示的值`AggregationPrefix`元素与关联`Database`元素。  
  
-   *CubePrefix*表示的值`AggregationPrefix`元素与关联`Cube`元素。  
  
-   *MeasureGroupPrefix*表示的值`AggregationPrefix`元素与关联`MeasureGroup`元素。  
  
-   *PartitionPrefix*表示的值`AggregationPrefix`元素与关联`Partition`元素。  
  
 该名称，第 5 部分*AggregationID*，是系统定义的 ID，用户可以不控制此名称的一部分。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `AggregationPrefix` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
