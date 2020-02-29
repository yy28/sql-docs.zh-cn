---
title: 列分布（数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c7eab32f251b9622c6ac77febf2c004806c024b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174537"
---
# <a name="column-distributions-data-mining"></a>列分布（数据挖掘）
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以在挖掘结构中定义列分布，以影响在创建挖掘模型时算法如何处理这些列中的数据。 对于某些算法，如果已知列中包含常用的值分布，则在处理模型之前定义任意连续列的分布将非常有用。 如果不定义分布，则由于算法据以解释数据的信息较少，生成的挖掘模型产生的预测可能不如定义了分布时产生的预测精确。

 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中可用的算法支持下列分布类型：

 `Normal`连续列的值构成具有正态分布的直方图。

 ![具有正态分布的直方图](../media/normal-distribution.gif "具有正态分布的直方图")

 `Log Normal`连续列的值构成一个直方图，其中曲线在高端高端延长，并沿低端向下倾斜。

 ![具有日志正态分布的直方图](../media/log-normal-distribution.gif "具有日志正态分布的直方图")

 `Uniform`连续列的值构成平面曲线，其中所有值都有可能出现。

 ![具有均匀分布的直方图](../media/uniform-distribution.gif "具有均匀分布的直方图")

 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的算法的详细信息，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)。

## <a name="see-also"></a>另请参阅
 [&#40;数据挖掘&#41;](content-types-data-mining.md) [挖掘结构的内容类型 &#40;Analysis Services 数据挖掘&#41;](mining-structures-analysis-services-data-mining.md) [离散化方法 &#40;数据挖掘&#41;](discretization-methods-data-mining.md)分布式 &#40;[DMX](/sql/dmx/distributions-dmx)&#41;[挖掘结构列](mining-structure-columns.md)


