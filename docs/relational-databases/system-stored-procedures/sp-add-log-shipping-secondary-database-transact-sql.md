---
title: "sp_add_log_shipping_secondary_database (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 965f2191ba9dbdbba5be91412c1459064972c22c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spaddlogshippingsecondarydatabase-transact-sql"></a>sp_add_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为日志传送设置辅助数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>参数  
 [ **@secondary_database** = ] '*secondary_database*'  
 辅助数据库的名称。 *secondary_database*是**sysname**，无默认值。  
  
 [ **@primary_server** = ] '*primary_server*'  
 主实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。 *primary_server*是**sysname**和不能为 NULL。  
  
 [ **@primary_database** = ] '*primary_database*'  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [ **@restore_delay** = ] '*restore_delay*'  
 辅助服务器在还原给定备份文件之前等待的时间（分钟）。 *restore_delay*是**int**和不能为 NULL。 默认值为 0。  
  
 [ **@restore_all** = ] '*restore_all*'  
 如果设置为 1，则在运行还原作业时，辅助服务器将还原所有可用的事务日志备份。 否则，辅助服务器将在还原一个文件后停止。 *restore_all*是**位**和不能为 NULL。  
  
 [ **@restore_mode** = ] '*restore_mode*'  
 辅助数据库的还原模式。  
  
 0 = with NORECOVERY 还原日志。  
  
 1 = 与待机还原日志。  
  
 *还原*是**位**和不能为 NULL。  
  
 [ **@disconnect_users** = ] '*disconnect_users*'  
 如果设置为 1，则在执行还原操作时，会断开用户与辅助数据库的连接。 默认值 = 0。 *断开连接*users 是**位**和不能为 NULL。  
  
 [  **@block_size**  =] '*block_size*  
 用作备份设备的块大小（字节）。 *block_size*是**int**默认值为-1。  
  
 [ **@buffer_count** = ] '*buffer_count*'  
 备份或还原操作使用的缓冲区总数。 *buffer_count*是**int**默认值为-1。  
  
 [ **@max_transfer_size** = ] '*max_transfer_size*'  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向备份设备发出的最大输入或输出请求的大小（字节）。 *max_transfersize*是**int**而且可以为 NULL。  
  
 [ **@restore_threshold** = ] '*restore_threshold*'  
 两次还原操作之间允许的间隔时间（分钟），一旦超过此值，就会生成警报。 *restore_threshold*是**int**和不能为 NULL。  
  
 [ **@threshold_alert** = ] '*threshold_alert*'  
 是在超出备份阈值时发出警报。 *threshold_alert*是**int**，默认值为 14,420。  
  
 [ **@threshold_alert_enabled** = ] '*threshold_alert_enabled*'  
 指定是否发生警报时*backup_threshold*超出。 默认值一 (1) 表示要引发警告。 *threshold_alert_enabled*是**位**。  
  
 [ **@history_retention_period** = ] '*history_retention_period*'  
 历史记录的保留时间（分钟）。 *history_retention_period*是**int**，默认值为 NULL。 如果不指定值，则使用值 14420。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_add_log_shipping_secondary_database**必须从运行**master**辅助服务器上的数据库。 此存储过程执行以下操作：  
  
1.  **sp_add_log_shipping_secondary_primary**应在此存储过程以初始化主日志传送辅助服务器上的数据库信息之前调用。  
  
2.  添加一个条目中的辅助数据库**log_shipping_secondary_databases**使用提供的参数。  
  
3.  将添加在本地监视记录**log_shipping_monitor_secondary**辅助服务器上使用提供自变量。  
  
4.  如果不同于辅助服务器监视服务器，将添加中的监视器记录**log_shipping_monitor_secondary**监视器使用 server 提供自变量。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_add_log_shipping_secondary_database**存储过程来将数据库添加**LogShipAdventureWorks**为日志传送配置中的辅助数据库与主数据库[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]驻留在主服务器 TRIBECA 上。  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_database   
@secondary_database = N'LogShipAdventureWorks'   
,@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks2012'   
,@restore_delay = 0   
,@restore_mode = 1   
,@disconnect_users = 0   
,@restore_threshold = 45     
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 &#40;SQL server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
