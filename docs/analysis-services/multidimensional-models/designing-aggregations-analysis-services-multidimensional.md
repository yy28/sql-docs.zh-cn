---
title: "设计聚合 (Analysis Services-多维) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- aggregations [Analysis Services], partitions
- partitions [Analysis Services], aggregations
ms.assetid: 3072b7e0-6961-42ad-a287-16f391f2cec4
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 71e50fc874562cceddc91b454a246b29370cf7c7
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>设计聚合（Analysis Services - 多维）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
聚合是预先计算的多维数据集数据的汇总，可帮助启用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以提供快速的查询响应。  
  
 若要为分区设置存储选项和设计聚合，请使用聚合设计向导。 由于向导每次可针对一个度量值组的一个分区进行操作，所以可以为每个分区选择不同的选项和设计。 向导将引导您完成为分区配置存储和设计聚合的各个步骤。 有关配置存储的详细信息，请参阅。  
  
 先选择一种方法控制向导所要设计的聚合数目，然后让向导自己设计聚合。  
  
 目标是设计最优数目的聚合。 该数目不仅能提供快速的响应时间，还能防止分区过大。 聚合的数目越多，响应时间就越快，但所需要的存储空间也就越大，计算所需的时间可能也会更长。 此外，随着该向导设计越来越多的聚合，早期的聚合比后来的聚合会产生更大的性能提升。 减少用处不大的聚合也能够提高性能。 通过以下向导中可用的方法之一，您可以控制向导设计的聚合数目：  
  
-   为聚合指定存储空间限制。  
  
-   指定性能提升的极限。  
  
-   当显示的“性能与大小”曲线开始稳定在一个可接受的性能提升高度上时，手动停止向导。  
  
-   选择不设计聚合。  
  
 若要设计存储，向导必须能够连接到目标服务器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 未在目标服务器上运行，或者存储设计进程无法连接到目标服务器，向导将显示错误消息。  
  
 向导的最后一步允许处理或推迟处理。 处理创建使用向导设计的聚合，而推迟处理则保存所设计的聚合以供将来进行处理，从而使设计活动不必处理就可以继续。 根据分区大小的不同，处理过程可能会需要相当长的一段时间。 根据您的选择，可以中断对分区的处理。  
  
## <a name="see-also"></a>另请参阅  
 [聚合和聚合设计](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
