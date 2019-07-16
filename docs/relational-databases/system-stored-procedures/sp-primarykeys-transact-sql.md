---
title: sp_primarykeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccae0385ef8c9305f4972ff6dcbd7a7960200370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056314"
---
# <a name="spprimarykeys-transact-sql"></a>sp_primarykeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定远程表的主键列，每个键列对应一行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @table_server = ] 'table_server'_` 是从中返回主键信息的链接服务器的名称。 *table_server*是**sysname**，无默认值。  
  
`[ @table_name = ] 'table_name'` 是要为其提供主键信息的名称。 *table_name*是**sysname**，默认值为 NULL。  
  
`[ @table_schema = ] 'table_schema'` 是表架构。 *table_schema*是**sysname**，默认值为 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中，该值对应于表所有者。  
  
`[ @table_catalog = ] 'table_catalog'` 是在其中的目录的名称指定*table_name*驻留。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中，该值对应于数据库名称。 *table_catalog*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|表目录。|  
|**TABLE_SCHEM**|**sysname**|表架构。|  
|**TABLE_NAME**|**sysname**|表的名称。|  
|**COLUMN_NAME**|**sysname**|列的名称。|  
|**KEY_SEQ**|**int**|多列主键中列的序列号。|  
|**PK_NAME**|**sysname**|主键标识符。 如果对数据源不适用，则返回 NULL。|  
  
## <a name="remarks"></a>备注  
 **sp_primarykeys**执行的查询的 PRIMARY_KEYS 行集**IDBSchemaRowset**对应的 OLE DB 访问接口*table_server*。 *Table_name*， *table_schema*， *table_catalog*，以及*列*参数传递给此接口的行进行限制返回。  
  
 **sp_primarykeys**返回空结果集，如果指定链接服务器的 OLE DB 访问接口不支持的 PRIMARY_KEYS 行集**IDBSchemaRowset**接口。  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中 `LONDON1` 表的 `HumanResources.JobCandidate` 服务器中的主键列。  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>请参阅  
 [分布式查询存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
