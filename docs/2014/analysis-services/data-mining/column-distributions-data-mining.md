---
title: 列分布 （数据挖掘） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5170f490f6e6940b2d5bf4d8f7de7880f88d2e7e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014920"
---
# <a name="column-distributions-data-mining"></a>列分布（数据挖掘）
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以定义挖掘结构中的列分布以影响在创建挖掘模型时算法如何处理这些列中的数据。 对于某些算法，如果已知列中包含常用的值分布，则在处理模型之前定义任意连续列的分布将非常有用。 如果不定义分布，则由于算法据以解释数据的信息较少，生成的挖掘模型产生的预测可能不如定义了分布时产生的预测精确。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中可用的算法支持下列分布类型：  
  
 `Normal`  
 连续列的值构成一个正态分布直方图。  
  
 ![与正态的分布的直方图](../media/normal-distribution.gif "正态分布直方图")  
  
 `Log Normal`  
 连续列的值构成一个直方图，其曲线在较高端延长并向较低端倾斜。  
  
 ![具有日志正态分布的直方图](../media/log-normal-distribution.gif "与对数正态分布的直方图")  
  
 `Uniform`  
 连续列的值构成平坦曲线，曲线上的所有值都具有相同概率。  
  
 ![使用均匀分布的直方图](../media/uniform-distribution.gif "使用均匀分布的直方图")  
  
 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的算法的详细信息，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 [内容类型&#40;数据挖掘&#41;](content-types-data-mining.md)   
 [挖掘结构&#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [离散化方法&#40;数据挖掘&#41;](discretization-methods-data-mining.md)   
 [分发&#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [挖掘结构列](mining-structure-columns.md)  
  
  
