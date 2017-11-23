---
title: "sys.sp_xtp_control_proc_exec_stats (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 721c120c200bb3142b36e06beb6e45cab1ca0805
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  对实例的本机编译存储过程启用统计信息收集。  
  
 若要启用在本机编译存储过程的查询级别统计信息收集，请参阅[sys.sp_xtp_control_query_exec_stats &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>语法  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>参数  
 @new_collection_value=*值*  
 决定打开 (1) 还是关闭 (0) 过程级统计信息收集。  
  
 @new_collection_value设置为零在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或数据库启动。  
  
 @old_collection_value=*值*  
 返回当前状态。  
  
## <a name="return-code"></a>返回代码  
 0 表示成功。 非零表示失败。  
  
## <a name="permissions"></a>Permissions  
 要求用户为固定 sysadmin 角色的成员。  
  
## <a name="code-samples"></a>代码示例  
 若要设置@new_collection_value和的值的查询@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
