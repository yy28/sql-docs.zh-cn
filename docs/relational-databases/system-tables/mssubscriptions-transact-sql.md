---
title: MSsubscriptions (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 05f5100843227093cd11909adede12f449cf0051
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33007754"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscriptions**表包含一个行，每个订阅由本地分发服务器提供服务中发布文章的。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID。|  
|**publisher_id**|**int**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**publication_id**|**int**|发布 ID。|  
|**article_id**|**int**|文章的 ID。|  
|**subscriber_id**|**int**|订阅服务器 ID。|  
|**subscriber_db**|**sysname**|订阅数据库的名称。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> **0** = 推送。<br /><br /> **1** = 请求。<br /><br /> **2** = 匿名。|  
|**sync_type**|**tinyint**|同步类型：<br /><br /> **1** = automatic。<br /><br /> **2** = 不同步。|  
|**status**|**tinyint**|订阅的状态：<br /><br /> **0** = 处于非活动状态。<br /><br /> **1** = 订阅。<br /><br /> **2** = 活动。|  
|**subscription_seqno**|**varbinary(16)**|快照事务序列号。|  
|**snapshot_seqno_flag**|**bit**|其中的一个值，该值指示快照事务序列号，源**1**意味着**subscription_seqno**是快照序列号。|  
|**independent_agent**|**bit**|表明该发布是否有独立的分发代理。|  
|**subscription_time**|**datetime**|仅限内部使用。|  
|**loopback_detection**|**bit**|适用于作为双向事务复制拓扑的一部分的订阅。 环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **1** = 不发回。<br /><br /> **0**回 = 发送。<br /><br /> 注意： 此列仅支持具有双向复制功能中的向后兼容性[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 对于更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，应改为使用对等复制。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
|**agent_id**|**int**|代理的 ID。|  
|**update_mode**|**tinyint**|更新的类型。|  
|**publisher_seqno**|**varbinary(16)**|该订阅在发布服务器上的事务序列号。|  
|**ss_cplt_seqno**|**varbinary(16)**|用于表示并发快照处理已完成的序列号。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
