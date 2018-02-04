---
title: "log_shipping_secondary (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f66609b64ef7066fe7edf1ca8459d68cda597f9d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="logshippingsecondary-transact-sql"></a>log_shipping_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个辅助 ID 存储一条记录。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|日志传送配置中辅助服务器的 ID。|  
|**primary_server**|**sysname**|日志传送配置中 SQL Server 数据库引擎的主要实例的名称。|  
|**primary_database**|**sysname**|日志传送配置中主数据库的名称。|  
|**backup_source_directory**|**nvarchar(500)**|存储主服务器的事务日志备份文件的目录。|  
|**backup_destination_directory**|**nvarchar(500)**|备份文件复制到的辅助服务器上的目录。|  
|**file_retention_period**|**int**|备份文件被删除之前在辅助服务器上保留的时间（以分钟为单位）。|  
|**copy_job_id**|**uniqueidentifier**|与辅助服务器上的复制作业关联的 ID。|  
|**restore_job_id**|**uniqueidentifier**|与辅助服务器上的还原作业关联的 ID。|  
|**monitor_server**|**sysname**|实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]用作监视服务器中的日志传送配置。|  
|**monitor_server_security_mode**|**bit**|用于连接到监视服务器的安全模式。<br /><br /> 1 = Windows 身份验证。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**last_copied_file**|**nvarchar(500)**|上次复制到辅助服务器的备份文件的文件名。|  
|**last_copied_date**|**datetime**|上次复制到辅助服务器的时间和日期。|  
  
## <a name="remarks"></a>注释  
 给定的主数据库相同的辅助服务器上的多个辅助数据库共享中的某些设置**log_shipping_secondary**表。 如果更改了其中一个数据库的共享设置，则所有数据库的该设置都将被更改。  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 &#40;SQL server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
