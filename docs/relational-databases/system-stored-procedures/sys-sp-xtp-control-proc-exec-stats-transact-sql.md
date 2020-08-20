---
description: sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
title: sys. sp_xtp_control_proc_exec_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e189cd4e7a5ec9f488cce78ee6cc159c8700a463
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473394"
---
# <a name="syssp_xtp_control_proc_exec_stats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  对实例的本机编译存储过程启用统计信息收集。  
  
 若要在查询级别为本机编译的存储过程启用统计信息收集，请参阅 [transact-sql&#41;&#40;sp_xtp_control_query_exec_stats ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>参数  
 @new_collection_value = *值*  
 决定打开 (1) 还是关闭 (0) 过程级统计信息收集。  
  
 @new_collection_value 当或数据库启动时，将设置为零 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 @old_collection_value = *值*  
 返回当前状态。  
  
## <a name="return-code"></a>返回代码  
 0 表示成功。 非零表示失败。  
  
## <a name="permissions"></a>权限  
 要求用户为固定 sysadmin 角色的成员。  
  
## <a name="code-samples"></a>代码示例  
 设置 @new_collection_value 和查询值 @new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
