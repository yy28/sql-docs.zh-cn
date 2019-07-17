---
title: cdc.change_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4432d4c45bdecc6f5e1804427770d005adde0cd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081282"
---
# <a name="cdcchangetables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为数据库中的每个更改表返回一行。 对源表启用变更数据捕获时，将创建一个更改表。 我们建议您不要直接查询系统表， 而应执行[sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)存储过程。  
  |列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|更改表的 ID。 是在数据库中唯一。|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 对于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，此列始终返回 0。|  
|**source_object_id**|**int**|为变更数据捕获启用的源表的 ID。|  
|**捕获实例**|**sysname**|用于命名特定于实例的跟踪对象的捕获实例的名称。 默认情况下，该名称派生自从源架构名称加上源表名称的格式*schemaname_sourcename*。|  
|**start_lsn**|**binary(10)**|日志序列号 (LSN)，表示查询更改表中的更改数据时的低端点。<br /><br /> NULL = 尚未建立低端点。|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，此列始终返回 NULL。|  
|**supports_net_changes**|**bit**|对更改表启用了查询净更改支持。|  
|**has_drop_pending**|**bit**|捕获进程收到关于源表已被删除的通知。|  
|**role_name**|**sysname**|用于访问更改数据的数据库角色的名称。<br /><br /> NULL = 未使用角色。|  
|**index_name**|**sysname**|用于唯一标识源表中的行的索引名称。 **index_name**是源表的主键索引名称或唯一索引的名称指定当对源表启用变更数据捕获。<br /><br /> NULL = 在变更数据捕获启用时，源表无主键，且未指定唯一索引。<br /><br /> 注意:如果存在主键的表启用变更数据捕获，变更数据捕获功能将使用而不考虑是否启用净更改的索引。 启用变更数据捕获之后，将不允许对主键进行修改。 如果该表没有主键，则仍可以启用变更数据捕获，但是只能将净更改设置为 False。 启用变更数据捕获之后，即可以创建主键。 由于变更数据捕获功能不使用主键，因此还可以修改主键。|  
|**filegroup_name**|**sysname**|更改表所驻留的文件组的名称。<br /><br /> NULL = 更改表在数据库的默认文件组中。|  
|**create_date**|**datetime**|启用源表的日期。|  
|**partition_switch**|**bit**|指示是否**SWITCH PARTITION**命令**ALTER TABLE**可以对启用了变更数据捕获的表执行。 0 指示分区切换被阻止。 未分区表始终返回 1。|  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
