---
title: SQL Server，数据库副本 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 78c54b8864b5dae4171ac5b8a1a13c08ff73482e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709905"
---
# <a name="sql-server-database-replica"></a>SQL Server，数据库副本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Database Replica** 性能对象包含的性能计数器报告有关 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中 Always On 可用性组的辅助数据库的信息。 此对象仅在承载辅助副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上有效。  
  
|计数器名称|描述|有关视图…|  
|------------------|-----------------|--------------|  
|**File Bytes Received/sec**|辅助副本在最后一秒为辅助数据库接收的 FILESTREAM 数据量。|辅助副本|  
|**Log Apply Pending Queue**|正在等待应用于数据库副本的日志块数。|辅助副本|
|**Log Apply Ready Queue**|正在等待且已准备好应用于数据库副本的日志块数。|辅助副本| 
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
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server，可用性副本](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server，Databases 对象](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
