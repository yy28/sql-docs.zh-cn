---
title: AggregationPrefix 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b23721728f8e196c47ab326024a6f514631c3b6f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationprefix-element-assl"></a>AggregationPrefix 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 聚合前缀生成中的聚合名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，并且还在聚合存储在关系 OLAP (ROLAP) 分区中的关系数据库中生成表名称。  
  
 一个完全展开的聚合名称包含以下部分：  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 聚合名称的前 4 个部分组成聚合前缀。 这前 4 个部分由用户提供：  
  
-   *DatabasePrefix*表示的值**AggregationPrefix**元素与关联**数据库**元素。  
  
-   *CubePrefix*表示的值**AggregationPrefix**元素与关联**多维数据集**元素。  
  
-   *MeasureGroupPrefix*表示的值**AggregationPrefix**元素与关联**MeasureGroup**元素。  
  
-   *PartitionPrefix*表示的值**AggregationPrefix**元素与关联**分区**元素。  
  
 第五个部分名称， *AggregationID*，是系统定义的 ID，并且用户必须不能控制此名称的一部分。  
  
 对应的父级的元素**AggregationPrefix**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
