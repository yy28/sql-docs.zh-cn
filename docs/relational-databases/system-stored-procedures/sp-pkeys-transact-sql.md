---
title: sp_pkeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e29c05d862f9f8bb391bef7a515db66ba70fb2ad
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43090057"
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回当前环境中单个表的主键信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @table_name=] '*名称*  
 是要为其返回信息的表。 *名称*是**sysname**，无默认值。 不支持通配符模式匹配。  
  
 [ @table_owner=] '*所有者*  
 为指定的表指定所有者。 *所有者*是**sysname**，默认值为 NULL。 不支持通配符模式匹配。 如果*所有者*未指定，则遵循基础 dbms 的默认表可见性规则将应用。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果当前用户拥有一个具有指定名称的表，则返回该表的列。 如果*所有者*未指定当前用户不拥有具有指定的表和*名称*，此过程使用指定的表查找*名称*归数据库所有者。 如果存在，则返回该表的列。  
  
 [ @table_qualifier=] '*限定符*  
 表限定符。 *限定符*是**sysname**，默认值为 NULL。 多种 DBMS 产品支持表的三部分命名 (*限定符 ***。*** 所有者 ***。*** 名称*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示数据库名称。 在某些产品中，它表示表所在数据库环境的服务器名称。  
  
## <a name="return-code-values"></a>返回代码值  
 None  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|表限定符的名称。 此字段可以为 NULL。|  
|TABLE_OWNER|**sysname**|表所有者的名称。 此字段始终返回值。|  
|TABLE_NAME|**sysname**|表的名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，该列表示在 sysobjects 表中列出的表名。 此字段始终返回值。|  
|COLUMN_NAME|**sysname**|返回的 TABLE_NAME 中每一列的列名。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，该列表示在 sys.columns 表中列出的列名。 此字段始终返回值。|  
|KEY_SEQ|**smallint**|多列主键中列的序列号。|  
|PK_NAME|**sysname**|主键标识符。 如果对数据源不适用，则返回 NULL。|  
  
## <a name="remarks"></a>Remarks  
 sp_pkeys 返回使用 PRIMARY KEY 约束显式定义的列的信息。 由于不是所有的系统均支持显式命名的主键，因此由网关实现者决定主键的构成。 请注意主键这一术语指的是表的逻辑主键。 应对被列为逻辑主键的每个键定义一个唯一索引。 此唯一索引也会由 sp_statistics 返回。  
  
 等效于 ODBC 中的 SQLPrimaryKeys sp_pkeys 存储过程。 返回的结果按 TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME 和 KEY_SEQ 排序。  
  
## <a name="permissions"></a>Permissions  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例检索 `HumanResources.Department` 数据库中 `AdventureWorks2012` 表的主键。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例检索 `DimAccount` 数据库中 `AdventureWorksPDW2012` 表的主键。 它将返回零行，该值指示表没有主键。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>请参阅  
 [目录存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

