---
title: MSdistribution_history (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f1db56fafb069836c7fa2ecd2f85cfac38ae548
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830208"
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdistribution_history**表包含与本地分发服务器关联的分发代理历史记录行。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|分发代理的 ID。|  
|**runstatus**|**int**|运行状态：<br /><br /> **1** = 开始。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**start_time**|**datetime**|开始执行作业的时间。|  
|**time**|**datetime**|记录消息的时间。|  
|**duration**|**int**|消息会话的持续时间（秒）。|  
|**注释**|**nvarchar(4000)**|消息文本。|  
|**xact_seqno**|**varbinary(16)**|上次处理的事务序列号。|  
|**current_delivery_rate**|**float**|自从最后一个历史记录条目后，平均每秒传送的命令数。|  
|**current_delivery_latency**|**int**|自从最后一个历史记录条目后，命令从进入分发数据库到应用于订阅服务器之间的滞后时间。 以毫秒为单位。|  
|**delivered_transactions**|**int**|会话中传递的事务总数。|  
|**delivered_commands**|**int**|在会话中传递的命令总数。|  
|**average_commands**|**int**|会话中传递的平均命令数。|  
|**delivery_rate**|**float**|平均每秒传递的命令数。|  
|**delivery_latency**|**int**|命令从进入分发数据库到应用于订阅服务器之间的滞后时间。 以毫秒为单位。|  
|**total_delivered_commands**|**bigint**|创建订阅后所传递的命令总数。|  
|**error_id**|**int**|中的错误的 ID **MSrepl_error**系统表。|  
|**updateable_row**|**bit**|设置为**1**如果可以覆盖历史记录行。|  
|**timestamp**|**timestamp**|该表的时间戳列。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
