---
title: "列分布（数据挖掘） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "正态分布类型 [数据挖掘]"
  - "均匀分布类型 [数据挖掘]"
  - "列 [数据挖掘], 分布"
  - "日志正态分布类型 [数据挖掘]"
  - "连续列"
  - "分发 [数据挖掘]"
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# 列分布（数据挖掘）
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以定义挖掘结构中的列分布以影响在创建挖掘模型时算法如何处理这些列中的数据。 对于某些算法，如果已知列中包含常用的值分布，则在处理模型之前定义任意连续列的分布将非常有用。 如果不定义分布，则由于算法据以解释数据的信息较少，生成的挖掘模型产生的预测可能不如定义了分布时产生的预测精确。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中可用的算法支持下列分布类型：  
  
 **Normal**  
 连续列的值构成一个正态分布直方图。  
  
 ![具有正态分布的直方图](../../analysis-services/data-mining/media/normal-distribution.png "具有正态分布的直方图")  
  
 **Log Normal**  
 连续列的值构成一个直方图，其曲线在较高端延长并向较低端倾斜。  
  
 ![具有日志正态分布的直方图](../../analysis-services/data-mining/media/log-normal-distribution.png "具有日志正态分布的直方图")  
  
 **Uniform**  
 连续列的值构成平坦曲线，曲线上的所有值都具有相同概率。  
  
 ![具有均匀分布的直方图](../../analysis-services/data-mining/media/uniform-distribution.png "具有均匀分布的直方图")  
  
 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的算法的详细信息，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
## 另请参阅  
 [内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)   
 [挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [离散化方法（数据挖掘）](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [分布 (DMX)](../../dmx/distributions-dmx.md)   
 [挖掘结构列](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  