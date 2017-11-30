---
title: "sp_help_log_shipping_secondary_primary (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
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
- sp_help_log_shipping_secondary_primary
- sp_help_log_shipping_secondary_primary_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_log_shipping_secondary_primary
ms.assetid: 1310fdaf-edb5-4294-9739-7fb37c2c2cb5
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba555812c165c5818da62801e640795b7663fbad
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelplogshippingsecondaryprimary-transact-sql"></a>sp_help_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程将在辅助服务器上检索给定的主数据库的设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server' OR  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>参数  
 [  **@primary_server**  =] '*primary_server*  
 主实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。 *primary_server*是**sysname**和不能为 NULL。  
  
 [  **@primary_database**  =] '*primary_database*  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 结果集包含列**secondary_id**， **primary_server**， **primary_database**， **backup_source_directory**， **backup_destination_directory**， **file_retention_period**， **copy_job_id**， **restore_job_id**， **monitor_server**， **monitor_server_security_mode**从**log_shipping_secondary**。  
  
## <a name="remarks"></a>注释  
 **sp_help_log_shipping_secondary_primary**必须从运行**master**辅助服务器上的数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
