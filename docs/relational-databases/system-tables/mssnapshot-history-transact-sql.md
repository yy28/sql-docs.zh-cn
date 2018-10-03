---
title: MSsnapshot_history (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 627e741c243b71d4e6b310f49b2f03091c4f9c63
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807675"
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_history**表包含与本地分发服务器关联的快照代理历史记录行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|快照代理的 ID。|  
|**runstatus**|**int**|运行状态：<br /><br /> **1** = 开始。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**start_time**|**datetime**|开始执行作业的时间。|  
|**time**|**datetime**|记录消息的时间。|  
|**duration**|**int**|消息会话的持续时间（秒）。|  
|**注释**|**nvarchar(255)**|消息文本。|  
|**delivered_transactions**|**int**|会话中传递的事务总数。|  
|**delivered_commands**|**int**|每秒传递的命令数。|  
|**delivery_rate**|**float(53)**|平均每秒传递的命令数。|  
|**error_id**|**int**|中的错误的 ID [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)系统表。|  
|**timestamp**|**timestamp**|该表的时间戳列。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
