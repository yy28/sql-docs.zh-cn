---
title: sp_change_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3a713687d41c21a3c99c30d6b7192d7c59e41505
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492719"
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
`[ @database = ] 'database'` 是主服务器上的名称。 *primary_database*是**sysname**，无默认值。  
  
`[ @backup_directory = ] 'backup_directory'` 是主服务器上备份文件夹的路径。 *backup_directory*是**nvarchar(500)**，无默认值，且不能为 NULL。  
  
`[ @backup_share = ] 'backup_share'` 是主服务器上的备份目录的网络路径。 *backup_share*是**nvarchar(500)**，无默认值，且不能为 NULL。  
  
`[ @backup_retention_period = ] 'backup_retention_period'` 是，以分钟为单位保留日志备份文件的备份目录中的主服务器上的长度。 *backup_retention_period*是**int**，无默认值，且不能为 NULL。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 用来连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 = SQL Server 身份验证。  
  
 *monitor_server_security_mode*是**位**且不能为 NULL。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 是用于访问监视服务器的用户名。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 是用于访问监视服务器的密码。  
  
`[ @backup_threshold = ] 'backup_threshold'` 时间，以分钟为单位，一次备份之前的长度*threshold_alert*引发错误。 *backup_threshold*是**int**，默认值为 60 分钟。  
  
`[ @threshold_alert = ] 'threshold_alert'` 超过备份阈值时引发警报。 *threshold_alert*是**int**且不能为 NULL。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定是否引发警报时*backup_threshold*超出。  
  
 1 = 启用。  
  
 0 = 已禁用。  
  
 *threshold_alert_enabled*是**位**且不能为 NULL。  
  
`[ @history_retention_period = ] 'history_retention_period'` 是以分钟为单位历史记录保留在其中长度。 *history_retention_period*是**int**。如果不指定值，则使用值 14420。  
  
`[ @backup_compression = ] backup_compression_option` 指定是否使用日志传送配置[备份压缩](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 只有 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]（或更高版本）支持此参数。  
  
 0 = 禁用。 从不压缩日志备份。  
  
 1 = 已启用。 始终压缩日志备份。  
  
 2 = 使用的设置[查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。 这是默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_change_log_shipping_primary_database**必须从运行**主**主服务器上的数据库。 此存储过程执行以下操作：  
  
1.  更改中的设置**log_shipping_primary_database**记录，如有必要。  
  
2.  更改中的本地记录**log_shipping_monitor_primary**主服务器上使用提供的参数，如有必要。  
  
3.  如果监视服务器不同于主服务器，更改记录在**log_shipping_monitor_primary**监视器服务器使用提供的参数，如有必要。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_change_log_shipping_primary_database**来更新与主数据库相关联的设置[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
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
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
