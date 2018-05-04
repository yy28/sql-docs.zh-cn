---
title: sp_change_log_shipping_primary_database (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d4a266a220a1be4597a82248618413348e4d62b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spchangelogshippingprimarydatabase-transact-sql"></a>sp_change_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改主数据库设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@database =** ]*数据库*  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [ **@backup_directory =** ] '*backup_directory*'  
 主服务器上备份文件夹的路径。 *backup_directory*是**nvarchar(500)**，无默认值，并不能为 NULL。  
  
 [  **@backup_share =** ]*backup_share*  
 主服务器上备份目录的网络路径。 *backup_share*是**nvarchar(500)**，无默认值，并不能为 NULL。  
  
 [ **@backup_retention_period =** ] '*backup_retention_period*'  
 在主服务器上的备份目录中保留日志备份文件的时间长度（分钟）。 *backup_retention_period*是**int**，无默认值，并不能为 NULL。  
  
 [ **@monitor_server_security_mode =** ] '*monitor_server_security_mode*'  
 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 = SQL Server 身份验证。  
  
 *monitor_server_security_mode*是**位**和不能为 NULL。  
  
 [ **@monitor_server_login =** ] '*monitor_server_login*'  
 访问监视服务器所用的帐户的用户名。  
  
 [  **@monitor_server_password =** ]*monitor_server_password*  
 用于访问监视服务器的帐户的密码。  
  
 [  **@backup_threshold =** ]*backup_threshold*  
 是的总时间，以分钟为单位之前, 在上次备份后*threshold_alert*引发错误。 *backup_threshold*是**int**，默认值为 60 分钟。  
  
 [  **@threshold_alert =** ]*threshold_alert*  
 超过备份阈值时引发的警报。 *threshold_alert*是**int**和不能为 NULL。  
  
 [ **@threshold_alert_enabled =** ] '*threshold_alert_enabled*'  
 指定是否发生警报时*backup_threshold*超出。  
  
 1 = 启用。  
  
 0 = 已禁用。  
  
 *threshold_alert_enabled*是**位**和不能为 NULL。  
  
 [ **@history_retention_period =** ] '*history_retention_period*'  
 历史记录的保留时间（分钟）。 *history_retention_period*是**int**。如果不指定值，则使用值 14420。  
  
 [ **@backup_compression**= ] *backup_compression_option*  
 指定是否使用日志传送配置[备份压缩](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 只有 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]（或更高版本）支持此参数。  
  
 0 = 禁用。 从不压缩日志备份。  
  
 1 = 已启用。 始终压缩日志备份。  
  
 2 = 使用的设置[查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。 这是默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_change_log_shipping_primary_database**必须从运行**master**主服务器上的数据库。 此存储过程执行以下操作：  
  
1.  更改中的设置**log_shipping_primary_database**记录，如有必要。  
  
2.  更改中的本地记录**log_shipping_monitor_primary**主服务器上使用提供的变量，如有必要。  
  
3.  如果不同于主服务器监视服务器，更改记录在**log_shipping_monitor_primary**监视器服务器使用提供的变量，如有必要。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_change_log_shipping_primary_database**更新主数据库与关联的设置[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
