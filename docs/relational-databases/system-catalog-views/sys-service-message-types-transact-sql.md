---
title: sys.service_message_types (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c07fbfe3af83a014ce3a4c92a73d7d96b4aaf0a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Service Broker 中注册的每个消息类型都在该目录视图中占一行。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|消息类型的名称，在数据库中是唯一的。 不可为 NULL。|  
|**message_type_id**|**int**|消息类型的标识符，在数据库中是唯一的。 不可为 NULL。|  
|**principal_id**|**int**|拥有该消息类型的数据库主体的标识符。 可以为 NULL。|  
|**validation**|**char(2)**|在发送该类型的消息之前由 Broker 执行的验证。 不可为 NULL。 可为下列值之一：<br /><br /> N = 无<br /><br /> X = XML<br /><br /> E = 空|  
|**validation_desc**|**nvarchar(60)**|在发送该类型的消息之前由 Broker 执行的验证的说明。 可以为 NULL。 可为下列值之一：<br /><br /> 无<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|对于使用 XML 架构的验证，使用该架构集合的标识符。<br /><br /> 否则，为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
