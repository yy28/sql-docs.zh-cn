---
title: 设置跟踪筛选器 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6e3ecc4b125d226fc2cdf6dbe241e0ce017eae6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126687"
---
# <a name="set-a-trace-filter-transact-sql"></a>设置跟踪筛选器 (Transact-SQL)
  本主题介绍了如何使用存储过程创建只检索有关所需跟踪事件信息的筛选器。  
  
### <a name="to-set-a-trace-filter"></a>设置跟踪筛选器  
  
1.  如果跟踪已在运行，请在执行 **sp_trace_setstatus** 时通过指定 **@status = 0** 停止跟踪。  
  
2.  执行 **sp_trace_setfilter** 以配置有关检索跟踪事件信息的类型。  
  
> [!IMPORTANT]
>  与常规存储过程，所有的参数不同[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]存储过程 (<strong>sp_trace_*xx*</strong>) 已严格类型化和不支持自动数据类型转换。 如果没有用正确的输入参数数据类型（参数说明中指定的类型）来调用这些参数，则存储过程将返回错误。  
  
## <a name="see-also"></a>请参阅  
 [筛选跟踪](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
