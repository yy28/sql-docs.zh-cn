---
title: "ALTER 架构 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs: TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: bcbc6cf4ed18bef5d4736375dd7eddaaa1167a33
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
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
  
 \<实体类型 >  
 更改其所有者的实体的类。 Object 是默认值。  
  
 *securable_name*  
 要移入架构中的架构包含安全对象的一部分或两部分名称。  
  
## <a name="remarks"></a>注释  
 用户与架构完全分离。  
  
 ALTER SCHEMA 仅可用于在同一数据库中的架构之间移动安全对象。 若要更改或删除架构中的安全对象，请使用特定于该安全对象的 ALTER 或 DROP 语句。  
  
 如果一个部分名称用于*securable_name*，名称解析规则当前实际上将用于查找对安全对象。  
  
 将安全对象移入新架构时，将删除与该安全对象关联的全部权限。 如果已显式设置安全对象的所有者，则该所有者保持不变。 如果安全对象的所有者已设置为 SCHEMA OWNER，则该所有者将保持为 SCHEMA OWNER；但移动之后，SCHEMA OWNER 将解析为新架构的所有者。 新所有者的 principal_id 将为 NULL。  
  
 若要使用更改表或视图的架构[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器，右键单击表或视图，然后单击**设计**。 按**F4**以打开属性窗口。 在**架构**框中，选择新的架构。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 若要从另一个架构中传输安全对象，当前用户必须拥有对该安全对象（非架构）的 CONTROL 权限，并拥有对目标架构的 ALTER 权限。  
  
 如果已为安全对象指定 EXECUTE AS OWNER，且所有者已设置为 SCHEMA OWNER，则用户还必须拥有对目标架构所有者的 IMPERSONATION 权限。  
  
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
 [创建架构 &#40;Transact SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [删除架构 &#40;Transact SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

