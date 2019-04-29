---
title: sp_depends (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f20945b6c4dc8fc1dda398c3dc9e721ff8b44d07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047161"
---
# <a name="spdepends-transact-sql"></a>sp_depends (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关数据库对象依赖关系的信息，例如，依赖于表或视图的视图和过程，以及视图或过程所依赖的表和视图。 不报告对当前数据库以外对象的引用。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)并[sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 数据库的名称。  
  
 *schema_name*  
 对象所属架构的名称。  
  
 *object_name*  
 要检查其依赖关系的数据库对象。 该对象可以是表、视图、存储过程、用户定义函数或触发器。 o*bject_name*是**nvarchar(776)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 **sp_depends**显示两个结果集。  
  
 下面的结果集显示的对象所在*\<对象 >* 取决于。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar(257** **)**|存在依赖项的项名称。|  
|**类型**|**nvarchar(16)**|项的类型。|  
|**updated**|**nvarchar(7)**|是否更新项。|  
|**selected**|**nvarchar(8)**|项是否用于 SELECT 语句。|  
|**column**|**sysname**|存在依赖项的列或参数。|  
  
 下面的结果集显示依赖于的对象*\<对象 >*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar(257** **)**|存在依赖项的项名称。|  
|**类型**|**nvarchar(16)**|项的类型。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. 列出表的依赖关系  
 以下示例列出在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中依赖于 `Sales.Customer` 表的数据库对象。 同时指定了架构名和表名。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. 列出触发器的依赖关系  
 以下示例列出 `iWorkOrder` 触发器所依赖的数据库对象。  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
