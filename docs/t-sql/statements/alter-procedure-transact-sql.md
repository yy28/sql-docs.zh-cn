---
title: "ALTER PROCEDURE (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_PROCEDURE_TSQL
- ALTER_PROC_TSQL
- ALTER PROC
- ALTER PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROCEDURE statement
- stored procedure modifications [SQL Server]
- modifying stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: ed9b2f76-11ec-498d-a95e-75b490a75733
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dc195d3f6ca908253ff5726c3f336435e7f2bd1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-procedure-transact-sql"></a>ALTER PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  修改先前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中通过执行 CREATE PROCEDURE 语句创建的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 (TRANSACT-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ VARYING ] [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Syntax for SQL Server CLR Stored Procedure  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameterdata_type } [= ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [ ; ] [ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 该过程所属的架构的名称。  
  
 *过程名称*  
 若要更改过程的名称。 过程名称必须符合 [标识符](../../relational-databases/databases/database-identifiers.md)规则。  
  
 **;** *数*  
 现有的可选整数，用于具有相同名称的组过程，以便可以通过使用一个 DROP PROCEDURE 语句一起删除它们。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 **@***参数*  
 该过程中的参数。 最多可以指定 2,100 个参数。  
  
 [ *type_schema_name***。** ] *data_type*  
 参数及其所属架构的数据类型。  
  
 有关数据类型限制的信息，请参阅[CREATE PROCEDURE &#40;Transact SQL &#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 VARYING  
 指定作为输出参数支持的结果集。 此参数由存储过程动态构造，并且其内容可以不同。 仅适用于游标参数。 该选项对于 CLR 过程无效。  
  
 *默认值*  
 参数的默认值。  
  
 OUT | OUTPUT  
 指示参数是返回参数。  
  
 READONLY  
 指示无法更新或在过程的正文内修改参数。 如果参数类型为表值类型，则必须指定 READONLY。  
  
 RECOMPILE  
 指示[!INCLUDE[ssDE](../../includes/ssde-md.md)]不会缓存该过程的计划，该过程在运行时重新编译。   
  
 ENCRYPTION  
 **适用于**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 和[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
 指示[!INCLUDE[ssDE](../../includes/ssde-md.md)]会将 ALTER PROCEDURE 语句的原始文本转换为模糊格式。 模糊处理的输出直接在中不可见的目录视图中的任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 对系统表或数据库文件没有访问权限的用户不能检索模糊文本。 但是，文本将可供既可以通过访问系统表的特权用户[DAC 端口](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)或直接访问数据库文件。 此外，能够向服务器进程附加调试器的用户可在运行时从内存中检索原始过程。 有关访问系统元数据的详细信息，请参阅[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
 使用此选项创建的过程不能作为的一部分发布[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制。  
  
 不能为公共语言运行时 (CLR) 存储过程指定此选项。  
  
> [!NOTE]  
>  升级过程中，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用存储在经过模糊处理的注释**sys.sql_modules**重新创建过程。  
  
 EXECUTE AS  
 指定访问存储过程后执行该存储过程所用的安全上下文。  
  
 有关详细信息，请参阅 [EXECUTE AS 子句 (Transact-SQL)](../../t-sql/statements/execute-as-clause-transact-sql.md)。  
  
 FOR REPLICATION  

  
 指定不能在订阅服务器上执行为复制创建的存储过程。 使用 FOR REPLICATION 选项创建的存储过程可用作存储过程筛选，且只能在复制过程中执行。 如果指定了 FOR REPLICATION，则无法声明参数。 该选项对于 CLR 过程无效。 对于使用 FOR REPLICATION 创建的过程，忽略 RECOMPILE 选项。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 {[BEGIN] *sql_statement* [;][ ... *n*  ] [结束]}  
 构成过程主体的一个或多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 您可以使用可选的 BEGIN 和 END 关键字将这些语句括起来。 有关详细信息，请参阅中的最佳做法，常规备注和限制和局限部分[CREATE PROCEDURE &#40;Transact SQL &#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 外部名称*程序集 _ 名称***。***class_name***。***method_name*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定的方法[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]CLR 的程序集存储过程来引用。 *class_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符，并且为程序集中的类必须存在。 如果类具有的命名空间限定的名称使用句点 (**。**) 来分隔命名空间部分，类名必须由使用方括号分隔 (**[]**) 或引号 (**""**). 指定的方法必须为该类的静态方法。  
  
 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能执行 CLR 代码。 你可以创建、 修改和删除引用公共语言运行时模块; 的数据库对象但是，无法执行中的这些引用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启用之前[clr enabled 选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。 若要启用该选项，使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
> [!NOTE]  
>  包含数据库中不支持 CLR 过程。  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程修改为 CLR 存储过程，反之亦然。  
  
 ALTER PROCEDURE 不会更改权限，也不影响相关的存储过程或触发器。 但是，当修改存储过程时，QUOTED_IDENTIFIER 和 ANSI_NULLS 的当前会话设置包含在该存储过程中。 如果设置不同于最初创建存储过程时有效的设置，则存储过程的行为可能会更改。  
  
 如果原来的过程定义是使用 WITH ENCRYPTION 或 WITH RECOMPILE 创建的，那么只有在 ALTER PROCEDURE 中也包含这些选项时，这些选项才有效。  
  
 有关存储过程的详细信息，请参阅[CREATE PROCEDURE &#40;Transact SQL &#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**ALTER**对该过程的权限或要求的成员身份**db_ddladmin**固定的数据库角色。  
  
## <a name="examples"></a>示例  
 以下示例将创建 `uspVendorAllInfo` 存储过程。 此过程返回提供 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的所有供应商的名称、所提供的产品、信用等级以及可用性。 创建过程之后，便可修改过程以返回不同的结果集。  
  
```  
  
IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE Purchasing.uspVendorAllInfo;  
GO  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 以下示例将更改 `uspVendorAllInfo` 存储过程。 该示例将删除 EXECUTE AS CALLER 子句并且将过程的主体修改为只返回那些提供指定产品的供应商。 `LEFT` 和 `CASE` 函数自定义结果集的外观。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER PROCEDURE Purchasing.uspVendorAllInfo  
    @Product varchar(25)   
AS  
    SET NOCOUNT ON;  
    SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
    'Rating' = CASE v.CreditRating   
        WHEN 1 THEN 'Superior'  
        WHEN 2 THEN 'Excellent'  
        WHEN 3 THEN 'Above average'  
        WHEN 4 THEN 'Average'  
        WHEN 5 THEN 'Below average'  
        ELSE 'No rating'  
        END  
    , Availability = CASE v.ActiveFlag  
        WHEN 1 THEN 'Yes'  
        ELSE 'No'  
        END  
    FROM Purchasing.Vendor AS v   
    INNER JOIN Purchasing.ProductVendor AS pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID   
    WHERE p.Name LIKE @Product  
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Vendor               Product name  Rating    Availability  
-------------------- ------------- -------   ------------  
Proseware, Inc.      LL Crankarm   Average   No  
Vision Cycles, Inc.  LL Crankarm   Superior  Yes  
(2 row(s) affected)`  
```  

## <a name="see-also"></a>另请参阅  
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [存储过程（数据库引擎）](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [与 sys.procedures &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)  
  
  

