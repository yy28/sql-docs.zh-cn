---
title: "ALTER VIEW (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
ms.assetid: 03eba220-13e2-49e3-bd9d-ea9df84dc28c
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 006b9fce1e13833c977d26d4bc0f13a602f2c96c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-view-transact-sql"></a>ALTER VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改先前创建的视图。 其中包括索引视图。 ALTER VIEW 不影响相关的存储过程或触发器，并且不会更改权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER VIEW [ schema_name . ] view_name [ ( column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ] [ ; ]  
  
<view_attribute> ::=   
{   
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 视图所属架构的名称。  
  
 *view_name*  
 要更改的视图。  
  
 *列*  
 将成为指定视图的一部分的一个或多个列的名称（以逗号分隔）。  
  
> [!IMPORTANT]  
>  只有在 ALTER VIEW 执行前后列名称不变的情况下，列的权限才会保持不变。  
  
> [!NOTE]  
>  在视图的各列中，列名的权限在 CREATE VIEW 或 ALTER VIEW 语句间均适用，与基础数据源无关。 例如，如果在授予权限**SalesOrderID** CREATE VIEW 语句中的列，ALTER VIEW 语句可以重命名**SalesOrderID**列，如与**OrderRef**，仍然具有关联视图使用权限和**SalesOrderID**。  
  
 ENCRYPTION  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 加密中的条目[sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md)包含 ALTER VIEW 语句的文本。 WITH ENCRYPTION 可防止视图作为 SQL Server 复制的一部分进行发布。  
  
 SCHEMABINDING  
 将视图绑定到基础表的架构。 如果指定了 SCHEMABINDING，则不能以可影响视图定义的方式来修改基表。 必须首先修改或删除视图定义本身，然后才能删除要修改的表的相关性。 当你使用 SCHEMABINDING， *select_statement*必须包含两部分名称 (*架构***。***对象*) 的表、 视图或引用的用户定义函数。 所有被引用对象都必须在同一个数据库内。  
  
 不能删除参与使用 SCHEMABINDING 子句创建的视图的表或视图，除非该视图已被删除或更改，而不再具有架构绑定。 否则，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误。 另外，如果对参与具有架构绑定的视图的表执行 ALTER TABLE 语句，而这些语句又会影响视图定义，则这些语句将会失败。  
  
 VIEW_METADATA  
 指定为引用视图的查询请求浏览模式的元数据时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将向 DB-Library、ODBC 和 OLE DB API 返回有关视图的元数据信息，而不返回基表的元数据信息。 浏览模式的元数据是[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例返回到客户端 DB-Library、ODBC 和 OLE DB API 的额外元数据。 如果使用此元数据，客户端 API 将可以实现可更新客户端游标。 浏览模式的元数据包含结果集中的列所属的基表的相关信息。  
  
 对于使用 VIEW_METADATA 创建的视图，浏览模式的元数据在描述结果集内视图中的列时，将返回视图名，而不返回基表名。  
  
 使用与 VIEW_METADATA，与其所有列中，创建一个视图时除外**时间戳**列中，是否可更新，如果此视图具有插入或更新 INSTEAD OF 触发器。 有关详细信息，请参阅备注部分中的[创建的视图 &#40;Transact SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 AS  
 视图要执行的操作。  
  
 *select_statement*  
 定义视图的 SELECT 语句。  
  
 WITH CHECK OPTION  
 强制执行针对视图遵循中设置的条件的所有数据修改语句*select_statement*。  
  
## <a name="remarks"></a>注释  
 有关 ALTER VIEW 的详细信息，请参阅中的备注[创建的视图 &#40;Transact SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
> [!NOTE]  
>  如果原来的视图定义是使用 WITH ENCRYPTION 或 CHECK OPTION 创建的，则只有在 ALTER VIEW 中也包含这些选项时，才会启用这些选项。  
  
 如果当前所用的视图使用 ALTER VIEW 来修改，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用对该视图的排他架构锁。 在授予锁时，如果该视图没有活动用户，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将从过程缓存中删除该视图的所有副本。 引用该视图的现有计划将继续保留在缓存中，但一旦被调用就会重新编译。  
  
 ALTER VIEW 可应用于索引视图；但是，ALTER VIEW 会无条件地删除视图的所有索引。  
  
## <a name="permissions"></a>Permissions  
 若要执行 ALTER VIEW，至少需要具有对 OBJECT 的 ALTER 权限。  
  
## <a name="examples"></a>示例  
 以下示例创建一个包含所有雇员及其雇佣日期（称为 `EmployeeHireDate`）的视图。 为该视图授予权限，但是要求更改为选择雇佣日期在某个日期之前的雇员。 然后，使用 `ALTER VIEW` 替换该视图。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
 必须将视图更改为只包括在 `2002` 年之前雇佣的雇员。 如果未使用 ALTER VIEW，而是删除并重新创建视图，则必须重新输入先前用来处理与视图有关的权限的 GRANT 语句和任何其他语句。  
  
```  
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)   
 [删除视图 &#40;Transact SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [创建存储过程](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  

