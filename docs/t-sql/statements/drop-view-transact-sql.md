---
title: "删除视图 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8dedeff21f56659d0cc55eef2d133a1ecbe0f63e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  从当前数据库中删除一个或多个视图。 可对索引视图执行 DROP VIEW。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)， [!INCLUDE[sssds](../../includes/sssds-md.md)])。 |  
  
 有条件地删除视图，仅当它已存在。  
  
 *schema_name*  
 视图所属架构的名称。  
  
 *view_name*  
 是要删除的视图的名称。  
  
## <a name="remarks"></a>注释  
 删除视图时，将从系统目录中删除视图的定义和有关视图的其他信息。 还将删除视图的所有权限。  
  
 使用 DROP TABLE 删除的表上的任何视图都必须使用 DROP VIEW 显式删除。  
  
 对索引视图执行 DROP VIEW 时，将自动删除视图上的所有索引。 若要在视图上显示的所有索引，使用[sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)。  
  
 通过视图进行查询时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将进行检查以确保语句中引用的所有数据库对象都存在，这些对象在语句的上下文中有效，以及数据修改语句没有违反任何数据完整性规则。 如果检查失败，将返回错误消息。 如果检查成功，则将操作转换为对基础表的操作。 如果基础表或视图自最初创建视图以来已发生更改，则删除并重新创建视图可能很有用。  
  
 有关确定特定的视图的依赖关系的详细信息，请参阅[sys.sql_dependencies &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 有关查看视图的文本的详细信息，请参阅[sp_helptext &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要**控件**在视图中，权限**ALTER**包含视图中或中的成员身份的架构权限**db_ddladmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-drop-a-view"></a>A. 删除视图  
 以下示例删除视图 `Reorder`。  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [使用 &#40;Transact SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 

