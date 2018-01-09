---
title: "主动缓存 （分区） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- hybrid OLAP
- partitions [Analysis Services], proactive caching
- relational OLAP
- multidimensional OLAP
- MOLAP
- proactive caching [Analysis Services]
- ROLAP
- cache [Analysis Services]
ms.assetid: 422660b2-4d80-4165-b1c9-3963bcde556b
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 25a6306e19f6eff72f84fffde0372ed0bc3d76e6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="partitions---proactive-caching"></a>分区的主动缓存
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]主动缓存可自动创建 MOLAP 缓存和 OLAP 对象的管理。 多维数据集可利用收自数据库的通知，立即合并对数据库中数据所做的更改。 主动缓存的目标是提供传统 MOLAP 所具有的性能，并同时保持使用 ROLAP 进行管理所具有的方便和快捷。  
  
 简单 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象由计时规范和表通知组成。 计时规范定义收到更改通知后更新缓存的时间范围。 表通知定义数据表和 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象之间的通知架构。  
  
 多维 OLAP (MOLAP) 存储提供最佳的查询响应，但是其不足之处是存在一些数据滞后时间。 实时关系 OLAP (ROLAP) 存储可使用户迅速浏览数据源中的最新更改，但是不足之处是较多维 OLAP (MOLAP) 存储的性能相差甚远，这是因为没有对数据进行预计算汇总，并且关系存储没有针对 OLAP 样式的查询进行优化。 如果用户需要在您的应用程序中查看最新数据，而您也希望利用 MOLAP 存储的性能优点，则 SQL Server Analysis Services 提供的主动缓存选项可满足这些应用需求，尤其是与分区组合使用时，更是如此。 主动缓存按分区和维度来设置。 主动缓存选项使得能够在 MOLAP 存储的增强性能和 ROLAP 存储的即时性之间达成平衡，并且还在基础数据更改时提供自动的分区处理或者按照设置计划进行处理。  
  
## <a name="proactive-caching-configuration-options"></a>主动缓存配置选项  
 SQL Server Analysis Services 提供了多个主动缓存配置选项，您可以利用它们来最大化性能，最小化滞后时间以及安排处理。 主动缓存功能可以简化管理数据过时的进程。 主动缓存设置确定多维 OLAP 结构（也称为 MOLAP 缓存）重新生成的频率，是否在重新生成缓存时对过时的 MOLAP 存储或基础 ROLAP 数据源进行查询，以及缓存是按计划重新生成还是根据数据库中的更改重新生成。  
  
### <a name="minimizing-latency"></a>最小化延迟  
 将主动缓存设置为最小化滞后时间之后，用户会对 ROLAP 存储或 MOLAP 存储执行 OLAP 对象查询，具体取决于数据是否发生了最新更改以及主动缓存的配置方式。 查询引擎会将查询导向 MOLAP 存储中的源数据，直至数据源发生更改为止。 若要最小化滞后时间，数据源发生更改后，可以删除已缓存的 MOLAP 对象，并当 MOLAP 对象在缓存中重新生成期间将查询切换到 ROLAP 存储。 在 MOLAP 对象重新生成和处理完毕之后，查询会自动切换到 MOLAP 存储。 对于小分区（例如当前分区）而言，缓存的刷新速度非常快，仅在当天便可进行刷新。  
  
### <a name="maximizing-performance"></a>最大化性能  
 若要最大化性能同时缩短滞留时间，还可以使用缓存，而无需删除当前 MOLAP 对象。 然后，在数据读入新缓存并在其中处理时，继续对 MOLAP 对象进行查询。 该方法可提供更好的性能，但是会导致在生成新缓存时查询返回旧数据。  
  
## <a name="see-also"></a>另请参阅  
 [维度存储](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [设置分区存储（Analysis Services - 多维）](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
