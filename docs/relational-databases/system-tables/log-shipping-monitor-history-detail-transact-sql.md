---
title: log_shipping_monitor_history_detail (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b57136a4f8378c25892fa32c29956d89f7da9868
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="logshippingmonitorhistorydetail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储日志传送作业的历史记录详细信息。 此表存储在**msdb**数据库。  
  
 与历史记录和监视相关的表也用于主服务器和辅助服务器。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|用于备份的主 ID 或者用于复制或还原的辅助 ID。|  
|**agent_type**|**tinyint**|日志传送作业的类型。<br /><br /> 0 = 备份。<br /><br /> 1 = 复制。<br /><br /> 2 = 还原。|  
|**session_id**|**int**|备份/复制/还原作业的会话 ID。|  
|**database_name**|**sysname**|与此记录关联的数据库的名称。 用于备份的主数据库、用于还原的辅助数据库或用于复制的空数据库。|  
|**session_status**|**tinyint**|会话的状态。<br /><br /> 0 = 正在启动。<br /><br /> 1 = 正在运行。<br /><br /> 2 = 成功。<br /><br /> 3 = 错误。<br /><br /> 4 = 警告。|  
|**log_time**|**datetime**|创建记录的日期和时间。|  
|**log_time_utc**|**datetime**|创建记录的日期和时间，使用通用协调时间表示。|  
|message|**nvarchar(max)**|消息正文。|  
  
## <a name="remarks"></a>注释  
 此表包含日志传送代理的历史记录详细信息。 若要标识某个代理会话，请使用列**agent_id**， **agent_type**，和**session_id**。 若要查看代理会话的历史记录详细信息，按排序**log_time**。  
  
 除了存储远程监视服务器上，与主服务器相关的信息存储中的主服务器上其**log_shipping_monitor_history_detail**表和到辅助副本相关的信息服务器还在辅助服务器上存储其**log_shipping_monitor_history_detail**表。  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [系统表&#40;Transact SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
