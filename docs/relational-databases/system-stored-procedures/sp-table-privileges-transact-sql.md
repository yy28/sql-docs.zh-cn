---
title: sp_table_privileges (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9d2863e17258fd0dea68548a15c059676c745424
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定的一个或多个表的表权限（如 INSERT、DELETE、UPDATE、SELECT、REFERENCES）的列表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @table_name=] '*table_name*  
 用来返回目录信息的表。 *table_name*是**nvarchar (** 384 **)**，无默认值。 支持通配符模式匹配。  
  
 [ @table_owner=] '*table_owner*  
 是用于返回目录信息的表所有者。 *table_owner*是**nvarchar (** 384 **)**，默认值为 NULL。 支持通配符模式匹配。 如果未指定所有者，则遵循基础 DBMS 的默认表可见性规则。  
  
 如果当前用户拥有一个具有指定名称的表，则返回该表的列。 如果*所有者*未指定当前用户不拥有具有指定的表和*名称*，此过程查找具有指定的表*table_name*归数据库所有者。 如果存在，则返回该表的列。  
  
 [ @table_qualifier=] '*table_qualifier*  
 表限定符的名称。 *table_qualifier*是**sysname**，默认值为 NULL。 各种 DBMS 产品支持三部分命名表 (*qualifier.owner.name*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示的数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。  
  
 [ @fUsePattern=] '*fUsePattern*  
 确定下划线 (_)、百分号 (%) 和方括号（[ 或 ]）是否解释为通配符。 有效值为 0（模式匹配为关闭状态）和 1（模式匹配为打开状态）。 *fUsePattern*是**位**，默认值为 1。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|表限定符名称。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示的数据库名称。 此字段可以为 NULL。|  
|TABLE_OWNER|**sysname**|表所有者名称。 此字段始终返回值。|  
|TABLE_NAME|**sysname**|表名。 此字段始终返回值。|  
|GRANTOR|**sysname**|已向列出的 GRANTEE 授予对此 TABLE_NAME 的权限的数据库用户名。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此列始终与 TABLE_OWNER 相同。 此字段始终返回值。 同样，GRANTOR 列可能是数据库所有者 (TABLE_OWNER)，或由数据库所有者使用 GRANT 语句中的 WITH GRANT OPTION 子句授予权限的用户。|  
|GRANTEE|**sysname**|已被列出的 GRANTOR 授予对此 TABLE_NAME 的权限的数据库用户名。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列始终包含从 sys.database_principalssystem 视图的数据库用户。 此字段始终返回值。|  
|PRIVILEGE|**sysname**|可用的表权限之一。 表权限可以是下列值之一（或在定义实现时数据源所支持的其他值）：<br /><br /> SELECT = GRANTEE 可以检索一列或多列的数据。<br /><br /> INSERT = GRANTEE 可为一列或多列的新行提供数据。<br /><br /> UPDATE = GRANTEE 可为一列或多列修改现有数据。<br /><br /> DELETE = GRANTEE 可从表中删除行。<br /><br /> REFERENCES = GRANTEE 可以用主键/外键关系引用外表中的列。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，主键/外键关系是使用表约束来定义的。<br /><br /> 由给定的表特权给予 GRANTEE 的操作的作用域是由数据源决定的。 例如，UPDATE 特权可能允许 GRANTEE 更新一个数据源的表中的所有列，而只允许 GRANTOR 更新另一数据源中它具有 UPDATE 特权的特定列。|  
|IS_GRANTABLE|**sysname**|指示是否允许 GRANTEE 向其他用户授权（通常称为“再授权”(grant with grant) 权限）。 可以是 YES、NO 或 NULL。 未知（或 NULL）值是指不适用“再授权”的数据源。|  
  
## <a name="remarks"></a>注释  
 sp_table_privileges 存储过程与 ODBC 中的 SQLTablePrivileges 等同。 返回结果按 TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME 和 PRIVILEGE 顺序排列。  
  
## <a name="permissions"></a>权限  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回其名称以单词 `Contact` 开头的所有表的特权信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>另请参阅  
 [目录存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
