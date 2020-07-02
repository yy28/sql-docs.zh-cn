---
title: sp_tables_ex （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36ac5833a4bf714c6f4b294f15f0cf6aca6fb64d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750426"
---
# <a name="sp_tables_ex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  返回有关指定链接服务器中表的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>自变量  
`[ @table_server = ] 'table_server'`要为其返回表信息的链接服务器的名称。 *table_server* **sysname**，无默认值。  
  
``[ , [ @table_name = ] 'table_name']``要为其返回数据类型信息的表的名称。 *table_name*的默认值为**sysname**，默认值为 NULL。  
  
`[ @table_schema = ] 'table_schema']`表架构。 *table_schema*的默认值为**sysname**，默认值为 NULL。  
  
`[ @table_catalog = ] 'table_catalog'`指定*table_name*所在的数据库的名称。 *table_catalog*的默认值为**sysname**，默认值为 NULL。  
  
`[ @table_type = ] 'table_type'`要返回的表的类型。 *table_type*的数据值为**sysname**，默认值为 NULL，可以具有以下值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**A**|别名。|  
|**GLOBAL TEMPORARY**|系统范围内可用的临时表的名称。|  
|**LOCAL TEMPORARY**|只限当前任务可用的临时表的名称。|  
|**同义词**|同义词的名称。|  
|**系统表**|系统表的名称。|  
|**系统视图**|系统视图的名称。|  
|**数据表**|用户表的名称。|  
|**显示**|视图的名称。|  
  
`[ @fUsePattern = ] 'fUsePattern'`确定字符 **_**、 **%** 、 **[** 和 **]** 是否解释为通配符。 有效值为 0（模式匹配为关闭状态）和 1（模式匹配为打开状态）。 *fUsePattern*的值为**bit**，默认值为1。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|表限定符名称。 各种 DBMS 产品支持表的三部分命名（_限定符_**。**_所有者_**。**_名称_）。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，此列表示数据库名称。 在某些其他产品中，该列表示表的数据库环境的服务器名。 此字段可以为 NULL。|  
|**TABLE_SCHEM**|**sysname**|表所有者名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此列表示创建该表的数据库用户的名称。 此字段始终返回值。|  
|**TABLE_NAME**|**sysname**|表名。 此字段始终返回值。|  
|**TABLE_TYPE**|**varchar(32)**|表、系统表或视图。|  
|**备注**|**varchar （254）**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不为此列返回值。|  
  
## <a name="remarks"></a>备注  
 **sp_tables_ex**通过查询与*table_server*对应的 OLE DB 提供程序的**IDBSchemaRowset**接口的 tables 行集来执行。 将*table_name*、 *table_schema*、 *table_catalog*和*列*参数传递到此接口，以限制返回的行数。  
  
 如果指定链接服务器的 OLE DB 提供程序不支持**IDBSchemaRowset**接口的表行集， **sp_tables_ex**将返回空结果集。  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回有关 `HumanResources` 链接服务器上 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中 `LONDON2` 架构包含的有关表的信息。  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>另请参阅  
 [分布式查询存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
