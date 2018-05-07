---
title: sp_change_log_shipping_secondary_primary (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 499c95fc980bd6e8d996b14c47907b814cbb94aa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改辅助数据库设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>参数  
 [ **@primary_server** =] '*primary_server*  
 主实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。 *primary_server*是**sysname**和不能为 NULL。  
  
 [ **@primary_database** =] '*primary_database*  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [ **@backup_source_directory** = ] '*backup_source_directory*'  
 存储主服务器的事务日志备份文件的目录。 *backup_source_directory*是**nvarchar(500)** 和不能为 NULL。  
  
 [ **@backup_destination_directory** =] '*backup_destination_directory*  
 备份文件复制到的辅助服务器上的目录。 *backup_destination_directory*是**nvarchar(500)** 和不能为 NULL。  
  
 [ **@file_retention_period** =] '*file_retention_period*  
 历史记录的保留时间长度（分钟）。 *history_retention_period*是**int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
 [ **@monitor_server_security_mode** =] '*monitor_server_security_mode*  
 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证；  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 *monitor_server_security_mode*是**位**和不能为 NULL。  
  
 [ **@monitor_server_login** =] '*monitor_server_login*  
 访问监视服务器所用的帐户的用户名。  
  
 [ **@monitor_server_password** =] '*monitor_server_password*  
 用于访问监视服务器的帐户的密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_change_log_shipping_secondary_primary**必须从运行**master**辅助服务器上的数据库。 此存储过程执行以下操作：  
  
1.  更改设置**log_shipping_secondary**根据需要记录。  
  
2.  如果不同于辅助服务器监视服务器，更改监视中的记录**log_shipping_monitor_secondary**监视器服务器使用提供的变量，如有必要。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
