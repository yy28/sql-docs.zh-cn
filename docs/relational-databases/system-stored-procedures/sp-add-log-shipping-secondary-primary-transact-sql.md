---
title: "sp_add_log_shipping_secondary_primary (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs: TSQL
helpviewer_keywords: sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5e5058e0403c06d722b29f0ff68d20240724a42
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlogshippingsecondaryprimary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定的主数据库设置主服务器信息，添加本地和远程监视器链接，并在辅助服务器上创建复制作业和还原作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@primary_server**  =] '*primary_server*  
 主实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。 *primary_server*是**sysname**和不能为 NULL。  
  
 [  **@primary_database**  =] '*primary_database*  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [  **@backup_source_directory**  =] '*backup_source_directory*  
 存储主服务器的事务日志备份文件的目录。 *backup_source_directory*是**nvarchar(500)**和不能为 NULL。  
  
 [  **@backup_destination_directory**  =] '*backup_destination_directory*  
 备份文件复制到的辅助服务器上的目录。 *backup_destination_directory*是**nvarchar(500)**和不能为 NULL。  
  
 [  **@copy_job_name**  =] '*copy_job_name*  
 要创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业使用的名称，此代理作业用于将事务日志备份复制到辅助服务器。 *copy_job_name*是**sysname**和不能为 NULL。  
  
 [  **@restore_job_name**  =] '*restore_job_name*  
 是的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将备份还原到辅助数据库的辅助服务器上的代理作业。 *restore_job_name*是**sysname**和不能为 NULL。  
  
 [  **@file_retention_period**  =] '*file_retention_period*  
 总时间，以分钟为单位的备份文件将保留在指定的路径中的辅助服务器@backup_destination_directory之前正在删除的参数。 *history_retention_period*是**int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
 [  **@monitor_server**  =] '*monitor_server*  
 监视服务器的名称。 *Monitor_server*是**sysname**，无默认值，并不能为 NULL。  
  
 [  **@monitor_server_security_mode**  =] '*monitor_server_security_mode*  
 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。  
  
 *monitor_server_security_mode*是**位**和不能为 NULL。  
  
 [  **@monitor_server_login**  =] '*monitor_server_login*  
 访问监视服务器所用的帐户的用户名。  
  
 [  **@monitor_server_password**  =] '*monitor_server_password*  
 用于访问监视服务器的帐户的密码。  
  
 [  **@copy_job_id**  =] '*copy_job_id*输出  
 与辅助服务器上的复制作业关联的 ID。 *copy_job_id*是**uniqueidentifier**和不能为 NULL。  
  
 [  **@restore_job_id**  =] '*restore_job_id*输出  
 与辅助服务器上的还原作业关联的 ID。 *restore_job_id*是**uniqueidentifier**和不能为 NULL。  
  
 [  **@secondary_id**  =] '*secondary_id*输出  
 日志传送配置中辅助服务器的 ID。 *secondary_id*是**uniqueidentifier**和不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 **sp_add_log_shipping_secondary_primary**必须从运行**master**辅助服务器上的数据库。 此存储过程执行以下操作：  
  
1.  为指定的主服务器和主数据库生成一个辅助 ID。  
  
2.  执行以下任务：  
  
    1.  添加一个条目中辅助 id **log_shipping_secondary**使用提供的参数。  
  
    2.  为禁用的辅助 ID 创建一个复制作业。  
  
    3.  设置的复制作业 ID **log_shipping_secondary**进入复制作业的作业 ID。  
  
    4.  为禁用的辅助 ID 创建一个还原作业。  
  
    5.  在中设置的还原作业 ID **log_shipping_secondary**进入还原作业的作业 ID。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_add_log_shipping_secondary_primary**存储过程来设置主数据库的信息[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]辅助服务器上。  
  
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
  
  
