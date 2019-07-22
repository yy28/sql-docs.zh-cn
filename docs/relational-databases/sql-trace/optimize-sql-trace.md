---
title: 优化 SQL 跟踪 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 59b1a599a38e31abeee677059d5a99842e76d807
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033225"
---
# <a name="optimize-sql-trace"></a>优化 SQL 跟踪
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  尽管运行 SQL 跟踪会导致性能损失（因为它使用系统资源收集数据），但是您可以通过多种方法将性能损失降到最低。 若要将跟踪引起的性能损失降到最低，可以尝试下列解决方法：  
  
-   请考虑使用命令提示运行跟踪。 使用图形用户界面会影响性能。 有关详细信息，请参阅 [sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)。  
  
-   避免包含频繁发生的事件。 如果可能，通过特定事件类和筛选器来缩小跟踪范围。 收集的跟踪事件越少，支持跟踪所需的系统资源就越少。  
  
-   集中跟踪以仅收集提供相关数据的事件。 例如，如果您的跟踪用于标识死锁，则包括 **Lock:Deadlock** 事件类，而不包括 **Lock:Acquired** 事件类。 如果同时包括这两个事件类，则跟踪将必须响应获取的每个锁，执行成本将加倍。  
  
-   避免收集重复数据。 例如，如果收集 **SQL:BatchStarted** 和 **SQL:BatchCompleted**，则可以通过仅收集 **SQL:BatchStarted** 事件类的文本数据来最小化结果集的大小。  
  
-   在跟踪定义中使用筛选器。 例如，如果您知道某个用户在即席查询期间报告较慢性能，则对 **LoginName**创建筛选器。 将筛选器设置为仅包含 **LoginName** 与该用户名匹配的事件。  
  
 如果需要跟踪对性能产生极大影响的事件，请考虑使用下列一种方法来限制对服务器性能的影响：  
  
-   短时间运行跟踪。 您可以通过启用停止时间来控制跟踪运行的时间长度。 这在您无法限制事件类或筛选事件的情况下非常重要。 启用停止时间可以确保性能不会无限期地受到影响。  
  
-   限制跟踪结果的大小。 您可以将跟踪结果的大小限制为最大文件大小。 此策略可以确保在达到文件大小限制时停止性能损失（如果未启用文件滚动更新）。  
  
-   限制返回的事件数。 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，可以通过将跟踪保存到表并设置最大行数来限制返回的事件数。 达到最大行数后，跟踪结果仍会返回到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 屏幕，但不再有将结果记录到表的开销。  
  
## <a name="see-also"></a>另请参阅  
 [筛选跟踪](../../relational-databases/sql-trace/filter-a-trace.md)  
  
  
