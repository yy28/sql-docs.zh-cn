---
title: "KILL STATS JOB (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2df18cfd1e0803fb937965ecc6c5880614e25df2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  终止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的异步统计信息更新作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>参数  
 *job_id*  
 job_id 字段，由该作业的 sys.dm_exec_background_job_queue 动态管理视图返回。  
  
## <a name="remarks"></a>注释  
 job_id 与在其他形式的 KILL 语句中所使用的 session_id 或工作单元无关。  
  
## <a name="permissions"></a>权限  
 若要从 sys.dm_exec_background_job_queue 动态管理视图访问信息，用户必须具有 VIEW SERVER STATE 权限。  
  
 默认情况下，sysadmin 和 processadmin 固定数据库角色的成员具有 KILL STATS JOB 权限，并且该权限不可转移。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何终止与作业相关联的统计信息更新其中*job_id* = `53`。  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [KILL &#40;Transact SQL &#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [终止查询通知订阅 &#40;Transact SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [统计信息](../../relational-databases/statistics/statistics.md)  
  
  
