---
title: 将跟踪结果保存到文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a55662b38fbd69dc45d8f0031856ad4da5929038
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63136438"
---
# <a name="save-trace-results-to-a-file"></a>将跟踪结果保存到文件
  可以将跟踪结果保存到文件中。 跟踪文件是写入跟踪结果的文件。 跟踪文件可以位于本地目录（如 C:\\foldername  \\filename.trc  ）中，也可以位于在网络目录（如 \\\computername\sharename\filename.trc）中。  
  
 可以使用跟踪文件执行下列操作：  
  
-   重播跟踪  
  
-   审核 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   进行性能分析  
  
-   将跟踪事件与性能计数器关联以增强问题检测能力  
  
-   执行数据库引擎优化顾问分析  
  
-   执行查询优化  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果为存储过程**@tracefile** **sp_trace_create**的参数指定了路径和文件名，则会将跟踪结果保存到文件。  
  
> [!NOTE]  
>  如果为存储过程 **sp_trace_create** 指定路径用来保存跟踪文件，则服务器必须可以访问该目录。 同时注意，如果为 **sp_trace_create**指定本地目录，则该目录应是服务器上的本地目录。  
  
 如果使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，则可以将跟踪结果保存到文件或表中。 将跟踪结果保存到表中后，可以与将跟踪保存到文件中后一样进行访问，另外还可以查询表以搜索特定事件。  
  
 有关保存跟踪结果的详细信息，请参阅 [将跟踪结果保存到表 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) 和 [将跟踪结果保存到文件 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_create (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [创建跟踪 (Transact-SQL)](../sql-trace/create-a-trace-transact-sql.md)   
 [创建跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
