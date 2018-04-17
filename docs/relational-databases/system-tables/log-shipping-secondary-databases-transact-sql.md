---
title: log_shipping_secondary_databases (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 206ed601e845fb4eceddcbca7146e4ca6974f71f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingsecondarydatabases-transact-sql"></a>log_shipping_secondary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在日志传送配置中为每个辅助数据库存储一条记录。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|日志传送配置中辅助数据库的名称。|  
|**secondary_id**|**uniqueidentifier**|日志传送配置中辅助服务器的 ID。|  
|**restore_delay**|**int**|以分钟为单位的辅助服务器将还原给定的备份文件之前等待的时间量。 默认为 0 分钟。|  
|**restore_all**|**bit**|如果设置为 1，则辅助服务器将在还原作业运行时还原所有可用的事务日志备份。 否则，在原还了一个文件之后它将停止。|  
|**restore_mode**|**bit**|辅助数据库的还原模式。<br /><br /> 0 = with NORECOVERY 还原日志。<br /><br /> 1 = 使用 STANDBY 还原日志。|  
|**disconnect_users**|**bit**|如果设置为 1，则当执行还原操作时，将断开用户与辅助数据库的连接。 默认值 = 0。|  
|**block_size**|**int**|用作备份设备的块大小（字节）。|  
|**buffer_count**|**int**|备份或还原操作使用的缓冲区总数。|  
|**max_transfer_size**|**int**|大小，以字节为单位的最大输入或输出请求由颁发[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份设备。|  
|**last_restored_file**|**nvarchar(500)**|上次还原到辅助数据库的备份文件的文件名。|  
|**last_restored_date**|**datetime**|上次对辅助数据库执行还原操作的时间和日期。|  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
