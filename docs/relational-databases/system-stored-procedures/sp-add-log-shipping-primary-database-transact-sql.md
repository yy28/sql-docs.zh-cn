---
title: sp_add_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 854edf82c32058c45df4ab4f71803933f59f2582
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494099"
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
`[ @database = ] 'database'` 是日志传送主数据库的名称。 *数据库*是**sysname**，无默认值，且不能为 NULL。  
  
`[ @backup_directory = ] 'backup_directory'` 是主服务器上备份文件夹的路径。 *backup_directory*是**nvarchar(500)**，无默认值，且不能为 NULL。  
  
`[ @backup_share = ] 'backup_share'` 是主服务器上的备份目录的网络路径。 *backup_share*是**nvarchar(500)**，无默认值，且不能为 NULL。  
  
`[ @backup_job_name = ] 'backup_job_name'` 是将备份复制到备份文件夹的主服务器上的 SQL Server 代理作业的名称。 *backup_job_name*是**sysname**且不能为 NULL。  
  
`[ @backup_retention_period = ] backup_retention_period` 是，以分钟为单位保留日志备份文件的备份目录中的主服务器上的长度。 *backup_retention_period*是**int**，无默认值，且不能为 NULL。  
  
`[ @monitor_server = ] 'monitor_server'` 是监视服务器的名称。 *Monitor_server*是**sysname**，无默认值，且不能为 NULL。  
  
`[ @monitor_server_security_mode = ] monitor_server_security_mode` 用来连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 *monitor_server_security_mode*是**位**且不能为 NULL。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 是用于访问监视服务器的用户名。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 是用于访问监视服务器的密码。  
  
`[ @backup_threshold = ] backup_threshold` 时间，以分钟为单位，一次备份之前的长度*threshold_alert*引发错误。 *backup_threshold*是**int**，默认值为 60 分钟。  
  
`[ @threshold_alert = ] threshold_alert` 是要超过备份阈值时引发的警报。 *threshold_alert*是**int**，默认值为 14,420。  
  
`[ @threshold_alert_enabled = ] threshold_alert_enabled` 指定是否将是警报时引发*backup_threshold*超出。 默认值零 (0) 表示警报被禁用，将不会引发警报。 *threshold_alert_enabled*是**位**。  
  
`[ @history_retention_period = ] history_retention_period` 是以分钟为单位保留历史记录长度。 *history_retention_period*是**int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
`[ @backup_job_id = ] backup_job_id OUTPUT` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与主服务器上的备份作业相关联的代理作业 ID。 *backup_job_id*是**uniqueidentifier**且不能为 NULL。  
  
`[ @primary_id = ] primary_id OUTPUT` 日志传送配置的主数据库的 ID。 *primary_id*是**uniqueidentifier**且不能为 NULL。  
  
`[ @backup_compression = ] backup_compression_option` 指定是否使用日志传送配置[备份压缩](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 只有 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]（或更高版本）支持此参数。  
  
 0 = 禁用。 从不压缩日志备份。  
  
 1 = 已启用。 始终压缩日志备份。  
  
 2 = 使用的设置[查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。 这是默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_log_shipping_primary_database**必须从运行**主**主服务器上的数据库。 此存储过程可执行以下功能：  
  
1.  生成主 ID，并在表中添加主数据库的条目**log_shipping_primary_databases**使用所提供的参数。  
  
2.  为被禁用的主数据库创建一个备份作业。  
  
3.  设置中的备份作业 ID **log_shipping_primary_databases**备份作业的作业 id 的条目。  
  
4.  在表中添加本地监视记录**log_shipping_monitor_primary**主服务器上使用提供的参数。  
  
5.  如果监视服务器从主服务器不同，监视器中添加记录**log_shipping_monitor_primary**监视器服务器使用提供的参数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
