---
title: sys. table_types （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e000d4e4f7f46d57bb1ae9a4e5c370169eb1227f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821309"
---
# <a name="systable_types-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的用户定义表类型的属性。 表类型是指无法从其中声明表变量或表值参数的类型。 每个表类型都有一个作为[sys.databases](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图中外键的**type_table_object_id** 。 您可以使用此 ID 列查询各种目录视图，其方式类似于常规表的**object_id**列，用于发现表类型的结构，如表的列和约束。    
 
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|*\<继承列>*||有关此视图所继承的列的列表，请参阅[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)。|  
|**type_table_object_id**|**int**|对象标识号。 此标识号在数据库中是唯一的。|  
|**is_memory_optimized**|**bit**|**适用于**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 及更高版本。<br /><br /> 下面是可能的值：<br /><br /> 0 = 非内存优化<br /><br /> 1 = 内存优化<br /><br /> 值 0 为默认值。<br /><br /> 表类型始终是用 DURABILITY = SCHEMA_ONLY 创建的。 只有架构保留在磁盘上。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [使用表值参数 &#40;数据库引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
