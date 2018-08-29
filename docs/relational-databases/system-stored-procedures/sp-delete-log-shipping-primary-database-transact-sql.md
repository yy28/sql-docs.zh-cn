---
title: sp_delete_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 302cdeb85ad475354d26a988580283db57415a40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023573"
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此存储过程删除主数据库的日志传送，包括备份作业、本地历史记录以及远程历史记录。 在删除辅助数据库使用后只能使用此存储的过程**sp_delete_log_shipping_primary_secondary**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>参数  
 [  **@database =** ] '*数据库*  
 日志传送主数据库的名称。 *数据库*是**sysname**，无默认值，且不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>Remarks  
 **sp_delete_log_shipping_primary_database**必须从运行**主**主服务器上的数据库。 此存储过程执行以下操作：  
  
1.  为指定的主数据库删除备份作业。  
  
2.  中的本地监视记录中删除**log_shipping_monitor_primary**主服务器上。  
  
3.  中的对应项中移除**log_shipping_monitor_history_detail**并**log_shipping_monitor_error_detail**。  
  
4.  如果监视服务器不同于主服务器，删除中的监视记录**log_shipping_monitor_primary**在监视服务器上。  
  
5.  中的对应项中移除**log_shipping_monitor_history_detail**并**log_shipping_monitor_error_detail**在监视服务器上。  
  
6.  删除中的条目**log_shipping_primary_databases**此主数据库。  
  
7.  调用**sp_delete_log_shipping_alert_job**在监视服务器上。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_delete_log_shipping_primary_database**若要删除主数据库**AdventureWorks2012**。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
