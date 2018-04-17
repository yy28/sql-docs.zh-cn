---
title: log_shipping_monitor_primary (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2777315e2faecfd5af1778cedde314856b4da9c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在每个日志传送配置中为每个主数据库存储一条监视记录。 此表存储在**msdb**数据库。  
  
 与历史记录和监视相关的表也用于主服务器和辅助服务器。   
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|日志传送配置的主数据库 ID。|  
|**primary_server**|**sysname**|主实例的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]日志传送配置中。|  
|**primary_database**|**sysname**|日志传送配置中主数据库的名称。|  
|**backup_threshold**|**int**|备份操作之间的占用时间阈值（分钟），一旦超过此值，就会生成警报。|  
|**threshold_alert**|**int**|超过备份阈值时引发的警报。|  
|**threshold_alert_enabled**|**bit**|确定是否启用备份阈值警报。 1 = 已启用。<br /><br /> 0 = 禁用。|  
|**last_backup_file**|**nvarchar(500)**|最近一次事务日志备份的绝对路径。|  
|**last_backup_date**|**datetime**|上一次在主数据库上执行事务日志备份操作的时间和日期。|  
|**last_backup_date_utc**|**datetime**|上一次在主数据库上执行事务日志备份操作的时间和日期，使用协调世界时表示。|  
|**history_retention_period**|**int**|日志传送历史记录在删除前保留在给定主数据库中的时间（分钟）。|  
  
## <a name="remarks"></a>注释  
 除了存储远程监视服务器上，与主服务器相关的信息存储中的主服务器上其**log_shipping_monitor_primary**表。  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
