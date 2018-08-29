---
title: sys.trigger_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1411dd697eafa0335a0e29fd8c55548397263b1b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078859"
---
# <a name="systriggerevents-transact-sql"></a>sys.trigger_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  激发触发器的每个事件对应一行。  
  
> [!NOTE]  
>  **sys.trigger_events**不适用于事件通知。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<从 sys.events 继承的列 >**|不适用|继承**object_id**，**类型**， **type_desc**中的列[sys.events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)。|  
|**is_first**|**bit**|触发器标记为第一个为此事件激发的触发器。|  
|**is_last**|**bit**|触发器标记为最后一个为此事件激发的触发器。|  
|**event_group_type**|**int**|要对其创建触发器的事件组，如果未对事件组创建触发器，则为 Null。|  
|**event_group_type**|**nvarchar(60)**|要对其创建触发器的事件组的说明，如果未对事件组创建触发器，则为 Null。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
