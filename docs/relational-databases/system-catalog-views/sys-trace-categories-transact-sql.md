---
description: sys.trace_categories (Transact-SQL)
title: sys. trace_categories (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_categories
- trace_categories_TSQL
- sys.trace_categories
- sys.trace_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_categories catalog view
ms.assetid: f6a86766-e2a9-4d9f-a073-1b59e888ba7d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c93fa579a54543ff1c08936796347c5bd1bc75d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88375013"
---
# <a name="systrace_categories-transact-sql"></a>sys.trace_categories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  将相似事件类按类别分组。 **Sys.databases. trace_categories**目录视图中的每一行标识一个在服务器中唯一的类别。 在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的给定版本中，这些类别不变。  
  
 有关支持的跟踪事件的完整列表，请参阅 [SQL Server 事件类引用](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
> **重要说明！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件目录视图。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**category_id**|**smallint**|此类别的唯一 ID。 此列也位于 **trace_events sys.databases** 目录视图中。|  
|**name**|**nvarchar(128)**|此类别的唯一名称。 此参数未本地化。|  
|type|**tinyint**|类别类型：<br /><br /> 0 = 正常<br /><br /> 1 = 连接<br /><br /> 2 = 错误|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys. trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys. trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys. trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
