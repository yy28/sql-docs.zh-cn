---
title: 查询处理事件类别 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a94b3198-be85-4935-845d-1cd4e121fc94
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ee6ef696f26397c3b4ca7656710d666d6e1941d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261483"
---
# <a name="query-processing-events-category"></a>查询处理事件类别
  “查询处理”事件类别包含下表中说明的各事件类：  
  
|**Event Class**|**事件 ID**|**Description**|  
|---------------------|------------------|---------------------|  
|查询子多维数据集|11|查询子多维数据集，用于基于使用情况的优化。|  
|查询子多维数据集详情|12|查询子多维数据集的详细信息。 此事件在启用时可能会对性能产生负面影响。|  
|从聚合获取数据|60|通过从聚合获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|从缓存获取数据|61|通过从某个缓存获取数据答复查询。 此事件在启用时可能会对性能产生负面影响。|  
|查询多维数据集开始|70|收集从开始跟踪后发生的所有查询多维数据集开始事件。|  
|查询多维数据集结束|71|收集从开始跟踪后发生的所有查询多维数据集结束事件。|  
|计算非空开始|72|计算非空开始。|  
|计算非空当前|73|计算非空当前。|  
|计算非空结束|74|计算非空结束。|  
|序列化结果开始|75|序列化结果开始。|  
|序列化结果当前|76|序列化结果当前。|  
|序列化结果结束|77|序列化结果结束。|  
|执行 MDX 脚本开始|78|执行 MDX 脚本开始。|  
|执行 MDX 脚本当前|79|执行 MDX 脚本当前。|  
|执行 MDX 脚本结束|80|执行 MDX 脚本结束。|  
|查询维度|81|查询维度。|  
|VertiPaq SE 查询开始|82|VertiPaq SE 查询|  
|VertiPaq SE 查询结束|83|VertiPaq SE 查询|  
  
 有关与每个“查询处理”事件类关联的列的信息，请参阅 [Query Processing Events Data Columns](query-processing-events-data-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 跟踪事件](analysis-services-trace-events.md)  
  
  
