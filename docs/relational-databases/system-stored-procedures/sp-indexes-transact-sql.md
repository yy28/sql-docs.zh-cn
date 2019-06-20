---
title: sp_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b1a14d1cf8c9eac0ace93e3aac6e16219fd60eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62961909"
---
# <a name="spindexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定的远程表的索引信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @table_server= ] '*table_server*'  
 要为其请求表信息的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 链接服务器的名称。 *table_server*是**sysname**，无默认值。  
  
 [ @table_name= ] '*table_name*'  
 要为其提供索引信息的远程表的名称。 *table_name*是**sysname**，默认值为 NULL。 如果为 NULL，则返回指定数据库中的所有表。  
  
 [ @table_schema= ] '*table_schema*'  
 指定表架构。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中，该值对应于表所有者。 *table_schema*是**sysname**，默认值为 NULL。  
  
 [ @table_catalog= ] '*table_db*'  
 是在其中的数据库名称*table_name*驻留。 *table_db*是**sysname**，默认值为 NULL。 如果为 NULL， *table_db*默认值为**master**。  
  
 [ @index_name= ] '*index_name*'  
 为其请求信息的索引的名称。 *索引*是**sysname**，默认值为 NULL。  
  
 [ @is_unique= ] '*is_unique*'  
 要为其返回信息的索引的类型。 *is_unique*是**位**，默认值为 NULL，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|1|返回有关唯一索引的信息。|  
|0|返回有关非唯一索引的信息。|  
|NULL|返回有关所有索引的信息。|  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|指定的表所在的数据库的名称。|  
|TABLE_SCHEM|**sysname**|表的架构。|  
|TABLE_NAME|**sysname**|远程表的名称。|  
|NON_UNIQUE|**smallint**|指示索引是否唯一：<br /><br /> 0 = 唯一<br /><br /> 1 = 不唯一|  
|INDEX_QUALIFER|**sysname**|索引所有者的名称。 某些 DBMS 产品允许表所有者之外的用户创建索引。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列始终是相同**TABLE_NAME**。|  
|INDEX_NAME|**sysname**|索引的名称。|  
|TYPE|**smallint**|索引的类型：<br /><br /> 0 = 表的统计信息<br /><br /> 1 = 聚集<br /><br /> 2 = 哈希<br /><br /> 3 = 其他|  
|ORDINAL_POSITION|**int**|在索引中的列的序号位置。 索引中的第一列为 1。 该列始终返回值。|  
|COLUMN_NAME|**sysname**|返回的 TABLE_NAME 中每个列的对应列名。|  
|ASC_OR_DESC|**varchar**|排序规则中使用的顺序：<br /><br /> A = 升序<br /><br /> D = 降序<br /><br /> NULL = 不适用<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 始终返回 A。|  
|CARDINALITY|**int**|表中的行数或索引中唯一值的数目。|  
|PAGES|**int**|存储索引或表的页数。|  
|FILTER_CONDITION|**nvarchar(** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不返回值。|  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例将返回 `Employees` 链接服务器上 `AdventureWorks2012` 数据库的 `Seattle1` 表的所有索引信息。  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>请参阅  
 [分布式查询存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
