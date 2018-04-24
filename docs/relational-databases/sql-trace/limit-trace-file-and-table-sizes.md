---
title: 限制跟踪文件和表的大小 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0ad01698894507e42835d4be11acf0b05863437
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="limit-trace-file-and-table-sizes"></a>限制跟踪文件和表的大小
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL 跟踪结果的大小依赖于跟踪中包括的事件类和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的用法。 如果跟踪经常出现的事件类，则可以通过设置最大文件大小或最大行数来最小化跟踪收集的数据量。 通过指定最大文件大小或行数，可以确保跟踪文件或表不会增长到超出指定范围。  
  
> [!NOTE]  
>  如果将跟踪数据保存到已经存在的文件，则可以向该文件追加数据或覆盖该文件。 如果选择向该文件追加数据，而此跟踪文件已经达到或超过指定的最大文件大小，则会通知您，并提示您可以增加最大文件大小或指定新文件。 对跟踪表也是如此。  
  
## <a name="maximum-file-size"></a>最大文件大小  
 指定有最大文件大小的跟踪在达到最大文件大小时，会停止将跟踪信息保存到该文件。 使用此选项可将事件分组成更小、更容易管理的文件。 此外，限制文件大小使得无人参与的跟踪运行起来更加安全，因为跟踪会在达到最大文件大小后停止。 可以为通过 Transact-SQL 存储过程或使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]创建的跟踪设置最大文件大小。  
  
 最大文件大小选项的上限为 1 GB。 默认最大文件大小为 5 MB。  
  
### <a name="enabling-file-rollover"></a>启用文件滚动更新  
 如果使用文件滚动更新选项，则在达到最大文件大小时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会关闭当前文件并创建一个新文件。 新文件与原文件同名，但是文件名后将追加一个整数以表示其序列。 例如，如果原始跟踪文件命名为 filename_1.trc，则下一跟踪文件为 filename_2.trc，依此类推。 如果指定给新滚动更新文件的名称已经被现有文件使用，则将覆盖现有文件，除非现有文件为只读文件。 将跟踪数据保存到文件时，默认情况下启用文件滚动选项。  
  
> [!NOTE]  
>  如果启用了文件滚动更新选项，则在使用其他某种方法停止跟踪之前，跟踪将一直继续。 若要停止在达到文件大小限制后进行跟踪，请禁用文件滚动更新选项。  
  
 **设置跟踪文件的最大文件大小**  
  
 [设置跟踪文件的最大文件大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>最大行数  
 指定有最大行数的跟踪在达到最大行数时，会停止将跟踪信息保存到表。 每个事件构成一行，因此该参数可设置收集的事件数的范围。 设置最大行数使得无人参与的跟踪运行起来更加方便。 例如，如果需要启动一个将跟踪数据保存到表的跟踪，同时希望在该表变得过大时停止跟踪，则可以使其自动停止。  
  
 如果已指定并且达到了最大行数，将在运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的同时继续运行跟踪，但不再记录跟踪信息。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 将继续显示跟踪结果，直到跟踪停止。  
  
 **设置跟踪的最大行数**  
  
 [设置跟踪表的最大表大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
  
