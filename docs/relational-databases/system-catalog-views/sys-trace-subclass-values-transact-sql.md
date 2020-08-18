---
description: sys.trace_subclass_values (Transact-SQL)
title: sys. trace_subclass_values (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_subclass_values
- trace_subclass_values_TSQL
- sys.trace_subclass_values_TSQL
- trace_subclass_values
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_subclass_values catalog view
ms.assetid: 542b19ca-61c8-41ca-aa2e-0aba8906cc24
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c13e9d2f1ce861a2240495f504e945141a01c12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400263"
---
# <a name="systrace_subclass_values-transact-sql"></a>sys.trace_subclass_values (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sys.databases. trace_subclass_values**目录视图包含一个命名列值列表。 在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的给定版本中，这些子类值不变。  
  
 有关支持的跟踪事件的完整列表，请参阅 [SQL Server 事件类引用](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件目录视图。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|跟踪事件的 ID。 此参数也在 **trace_events sys.databases** 目录视图中。|  
|**trace_column_id**|**smallint**|用于枚举的跟踪列的 ID。 此参数也在 **trace_columns sys.databases** 目录视图中。|  
|**subclass_name**|**nvarchar(128)**|列值的含义。|  
|**subclass_value**|**smallint**|列值。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys. trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys. trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys. trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)  
  
  
