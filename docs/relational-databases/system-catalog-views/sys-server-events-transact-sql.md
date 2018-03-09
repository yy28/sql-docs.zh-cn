---
title: "sys.server_events (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbacdd3b1f3943906be711c64f2368c4a5e7a779
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysserverevents-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含的每一行都对应于要为其激发服务器级事件通知或服务器级 DDL 触发器的一个事件。 列**object_id**和**类型**唯一标识服务器事件。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|要激发的服务器级事件通知或服务器级 DDL 触发器的 ID。|  
|**type**|**int**|导致激发事件通知或 DDL 触发器的事件的类型。|  
|**type_desc**|**nvarchar(60)**|对导致激发 DDL 触发器或事件通知的事件的说明。|  
|**event_group_type**|**int**|要对其创建触发器或事件通知的事件组，如果未对事件组中创建触发器或事件通知，则为 Null。|  
|**event_group_type_desc**|**nvarchar(60)**|要对其创建触发器或事件通知的事件组的说明，如果未对事件组创建触发器或事件通知，则为 Null。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
