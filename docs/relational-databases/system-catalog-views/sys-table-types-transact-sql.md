---
title: sys.table_types (TRANSACT-SQL) |Microsoft Docs
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
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fd03f2faea1d877ba755bfd53220e0690456f27
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079887"
---
# <a name="systabletypes-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的用户定义表类型的属性。 表类型是指无法从其中声明表变量或表值参数的类型。 每个表类型具有**type_table_object_id**的外键，它是[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图。 可以使用此 ID 列来查询各种目录视图，以类似于一种**object_id**常规表，以发现等的列和约束的表类型的结构列。    
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|*\<继承列 >*||此视图所继承的列的列表，请参阅[sys.types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)。|  
|**type_table_object_id**|**int**|对象标识号。 此标识号在数据库中是唯一的。|  
|**is_memory_optimized**|**bit**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 下面是可能的值：<br /><br /> 0 = 非内存优化<br /><br /> 1 = 内存优化<br /><br /> 值 0 为默认值。<br /><br /> 表类型始终是用 DURABILITY = SCHEMA_ONLY 创建的。 只有架构保留在磁盘上。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [使用表值参数（数据库引擎）](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
