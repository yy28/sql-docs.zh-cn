---
title: sys.dm_broker_forwarded_messages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87f471a91aad067dd1662f243cdbafd73d335979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099147"
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  针对每个 Service Broker 消息都返回一行，此消息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例正在转发中。  
  

|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|此消息所属会话的 ID。 可以为 NULL。|  
|**is_initiator**|**bit**|指示此消息是否来自会话的发起方。  可以为 NULL。<br /><br /> 0 = 不来自发起方<br /><br /> 1 = 来自发起方|  
|**to_service_name**|**nvarchar(512)**|此消息所发往的服务的名称。 可以为 NULL。|  
|**to_broker_instance**|**nvarchar(512)**|Broker 的标识符，该 Broker 承载此消息所发往的服务。 可以为 NULL。|  
|**from_service_name**|**nvarchar(512)**|发送此消息的服务的名称。 可以为 NULL。|  
|**from_broker_instance**|**nvarchar(512)**|承载发送此消息的服务的 Broker 的标识符。 可以为 NULL。|  
|**adjacent_broker_address**|**nvarchar(512)**|此消息发往的网络地址。 可以为 NULL。|  
|**message_sequence_number**|**bigint**|对话框中的消息的序列号。 可以为 NULL。|  
|**message_fragment_number**|**int**|如果对话消息分为多个片段，则它表示此传输消息包含的片段数。 可以为 NULL。|  
|**hops_remaining**|**tinyint**|消息在到达最终目标地址之前可能被重新传送的次数。 每次转发消息时，此数字都会减少 1。 可以为 NULL。|  
|**time_to_live**|**int**|消息保持活动状态的最长时间。 当该值为 0 时，表示放弃了消息。 可以为 NULL。|  
|**time_consumed**|**int**|消息已保持活动状态的时间。 每次转发消息时，该数字都会按照它转发消息所用的时间增加。 不可为 NULL。|  
|**message_id**|**uniqueidentifier**|消息的 ID。 可以为 NULL。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 Service Broker 有关的动态管理视图 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

