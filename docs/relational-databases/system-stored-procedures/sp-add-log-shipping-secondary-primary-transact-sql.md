---
title: sp_add_log_shipping_secondary_primary （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 155f59426e8167d5d888f3890089dd4b2ea3bf7c
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909688"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定的主数据库设置主服务器信息，添加本地和远程监视器链接，并在辅助服务器上创建复制作业和还原作业。  
  
 ![“主题链接”图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>参数  
在日志传送配置中 `[ @primary_server = ] 'primary_server'` [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 主实例的名称。 *primary_server*为**sysname** ，且不能为 NULL。  
  
`[ @primary_database = ] 'primary_database'` 是主服务器上的数据库的名称。 *primary_database* **sysname**，无默认值。  
  
`[ @backup_source_directory = ] 'backup_source_directory'` 存储主服务器中的事务日志备份文件的目录。 *backup_source_directory*为**nvarchar （500）** ，且不能为 NULL。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` 辅助服务器上将备份文件复制到的目录。 *backup_destination_directory*为**nvarchar （500）** ，且不能为 NULL。  
  
`[ @copy_job_name = ] 'copy_job_name'` 要创建的用于将事务日志备份复制到辅助服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的名称。 *copy_job_name*为**sysname** ，且不能为 NULL。  
  
`[ @restore_job_name = ] 'restore_job_name'` 是辅助服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的名称，可将备份还原到辅助数据库。 *restore_job_name*为**sysname** ，且不能为 NULL。  
  
`[ @file_retention_period = ] 'file_retention_period'` 在删除之前将备份文件保留在 @backup_destination_directory 参数指定的路径中的辅助服务器上的时间长度（分钟）。 *history_retention_period*的值为**int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
`[ @monitor_server = ] 'monitor_server'` 是监视服务器的名称。 *Monitor_server* **sysname**，无默认值，且不能为 NULL。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。  
  
 *monitor_server_security_mode*是**bit** ，并且不能为 NULL。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 是用于访问监视服务器的帐户的用户名。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 是用于访问监视服务器的帐户的密码。  
  
`[ @copy_job_id = ] 'copy_job_id' OUTPUT` 与辅助服务器上的复制作业关联的 ID。 *copy_job_id*为**uniqueidentifier** ，且不能为 NULL。  
  
`[ @restore_job_id = ] 'restore_job_id' OUTPUT` 与辅助服务器上的还原作业关联的 ID。 *restore_job_id*为**uniqueidentifier** ，且不能为 NULL。  
  
`[ @secondary_id = ] 'secondary_id' OUTPUT` 日志传送配置中辅助服务器的 ID。 *secondary_id*为**uniqueidentifier** ，且不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Remarks  
 必须从辅助服务器上的**master**数据库运行**sp_add_log_shipping_secondary_primary** 。 此存储过程执行以下操作：  
  
1.  为指定的主服务器和主数据库生成一个辅助 ID。  
  
2.  执行以下操作：  

    1.  使用提供的参数在**log_shipping_secondary**中添加辅助 ID 的条目。  
  
    2.  为禁用的辅助 ID 创建一个复制作业。  
  
    3.  将**log_shipping_secondary**条目中的复制作业 id 设置为复制作业的作业 id。  
  
    4.  为禁用的辅助 ID 创建一个还原作业。  
  
    5.  将**log_shipping_secondary**条目中的还原作业 id 设置为还原作业的作业 id。  
  
## <a name="permissions"></a>Permissions  
 只有**sysadmin**固定服务器角色的成员才能运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_add_log_shipping_secondary_primary**存储过程为辅助服务器上的主数据库 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 设置信息。  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
