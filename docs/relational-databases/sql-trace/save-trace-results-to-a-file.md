---
title: 将跟踪结果保存到文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 168c3e17cbf01b4a4c85d4374b716d0bbf3b4f59
ms.sourcegitcommit: ddb682c0061c2a040970ea88c051859330b8ac00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51570467"
---
# <a name="save-trace-results-to-a-file"></a>将跟踪结果保存到文件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以将跟踪结果保存到文件中。 跟踪文件是写入跟踪结果的文件。 跟踪文件可以位于本地目录（如 C:\\foldername\\filename.trc）中，也可以位于在网络目录（如 \\\computername\sharename\filename.trc）中。  
  
 可以使用跟踪文件执行下列操作：  
  
-   重播跟踪  
  
-   审核 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   进行性能分析  
  
-   将跟踪事件与性能计数器关联以增强问题检测能力  
  
-   执行数据库引擎优化顾问分析  
  
-   执行查询优化  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为存储过程 **@tracefile** 的 **@tracefile**参数指定路径和文件名后，将跟踪结果保存到文件中。  
  
> [!NOTE]  
>  如果为存储过程 **sp_trace_create** 指定路径用来保存跟踪文件，则服务器必须可以访问该目录。 同时注意，如果为 **sp_trace_create**指定本地目录，则该目录应是服务器上的本地目录。  
  
 如果使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，则可以将跟踪结果保存到文件或表中。 将跟踪结果保存到表中后，可以与将跟踪保存到文件中后一样进行访问，另外还可以查询表以搜索特定事件。  
  
 有关保存跟踪结果的详细信息，请参阅 [将跟踪结果保存到表 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) 和 [将跟踪结果保存到文件 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [创建跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
