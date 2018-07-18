---
title: sys.transmission_queue (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04a1eb9729cf819d8c01fe1cc20fd963379d9fc4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221648"
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此目录视图中的每一行对应于传输队列中的一条消息，如下表所示：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|此消息所属会话的标识符。 不可为 NULL。|  
|**to_service_name**|**nvarchar(256)**|此消息要发送到的服务的名称。 可以为 NULL。|  
|**to_broker_instance**|**nvarchar(128)**|承载此消息要发送到的服务的 Broker 名称。 可以为 NULL。|  
|**from_service_name**|**nvarchar(256)**|发送此消息的服务的名称。 可以为 NULL。|  
|**service_contract_name**|**nvarchar(256)**|此消息的会话所遵循的约定名称。 可以为 NULL。|  
|**enqueue_time**|**datetime**|消息进入队列的时间。 无论实例的本地时区如何，该值都使用 UTC。 不可为 NULL。|  
|**message_sequence_number**|**bigint**|消息的序列号。 不可为 NULL。|  
|**message_type_name**|**nvarchar(256)**|消息的消息类型名称。 可以为 NULL。|  
|**is_conversation_error**|**bit**|此消息是否是错误消息。<br /><br /> 0 = 不是错误消息。<br /><br /> 1 = 是错误消息。<br /><br /> 不可为 NULL。|  
|**is_end_of_dialog**|**bit**|此消息是否是会话消息的结尾。 不可为 NULL。<br /><br /> 0 = 不是会话消息的结尾。<br /><br /> 1 = 是会话消息的结尾。<br /><br /> 不可为 NULL。|  
|**message_body**|**varbinary(max)**|此消息的正文。 可以为 NULL。|  
|**transmission_status**|**nvarchar(4000)**|此消息位于队列中的原因。 这通常是一条错误消息，说明未能发送该消息的原因。 如果为空白，则尚未发送此消息。 可以为 NULL。|  
|**priority**|**tinyint**|为此消息指定的优先级。 不可为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
