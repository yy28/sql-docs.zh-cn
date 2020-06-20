---
title: SQL Server，数据库副本 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c8830ae30ad3514e107b718f9a02fef873e20295
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038778"
---
# <a name="sql-server-database-replica"></a>SQL Server，数据库副本
  **SQLServer:Database Replica** 性能对象包含的性能计数器报告有关 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中 AlwaysOn 可用性组的辅助数据库的信息。 此对象仅在承载辅助副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上有效。  
  
|计数器名称|说明|有关视图…|  
|------------------|-----------------|--------------|  
|**File Bytes Received/sec**|辅助副本在最后一秒为辅助数据库接收的 FILESTREAM 数据量。|辅助副本|  
|**Log Bytes Received/sec**|辅助副本在最后一秒为数据库接收的日志记录量。|辅助副本|  
|**Log remaining for undo**|为完成撤消阶段尚剩余的日志量 (KB)。|辅助副本|  
|**Log Send Queue**|主数据库的日志文件中尚未发送到辅助副本的日志记录量 (KB)。 此值从主副本发送到辅助副本。 队列大小不包括发送到辅助副本的 FILESTREAM 文件。|辅助副本|  
|**Mirrored Write Transaction/sec**|在最后一秒钟内写入主数据库，然后等待提交直到将日志发送到辅助数据库的事务数。|主副本|  
|**恢复队列**|辅助副本的日志文件中尚未重做的日志记录量。|辅助副本|  
|**Redo blocked/sec**|被数据库读取器持有的锁阻塞的重做线程数。|辅助副本|  
|**Redo Bytes Remaining**|为完成恢复阶段而要重做的剩余的日志量 (KB)。|辅助副本|  
|**Redone Bytes/sec**|在最后一秒在辅助数据库上重做的日志记录量。|辅助副本|  
|**Total Log requiring undo**|必须撤消的日志总字节数 (KB)。|辅助副本|  
|**Transaction Delay**|等待未终止的提交确认的延迟时间（毫秒）。|主副本|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况 &#40;系统监视器&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server，可用性副本](sql-server-availability-replica.md)   
 [SQL Server，数据库对象](sql-server-databases-object.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
