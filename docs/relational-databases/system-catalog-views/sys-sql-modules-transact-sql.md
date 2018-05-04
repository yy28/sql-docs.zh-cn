---
title: sys.sql_modules (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 39c8e18600d075f4f5b7c1e39135291416cd025c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回每个对象都是一个 SQL 语言定义的模块中一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，包括本机编译标量用户定义函数。 类型为 P、RF、V、TR、FN、IF、TF 和 R 的对象均有关联的 SQL 模块。 在此视图中，独立的默认值，即 D 类型的对象也具有 SQL 模块定义。 有关这些类型的说明，请参阅**类型**中的列[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目录视图。  
  
 有关详细信息，请参阅[内存中 OLTP 的标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含对象的对象 ID。 是一个数据库中唯一的。|  
|**定义**|**nvarchar(max)**|定义此模块的 SQL 文本。 此外可以通过获取此值[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)内置函数。<br /><br /> NULL = 加密。|  
|**uses_ansi_nulls**|**bit**|模块是使用 SET ANSI_NULLS ON 创建的。<br /><br /> 对于规则和默认值，始终 = 0。|  
|**uses_quoted_identifier**|**bit**|模块是使用 SET QUOTED_IDENTIFIER ON 创建的。|  
|**is_schema_bound**|**bit**|模块已使用 SCHEMABINDING 选项创建。<br /><br /> 对于本机编译存储过程，始终包含值 1。|  
|**uses_database_collation**|**bit**|1 = 架构绑定模块定义取决于正确处理所需的数据库的默认排序规则；否则为 0。 这种相关性可防止更改数据库的默认排序规则。|  
|**is_recompiled**|**bit**|过程的创建 WITH RECOMPILE 选项。|  
|**null_on_null_input**|**bit**|模块被声明为针对任何 NULL 输入生成 NULL 输出。|  
|**execute_as_principal_id**|**Int**|EXECUTE AS 数据库主体的 ID。<br /><br /> 默认情况下，或者 EXECUTE AS CALLER 时，为 NULL。<br /><br /> 指定的主体如果 ID EXECUTE AS SELF 或 EXECUTE AS\<主体 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**uses_native_compilation**|**bit**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。<br /><br /> 0 = 非本机编译<br /><br /> 1 = 本机编译<br /><br /> 默认值为 0。|  
  
## <a name="remarks"></a>注释  
 在中找到默认约束，D，类型的对象的 SQL 表达式[sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)目录视图。 在中找到 CHECK 约束，C，类型的对象的 SQL 表达式[sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)目录视图。  
  
 中也介绍了此信息[sys.dm_db_uncontained_entities &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
 下面的示例返回当前数据库中每个模块的名称、类型和定义。  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
