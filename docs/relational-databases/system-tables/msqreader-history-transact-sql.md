---
title: "MSqreader_history (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c9615bb702c89d8b2a5be0087671df9d8a6a910
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msqreaderhistory-transact-sql"></a>MSqreader_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSqreader_history**表中包含与本地分发服务器关联的队列读取器代理程序历史记录行数。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|队列读取器代理的 ID。|  
|**publication_id**|**int**|发布 ID。|  
|**runstatus**|**int**|代理的运行状态：<br /><br /> **1** = start。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**start_time**|**datetime**|代理会话开始的日期和时间。|  
|**time**|**datetime**|最后记录消息的日期和时间。|  
|**duration**|**int**|记录的会话活动的占用时间（秒）。|  
|**注释**|**nvarchar(255)**|说明文本。|  
|**transaction_id 收集**|**nvarchar （40)**|存储在消息中的事务 ID（如果适用）。|  
|**transaction_status**|**int**|事务的状态。|  
|**transactions_processed**|**int**|会话中处理的事务的累计数量。|  
|**commands_processed**|**int**|会话中处理的命令的累计数量。|  
|**delivery_rate**|**float(53)**|每秒传送的平均命令数。|  
|**transaction_rate**|**float(53)**|事务处理速率。|  
|**订阅服务器**|**sysname**|订阅服务器的名称。|  
|**subscriberdb**|**sysname**|订阅数据库的名称。|  
|**error_id**|**int**|如果不是零，数字表示[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误消息。|  
|**timestamp**|**timestamp**|表的时间戳列。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
