---
title: 确定轮询频率-分析平台系统 |Microsoft Docs
description: 本文介绍如何确定分析平台系统 appliance 警报的轮询频率。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2d305c766801ce27268e2d3bc873d9c361c034f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961074"
---
# <a name="determine-polling-frequency"></a>确定轮询频率
本文介绍如何确定分析平台系统 appliance 警报的轮询频率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要确定轮询频率  
由于 PDW 当前不支持主动通知，出现警报时，监视解决方案需要连续轮询设备 Dll。  在内部，PDW 在不同的时间间隔轮询组件：  
  
-   群集-60 秒  
  
-   检测信号-60 秒  
  
-   所有其他组件-五分钟  
  
-   性能计数器-三秒  
  
是一个常见的间隔来轮询对于警报，也使用由 System Center，该**每隔 15 分钟**。  很明显，则可以查询多或较少，但不是建议以轮询小于每 6 小时。  
  
更频繁地轮询是可以接受的但过于频繁地轮询混乱不堪[sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV。  过于频繁地轮询可以使其很难有关用户诊断查询性能问题时其快速将滚动出视野之外。  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备监视&#40;分析平台系统&#41;](appliance-monitoring.md)  
  
