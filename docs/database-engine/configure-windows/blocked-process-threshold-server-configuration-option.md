---
title: blocked process threshold 服务器配置选项 | Microsoft Docs
description: 了解如何使用阻止的进程阈值选项来指定 SQL Server 生成阻止的进程报表和发出警报的间隔。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bdd5f7d01e7271609562fb7d42126746d6163de4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725237"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>blocked process threshold 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 **blocked process threshold** 选项用于指定阈值（以秒为单位），超过该阈值将生成阻塞的进程报告。 该阈值可介于 5 到 86,400 之间。  锁监视每 5 秒钟唤醒一次来检测阻止条件（它还查找死锁等其他情况）。 因此，如果将“阻止的进程阈值”值设置为 1，将不会检测已阻止 1 秒的进程。 可以检测到阻止的进程的最短时间为 5 秒。
 
 默认情况下，不生成阻塞的进程报告。 对于系统任务或正在等待未生成可检测死锁的资源的任务，不生成该事件。  
  
 可以定义一个生成该事件时执行的 [警报](../../ssms/agent/alerts.md) 。 例如，可以选择通知管理员采取相应的操作来处理阻塞情况。  
  
 阻塞的进程阈值使用死锁监视器后台线程监视等待时间大于（或数倍于）配置的阈值的任务列表。 每个报告间隔中，为每个阻塞的任务生成一次事件。  
  
 已通过最大努力完成了阻塞的进程报告。 不保证报表的数据始终为实时数据，也不保证报表数据接近实时。  
  
 该设置立即生效，无需停止并重新启动服务器。  
  
## <a name="examples"></a>示例  
 下面的示例将 `blocked process threshold` 设置为 `20` 秒，超过该阈值将为阻塞的每个任务生成阻塞的进程报告。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Blocked Process Report 事件类](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
