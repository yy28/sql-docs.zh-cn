---
title: SQL Server - ExecStatistics 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a09c2a57b76974758626a1847d5f0df3f8b7f55c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777779"
---
# <a name="sql-server-execstatistics-object"></a>SQL Server ExecStatistics 对象
  Microsoft SQL Server 中的 **SQLServer:ExecStatistics** 对象提供了用于监视各种执行的计数器。  
  
 下表介绍了 SQL Server **Exec Statistics** 计数器。  
  
|SQL Server Exec Statistics 计数器|Description|  
|-----------------------------------------|-----------------|  
|**Distributed Query**|与执行分布式查询相关的统计信息。|  
|**DTC calls**|与执行 DTC 调用相关的统计信息。|  
|**Extended Procedures**|与执行扩展过程相关的统计信息。|  
|**OLEDB calls**|与执行 OLEDB 调用相关的统计信息。|  
  
 对象中的每个计数器均包含以下实例：  
  
|项|Description|  
|----------|-----------------|  
|**平均执行时间 (ms)**|所选执行类型的平均执行时间。|  
|**每秒的累积执行时间 (ms)**|所选执行类型每秒的累积执行时间。|  
|**正在进行的执行数**|正在进行的所选执行类型的执行数。|  
|**每秒启动的执行数**|每秒启动的所选执行类型的执行数。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
