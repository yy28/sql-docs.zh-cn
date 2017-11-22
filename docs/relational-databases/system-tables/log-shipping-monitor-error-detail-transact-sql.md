---
title: "log_shipping_monitor_error_detail (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs: TSQL
helpviewer_keywords: log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7a2797659e6f20192a87662700632c399f72763
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储日志传送作业的错误详细信息。 此表存储在**msdb**数据库。  
  
 与历史记录和监视相关的表也用于主服务器和辅助服务器。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|用于备份的主 ID 或者用于复制或还原的辅助 ID。|  
|**agent_type**|**tinyint**|日志传送作业的类型。<br /><br /> 0 = 备份。<br /><br /> 1 = 复制。<br /><br /> 2 = 还原。|  
|**session_id**|**int**|备份/复制/还原作业的会话 ID。|  
|**database_name**|**sysname**|与此错误记录相关联的数据库的名称。 用于备份的主数据库、用于还原的辅助数据库或用于复制的空数据库。|  
|**sequence_number**|**int**|一个增量数字，指示跨多个记录的错误信息的正确顺序。|  
|**log_time**|**datetime**|创建记录的日期和时间。|  
|**log_time_utc**|**datetime**|创建记录的日期和时间，使用通用协调时间表示。|  
|**消息**|**nvarchar**|消息正文。|  
|**源 (source)**|**nvarchar**|错误消息或事件的源。|  
|**help_url**|**nvarchar**|可从中找到更多错误信息的 URL（如果有）。|  
  
## <a name="remarks"></a>注释  
 此表包含日志传送代理的错误详细信息。 每个错误都记录为一个异常序列。 每个代理会话可以有多个错误（序列）。  
  
 除了存储远程监视服务器上，与主服务器相关的信息存储中的主服务器上其**log_shipping_monitor_error_detail**表和与辅助服务器相关的信息中的辅助服务器上也存储其**log_shipping_monitor_error_detail**表。  
  
 若要标识某个代理会话，请使用列**agent_id**， **agent_type**，和**session_id**。 作为排序依据**log_time**若要查看在其中记录的顺序中的错误。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;Transact SQL &#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
