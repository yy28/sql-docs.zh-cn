---
title: "已分类列（数据挖掘） | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "内容类型 [数据挖掘]"
  - "STDEV 列"
  - "VARIANCE 列"
  - "PROBABLILITY 列"
  - "PROBABILITY_STDEV 列"
  - "列 [数据挖掘], 已分类"
  - "已分类列 [数据挖掘]"
  - "PROBABILITY_VARIANCE 列"
  - "SUPPORT 列"
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 26
---
# 已分类列（数据挖掘）
  定义已分类列时，在挖掘结构中创建当前列和另一个列之间的关系。 指定为已分类列的挖掘结构列中的数据包含描述挖掘结构中另一个列的值的分类信息。  
  
 例如，假定有两个包含数值数据的列：其中 [Yearly Purchases] 列包含特定日历年每个客户每年的总购买量，[Standard Deviations] 列则包含这些值的标准偏差。 在此例中，可以指定 [Yearly Purchases] 列为已分类列，模型将在分析中使用此关系。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的算法不支持使用已分类列，此功能用于创建自定义算法中。  
  
## 定义已分类列  
 已分类列的数据类型必须为 **Long** 或 **Double**。  
  
 以下列表说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持的已分类列内容类型。  
  
 **PROBABILITY**  
 列内的值是相关值的概率，是介于 0 和 1 之间的数字。  
  
 **VARIANCE**  
 列内的值是相关值的方差。  
  
 **STDEV**  
 列内的值是相关值的标准偏差。  
  
 **PROBABILITY_VARIANCE**  
 列内的值是相关值概率的方差。  
  
 **PROBABILITY_STDEV**  
 列内的值是相关值概率的标准偏差。  
  
 **Support**  
 列内的值是相关值的权重或事例复制因子。  
  
## 另请参阅  
 [内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)   
 [挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [数据类型（数据挖掘）](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  