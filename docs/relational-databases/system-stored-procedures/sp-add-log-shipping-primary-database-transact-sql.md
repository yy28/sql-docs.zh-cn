---
title: sp_add_log_shipping_primary_database (Transact SQL) |Microsoft 文档
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
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 002e467254e145a3299b12f3df2f7d1e0e491955
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置日志传送配置（包括备份作业、本地监视记录及远程监视记录）的主数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>参数  
 [  **@database=** ]*数据库*  
 日志传送主数据库的名称。 *数据库*是**sysname**，无默认值，并不能为 NULL。  
  
 [  **@backup_directory=** ]*backup_directory*  
 主服务器上备份文件夹的路径。 *backup_directory*是**nvarchar(500)**，无默认值，并不能为 NULL。  
  
 [  **@backup_share=** ]*backup_share*  
 主服务器上备份目录的网络路径。 *backup_share*是**nvarchar(500)**，无默认值，并不能为 NULL。  
  
 [ **@backup_job_name=** ] '*backup_job_name*'  
 主服务器上用于将备份复制到备份文件夹中的 SQL Server 代理作业的名称。 *backup_job_name*是**sysname**和不能为 NULL。  
  
 [ **@backup_retention_period=** ] *backup_retention_period*  
 在主服务器上的备份目录中保留日志备份文件的时间长度（分钟）。 *backup_retention_period*是**int**，无默认值，并不能为 NULL。  
  
 [  **@monitor_server=** ]*monitor_server*  
 监视服务器的名称。 *Monitor_server*是**sysname**，无默认值，并不能为 NULL。  
  
 [ **@monitor_server_security_mode=** ] *monitor_server_security_mode*  
 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 *monitor_server_security_mode*是**位**和不能为 NULL。  
  
 [  **@monitor_server_login=** ]*monitor_server_login*  
 访问监视服务器所用的帐户的用户名。  
  
 [  **@monitor_server_password=** ]*monitor_server_password*  
 用于访问监视服务器的帐户的密码。  
  
 [  **@backup_threshold=** ] *backup_threshold*  
 是的总时间，以分钟为单位之前, 在上次备份后*threshold_alert*引发错误。 *backup_threshold*是**int**，默认值为 60 分钟。  
  
 [  **@threshold_alert=** ] *threshold_alert*  
 是在超出备份阈值时发出警报。 *threshold_alert*是**int**，默认值为 14,420。  
  
 [ **@threshold_alert_enabled=** ] *threshold_alert_enabled*  
 指定是否将是警报时引发*backup_threshold*超出。 默认值零 (0) 表示警报被禁用，将不会引发警报。 *threshold_alert_enabled*是**位**。  
  
 [ **@history_retention_period=** ] *history_retention_period*  
 历史记录的保留时间长度（分钟）。 *history_retention_period*是**int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
 [ **@backup_job_id=** ] *backup_job_id* OUTPUT  
 与主服务器上的备份作业相关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业 ID。 *backup_job_id*是**uniqueidentifier**和不能为 NULL。  
  
 [  **@primary_id=** ] *primary_id*输出  
 日志传送配置的主数据库 ID。 *primary_id*是**uniqueidentifier**和不能为 NULL。  
  
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
 **sp_add_log_shipping_primary_database**必须从运行**master**主服务器上的数据库。 此存储过程可执行以下功能：  
  
1.  生成的主 ID 并将主数据库的条目添加表中**log_shipping_primary_databases**使用提供的参数。  
  
2.  为被禁用的主数据库创建一个备份作业。  
  
3.  设置的备份作业 ID **log_shipping_primary_databases**进入备份作业的作业 ID。  
  
4.  表中添加本地监视记录**log_shipping_monitor_primary**主服务器上使用提供自变量。  
  
5.  如果不同于主服务器监视服务器，将添加中的监视器记录**log_shipping_monitor_primary**监视器使用 server 提供自变量。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例将在日志传送配置中添加 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库作为主数据库。  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
