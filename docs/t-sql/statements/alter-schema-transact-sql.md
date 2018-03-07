---
title: "ALTER 架构 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 30ef553ccfba1f30be9b75f8d0290115be395925
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在架构之间传输安全对象。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 是在当前数据库中，在其中对安全对象将被移动的名称。 其数据类型不能为 SYS 或 INFORMATION_SCHEMA。  
  
 \<entity_type>  
 更改其所有者的实体的类。 Object 是默认值。  
  
 *securable_name*  
 是安全对象移动到架构的架构范围的一部分或两个部分构成的名称。  
  
## <a name="remarks"></a>注释  
 用户与架构完全分离。  
  
 ALTER SCHEMA 仅可用于在同一数据库中的架构之间移动安全对象。 若要更改或删除架构中的安全对象，请使用特定于该安全对象的 ALTER 或 DROP 语句。  
  
 如果一个部分名称用于*securable_name*，名称解析规则当前实际上将用于查找对安全对象。  
  
 将安全对象移入新架构时，将删除与该安全对象关联的全部权限。 如果已显式设置安全对象的所有者，则该所有者保持不变。 如果安全对象的所有者已设置为 SCHEMA OWNER，则该所有者将保持为 SCHEMA OWNER；但移动之后，SCHEMA OWNER 将解析为新架构的所有者。 新所有者的 principal_id 将为 NULL。  
  
 移动存储的过程、 函数、 视图或触发器不会更改架构名称，如果存在，则相应对象的定义列在[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目录视图或使用获取[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)内置函数。 因此，我们建议，ALTER SCHEMA 不用于移动这些对象类型。 相反，除去并重新创建其新的架构中的对象。  
  
 移动如表或同义词的对象不会自动更新对该对象的引用。 您必须修改任何手动引用传输的对象的对象。 例如，如果移动表和触发器中引用该表，则必须修改触发器以反映新的架构名称。 使用[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)之前将其移动列表对象上的依赖项。  

 若要使用更改的表架构[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器，右键单击该表，然后单击**设计**。 按**F4**以打开属性窗口。 在**架构**框中，选择新的架构。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>权限  
 若要从另一个架构中传输安全对象，当前用户必须拥有对该安全对象（非架构）的 CONTROL 权限，并拥有对目标架构的 ALTER 权限。  
  
 如果对安全对象在其上具有 EXECUTE AS OWNER 规范并且的所有者设置为架构所有者，用户还必须在目标架构的所有者具有 IMPERSONATE 权限。  
  
 在移动安全对象后，将删除与所传输的安全对象相关联的所有权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-transferring-ownership-of-a-table"></a>A. 传递表的所有权  
 以下示例通过将表 `HumanResources` 从架构 `Address` 传输到 `Person` 架构来修改该架构。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. 传递类型的所有权  
 以下示例在 `Production` 架构中创建一个类型，然后将该类型传递到 `Person` 架构。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [varchar](10) NOT NULL ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
  
-- Change the type to the Person schema.  
ALTER SCHEMA Person TRANSFER type::Production.TestType ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. 传递表的所有权  
 下面的示例创建一个表`Region`中`dbo`架构，创建`Sales`架构，然后移动`Region`表从`dbo`架构`Sales`架构。  
  
```  
CREATE TABLE dbo.Region   
    (Region_id int NOT NULL,  
    Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [删除架构 &#40;Transact SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

