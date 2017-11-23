---
title: "确定轮询频率 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: "7"
ms.openlocfilehash: fb32abc38a90cd7450dc310a9f73eb7a5d72b5fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="determine-polling-frequency"></a>确定轮询频率
本主题说明如何确定 SQL Server PDW 设备警报的轮询频率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要确定轮询频率  
由于 PDW 当前不支持主动通知，发生警报时，需要持续轮询设备 Dll 的监视解决方案。  在内部，PDW 在不同的时间间隔轮询组件：  
  
-   群集-60 秒  
  
-   检测信号-60 秒  
  
-   所有其他组件 – 5 分钟  
  
-   性能计数器 – 3 秒  
  
一个常见的间隔轮询警报，也使用由 System Center，该是**每隔 15 分钟**。  显然，你可以更多或更少经常查询，但不是建议轮询小于每 6 小时。  
  
更频繁地轮询可以接受，但过于频繁地轮询混乱不堪[sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV。  这可以使难以用户以诊断查询性能问题，如果存在查询快速将滚动出视野。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备监视 &#40;分析平台系统 &#41;](appliance-monitoring.md)  
  
