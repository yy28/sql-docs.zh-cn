---
title: "sp_table_privileges_ex (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0b117cb37d12eed86de59fec60eeaac84aef15e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sptableprivilegesex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关指定链接服务器中的指定表的特权信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>参数  
 [  **@table_server =** ] *table_server*  
 要返回信息的链接服务器的名称。 *table_server*是**sysname**，无默认值。  
  
 [  **@table_name =** ] *table_name*]  
 将为其提供表特权信息的表的名称。 *table_name*是**sysname**，默认值为 NULL。  
  
 [  **@table_schema =** ] *table_schema*  
 表架构。 在某些 DBMS 环境中是表所有者。 *table_schema*是**sysname**，默认值为 NULL。  
  
 [  **@table_catalog =** ] *table_catalog*  
 是在其中的数据库的名称指定*table_name*驻留。 *table_catalog*是**sysname**，默认值为 NULL。  
  
 [  **@fUsePattern =**] *fUsePattern*  
 确定字符 "_"、"%"、"[" 和 "]" 是否解释为通配符。 有效值为 0（模式匹配为关闭状态）和 1（模式匹配为打开状态）。 *fUsePattern*是**位**，默认值为 1。  
  
## <a name="return-code-values"></a>返回代码值  
 无  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|表限定符名称。 各种 DBMS 产品支持三部分命名表 (*限定符***。***所有者***。***名称*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列表示的数据库名称。 在某些产品中，该列表示表所在的数据库环境的服务器名。 此字段可以为 NULL。|  
|**TABLE_SCHEM**|**sysname**|表所有者名称。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此列表示创建该表的数据库用户的名称。 此字段始终返回值。|  
|**TABLE_NAME**|**sysname**|表名。 此字段始终返回值。|  
|**授权者**|**sysname**|已授予此权限的数据库用户名**TABLE_NAME**到列出**被授权者**。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此列始终是相同**TABLE_OWNER**。 此字段始终返回值。 此外，授权者该列可能是数据库所有者 (**TABLE_OWNER**) 或用户向其数据库所有者授予权限的 GRANT 语句中使用 WITH GRANT OPTION 子句。|  
|**被授权者**|**sysname**|已被授予此权限的数据库用户名**TABLE_NAME**通过列出**授权者**。 此字段始终返回值。|  
|**特权**|**varchar (**32**)**|可用的表权限之一。 表权限可以是以下值之一或定义实现时数据源支持的其他值：<br /><br /> 选择 =**被授权者**可以检索的一个或多个列的数据。<br /><br /> 插入 =**被授权者**可以为一个或多个列的新行提供数据。<br /><br /> 更新 =**被授权者**可以修改为一个或多个列的现有数据。<br /><br /> 删除 =**被授权者**可以从表中删除行。<br /><br /> 引用 =**被授权者**可以引用外部表中主键的键/外键关系中的列。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，主键/外键关系是使用表约束定义的。<br /><br /> 提供给操作的作用域**被授权者**通过特定的表权限是数据源相关。 例如，更新权限可能会使**被授权者**若要为其更新在一个数据源的表中的所有列和仅这些列**授权者**另一个数据源具有更新权限。|  
|**IS_GRANTABLE**|**varchar (**3**)**|指示是否**被授权者**允许向其他用户授予权限。 这常常称为“授予再授予”权限。 可以是 YES、NO 或 NULL。 未知的（或 NULL）值指不适用“授予再授予”的数据源。|  
  
## <a name="remarks"></a>注释  
 返回对结果进行排序的**TABLE_QUALIFIER**， **TABLE_OWNER**， **TABLE_NAME**，和**特权**。  
  
## <a name="permissions"></a>Permissions  
 需要对架构的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例从指定的链接数据库 `Product` 返回有关 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中名称以 `Seattle1` 开头的表的特权信息。 （[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 假定为链接服务器）。  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_column_privileges_ex &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分布式的查询存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
