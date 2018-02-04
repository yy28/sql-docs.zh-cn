---
title: "sp_delete_log_shipping_primary_database (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb6fef78645552f7f4bd0b60d16a05e89633658f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此存储过程删除主数据库的日志传送，包括备份作业、本地历史记录以及远程历史记录。 仅使用此存储的过程后已删除辅助数据库使用**sp_delete_log_shipping_primary_secondary**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>参数  
 [ **@database =** ] '*database*'  
 日志传送主数据库的名称。 *数据库*是**sysname**，无默认值，并不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>注释  
 **sp_delete_log_shipping_primary_database**必须从运行**master**主服务器上的数据库。 此存储过程执行以下操作：  
  
1.  为指定的主数据库删除备份作业。  
  
2.  删除在本地监视记录**log_shipping_monitor_primary**主服务器上。  
  
3.  删除中的对应条目**log_shipping_monitor_history_detail**和**log_shipping_monitor_error_detail**。  
  
4.  如果不同于主服务器监视服务器，删除中的监视器记录**log_shipping_monitor_primary**监视服务器上。  
  
5.  删除中的对应条目**log_shipping_monitor_history_detail**和**log_shipping_monitor_error_detail**监视服务器上。  
  
6.  删除中的条目**log_shipping_primary_databases**此主数据库。  
  
7.  调用**sp_delete_log_shipping_alert_job**监视服务器上。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_delete_log_shipping_primary_database**删除主数据库**AdventureWorks2012**。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 &#40;SQL server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
