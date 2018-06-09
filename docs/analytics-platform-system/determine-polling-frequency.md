---
title: 确定轮询频率-分析平台系统 |Microsoft 文档
description: 此文章介绍了如何确定 Analytics Platform System 设备警报的轮询频率。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 39597e0e4623a3006709acde7fe54f97545c362f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707615"
---
# <a name="determine-polling-frequency"></a>确定轮询频率
此文章介绍了如何确定 Analytics Platform System 设备警报的轮询频率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要确定轮询频率  
由于 PDW 当前不支持主动通知，发生警报时，需要持续轮询设备 Dll 的监视解决方案。  在内部，PDW 在不同的时间间隔轮询组件：  
  
-   群集-60 秒  
  
-   检测信号-60 秒  
  
-   所有其他组件 – 五分钟  
  
-   性能计数器 – 三秒  
  
一个常见的间隔轮询警报，也使用由 System Center，该是**每隔 15 分钟**。  显然，你可以更多或更少经常查询，但不是建议轮询小于每 6 小时。  
  
更频繁地轮询可以接受，但过于频繁地轮询混乱不堪[sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV。  过于频繁地轮询变得困难用户也需要诊断查询性能问题时其快速滚动出视野。  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备监视&#40;分析平台系统&#41;](appliance-monitoring.md)  
  
