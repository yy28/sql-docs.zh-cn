---
title: sys.messages (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 07a5a426c0a2cf0b4b7c0385850471c3580d4fd3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178993"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>（错误） 的消息目录视图的 sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个表中占一行**message_id**或**language_id**在系统中，同时系统定义和用户定义消息的错误消息。 有关详细信息，请参阅 [sp_addmessage (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|消息的 ID。 此 ID 在服务器中是唯一的。 编号在 50000 以下的消息 ID 是系统消息。|  
|**language_id**|**int**|为其语言 ID 中的文本**文本**中定义使用**syslanguages**。 这是唯一的指定**message_id**。|  
|severity|**tinyint**|消息的严重级别，在 1 到 25 之间。 这等同于所有消息中的语言**message_id**。|  
|**is_event_logged**|**bit**|1 = 出现错误时将消息记入事件日志。 这等同于所有消息中的语言**message_id**。|  
|**text**|**nvarchar(2048)**|消息的文本时使用相应**language_id**处于活动状态。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [THROW (Transact-SQL)](../../t-sql/language-elements/throw-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [消息&#40;错误&#41;目录视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [异常消息框编程](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [错误消息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [数据库引擎错事件和错误](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
