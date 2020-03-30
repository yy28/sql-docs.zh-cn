---
title: SQL Server - Memory Broker Clerk 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fff8aa7a2e37f66470798b2772ed00d0298708a3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68093413"
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server，Memory Broker Clerk 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**SQLServer：Memory Broker Clerk** 性能对象提供与 Memory Broker Clerk 相关的统计信息的计数器。

下表介绍了 SQL Server **Memory Broker Clerk** 性能对象。

|**SQL Server Memory Broker Clerk 计数器**|说明|  
|-------------|-----------------|  
|**内部优势**|条目计数压力的内部内存值（毫秒/页/毫秒，乘以 100 亿并截断为整数）。|
|**Memory Broker Clerk 大小**|Clerk 的大小（页数）。|
|**定期逐出（页数）**|上一次定期逐出从 Broker Clerk 中逐出的页数。|
|**压力逐出（页数/秒）**|内存压力从 Broker Clerk 中每秒逐出的页数。|
|**模拟优势**|分配给 Clerk 的内存值（毫秒/页/毫秒，乘以 100 亿并截断为整数）。|
|**模拟大小**|Clerk 模拟的当前大小（页数）。|

有一个缓冲池和列存储对象池的计数器实例。

## <a name="see-also"></a>另请参阅  
[监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
