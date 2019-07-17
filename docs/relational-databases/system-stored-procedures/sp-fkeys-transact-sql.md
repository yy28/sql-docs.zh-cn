---
title: sp_fkeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cb5f684321a11d56a419ae73be0bfb2950fb9939
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124402"
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回当前环境的逻辑外键信息。 此过程显示各种外键关系，包括禁用的外键。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @pktable_name=] '*pktable_name*  
 带主键的表的名称，用于返回目录信息。 *pktable_name*是**sysname**，默认值为 NULL。 不支持通配符模式匹配。 此参数或*fktable_name*必须提供参数，或同时。  
  
 [ @pktable_owner=] '*pktable_owner*  
 是用于返回目录信息 （带主键） 所有者的名称。 *pktable_owner*是**sysname**，默认值为 NULL。 不支持通配符模式匹配。 如果*pktable_owner*未指定，则遵循基础 dbms 的默认表可见性规则将应用。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果当前用户拥有具有指定名称的表，则返回该表的列。 如果*pktable_owner*未指定当前用户不拥有具有指定的表和*pktable_name*，该过程使用指定的表查找*pktable_name*由数据库所有者拥有。 如果有，则返回该表的列。  
  
 [ @pktable_qualifier =] '*pktable_qualifier*  
 是表 （带主键） 限定符的名称。 *pktable_qualifier*数据类型为 sysname，默认值为 NULL。 多种 DBMS 产品支持表的三部分命名 (*qualifier.owner.name*)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，限定符表示数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。  
  
 [ @fktable_name=] '*fktable_name*  
 用于返回目录信息的表（带外键）的名称。 *fktable_name*数据类型为 sysname，默认值为 NULL。 不支持通配符模式匹配。 此参数或*pktable_name*必须提供参数，或同时。  
  
 [ @fktable_owner =] '*fktable_owner*  
 用于返回目录信息的表（带外键）的所有者的名称。 *fktable_owner*是**sysname**，默认值为 NULL。 不支持通配符模式匹配。 如果*fktable_owner*未指定，则遵循基础 dbms 的默认表可见性规则将应用。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果当前用户拥有具有指定名称的表，则返回该表的列。 如果*fktable_owner*未指定当前用户不拥有具有指定的表和*fktable_name*，该过程使用指定的表查找*fktable_name*由数据库所有者拥有。 如果有，则返回该表的列。  
  
 [ @fktable_qualifier=] '*fktable_qualifier*  
 是表 （带外键） 限定符的名称。 *fktable_qualifier*是**sysname**，默认值为 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，限定符表示数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|表（带主键）限定符的名称。 此字段可以为 NULL。|  
|PKTABLE_OWNER|**sysname**|表（带主键）所有者的名称。 此字段始终返回值。|  
|PKTABLE_NAME|**sysname**|（带主键） 表的名称。 此字段始终返回值。|  
|PKCOLUMN_NAME|**sysname**|主键列的名称，针对返回的 TABLE_NAME 的每个列。 此字段始终返回值。|  
|FKTABLE_QUALIFIER|**sysname**|表（带外键）限定符的名称。 此字段可以为 NULL。|  
|FKTABLE_OWNER|**sysname**|表（带外键）所有者的名称。 此字段始终返回值。|  
|FKTABLE_NAME|**sysname**|（带外键） 表的名称。 此字段始终返回值。|  
|FKCOLUMN_NAME|**sysname**|外键列的名称，针对返回的 TABLE_NAME 的每个列。 此字段始终返回值。|  
|KEY_SEQ|**smallint**|多列主键中列的序列号。 此字段始终返回值。|  
|UPDATE_RULE|**smallint**|当 SQL 操作是更新操作时应用于外键的操作。  可能的值：<br /> 0=对外键的 CASCADE 更改。<br /> 1=NO ACTION 更改（如果有外键）。<br />   2 = 设置 null <br /> 3 = 设置默认值 |  
|DELETE_RULE|**smallint**|当 SQL 操作是删除操作时应用于外键的操作。 可能的值：<br /> 0=对外键的 CASCADE 更改。<br /> 1=NO ACTION 更改（如果有外键）。<br />   2 = 设置 null <br /> 3 = 设置默认值 |  
|FK_NAME|**sysname**|外键标识符。 如果不适用于数据源，则为 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回 FOREIGN KEY 约束名称。|  
|PK_NAME|**sysname**|主键标识符。 如果不适用于数据源，则为 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回 PRIMARY KEY 约束名称。|  
  
 返回的结果按 FKTABLE_QUALIFIER、 FKTABLE_OWNER、 FKTABLE_NAME 以及 KEY_SEQ 排序。  
  
## <a name="remarks"></a>备注  
 可以通过以下方法实现包含带禁用外键的表的应用程序编码：  
  
-   当使用这些表时，临时禁用约束检查（ALTER TABLE NOCHECK 或 CREATE TABLE NOT FOR REPLICATION），稍后再重新启用它。  
  
-   使用触发器或应用程序代码强制实施各种关系。  
  
如果提供了主键表名，而外键表名为 NULL，则 sp_fkeys 将返回包含了给定表外键的所有表。 如果提供了外键表名，而主键表名为 NULL，则 sp_fkeys 将返回通过主键/外键关系与外键表中的外键相关联的所有表。  
  
等效于 ODBC 中的 SQLForeignKeys sp_fkeys 存储过程。  
  
## <a name="permissions"></a>权限  
 需要`SELECT`拥有架构的权限。  
  
## <a name="examples"></a>示例  
 以下示例将为 `HumanResources.Department` 数据库中的 `AdventureWorks2012` 表检索一个外键的列表。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例将为 `DimDate` 数据库中的 `AdventureWorksPDW2012` 表检索一个外键的列表。 不返回任何行，因为[!INCLUDE[ssDW](../../includes/ssdw-md.md)]不支持外键。  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>请参阅  
 [目录存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

