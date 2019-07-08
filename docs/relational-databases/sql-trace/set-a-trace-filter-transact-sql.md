---
title: 设置跟踪筛选器 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 617d0b4c015f52ea72e4fa2787198077e0e5da3c
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582413"
---
# <a name="set-a-trace-filter-transact-sql"></a>设置跟踪筛选器 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍了如何使用存储过程创建只检索有关所需跟踪事件信息的筛选器。  
  
### <a name="to-set-a-trace-filter"></a>设置跟踪筛选器  
  
1.  如果跟踪已在运行，请在执行 **sp_trace_setstatus** 时通过指定 **@status = 0** 停止跟踪。  
  
2.  执行 **sp_trace_setfilter** 以配置有关检索跟踪事件信息的类型。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!IMPORTANT]  
>  与常规的存储过程不同，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 存储过程 (sp_trace\_xx  ) 参数的类型都受到严格限制，不支持自动的数据类型转换  。 如果没有用正确的输入参数数据类型（参数说明中指定的类型）来调用这些参数，则存储过程将返回错误。  
  
## <a name="see-also"></a>另请参阅  
 [筛选跟踪](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
