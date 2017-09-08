---
title: "EXECUTE AS 子句 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
caps.latest.revision: 70
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b96757281a5b36755422346ef444136ad8702726
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS 子句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可以定义以下用户定义模块的执行上下文：函数（内联表值函数除外）、过程、队列和触发器。  
  
 通过指定执行模块的上下文，可以控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)]使用哪一个用户帐户来验证对模块引用的对象的权限。 这有助于人们更灵活、有力地管理用户定义的模块及其所引用对象所形成的对象链中的权限。 必须而且只需授予用户对模块自身的权限，而无需授予用户对被引用对象的显式权限。 只有运行模块的用户必须对模块访问的对象拥有权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Windows Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>参数  
 **调用方**  
 指定模块内的语句在模块调用方的上下文中执行。 执行模块的用户不仅必须对模块本身拥有适当的权限，还要对模块引用的任何数据库对象拥有适当权限。  
  
 CALLER 是除队列外的所有模块的默认值，与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 行为相同。  
  
 CALLER 不能在 CREATE QUEUE 或 ALTER QUEUE 语句中指定。  
  
 **自助**  
 EXECUTE AS SELF 相当于 EXECUTE AS *user_name*，其中指定的用户是创建或更改模块的人员。 创建或修改的模块的人员的实际用户 ID 存储在**execute_as_principal_id**中的列**sys.sql_modules**或**sys.service_queues**目录视图。  
  
 SELF 是队列的默认值。  
  
> [!NOTE]  
>  若要更改的用户 ID **execute_as_principal_id**中**sys.service_queues**目录视图，则必须显式指定 EXECUTE 作为 ALTER QUEUE 语句中的设置。  
  
 OWNER  
 指定模块内的语句在模块的当前所有者上下文中执行。 如果模块没有指定的所有者，则使用模块架构的所有者。 不能为 DDL 或登录触发器指定 OWNER。  
  
> [!IMPORTANT]  
>  所有者必须映射到单一实例帐户，而且不能是角色或组。  
  
  *user_name*   
 指定模块中的语句中指定的用户的上下文中执行*user_name*。 针对验证的模块中的任何对象的权限*user_name*。 *user_name*不能为具有服务器作用域或登录触发器的 DDL 触发器指定。 使用*login_name*相反。  
  
 *user_name*当前数据库中必须存在并且必须是单独帐户。 *user_name*不能为组、 角色、 证书、 密钥或内置帐户，如 NT AUTHORITY\LocalService、 NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
 执行上下文的用户 ID 存储在元数据，并可以在中查看**execute_as_principal_id**中的列**sys.sql_modules**或**sys.assembly_modules**目录视图。  
  
  *login_name*   
 指定模块中的语句的上下文中执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的登录名*login_name*。 针对验证的模块中的任何对象的权限*login_name*。 *login_name*可以指定仅对具有服务器作用域或登录触发器的 DDL 触发器。  
  
 *login_name*不能为组、 角色、 证书、 密钥或内置帐户，如 NT AUTHORITY\LocalService、 NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]对模块所引用对象的权限进行评估的方式取决于调用对象和被引用对象之间存在的所有权链。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，所有权链是可以避免授权调用用户访问所有被引用对象权限的唯一方式。  
  
 所有权链具有以下限制：  
  
-   仅适用于 DML 语句：SELECT、INSERT、UPDATE 和 DELETE。  
  
-   调用和被调用对象的所有者必须相同。  
  
-   不适用于模块内的动态查询。  
  
 不论模块中指定的执行上下文如何，以下操作始终适用：  
  
-   执行模块时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]首先验证执行模块的用户是否拥有对模块的 EXECUTE 权限。  
  
-   所有权链规则继续应用。 这意味着如果调用和被调用对象的所有者相同，则不检查对基础对象的权限。  
  
 当某用户要执行已指定在 CALLER 之外的上下文中执行的模块时，系统将检查该用户是否有执行该模块的权限，但对该模块访问的对象的权限检查，则是针对 EXECUTE AS 子句中指定的用户帐户执行。 实际上，执行模块的用户将扮演指定的用户。  
  
 在模块的 EXECUTE AS 子句中指定的上下文，仅在模块执行期间有效。 模块执行完毕后，上下文反转为调用方。  
  
## <a name="specifying-a-user-or-login-name"></a>指定用户名或登录名  
 修改模块以便在其他上下文中执行前，不能删除模块的 EXECUTE AS 子句中指定的数据库用户或服务器登录。  
  
 EXECUTE AS 子句中指定的用户名或登录名作为中的主体必须存在**sys.database_principals**或**sys.server_principals**、 分别或其他创建或更改模块操作失败. 此外，创建或更改模块的用户必须拥有对主体的 IMPERSONATE 权限。  
  
 如果用户拥有通过 Windows 组成员身份隐式访问数据库或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的权限，并且满足以下要求之一，则创建模块时，也将隐式创建在 EXECUTE AS 子句中指定的用户：  
  
-   指定的用户或登录名为属于**sysadmin**固定的服务器角色。  
  
-   创建模块的用户拥有创建主体的权限。  
  
 如果这些要求都不满足，则创建模块的操作将失败。  
  
> [!IMPORTANT]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服务是使用本地帐户（本地服务或本地用户帐户）运行的，它将无权获取 EXECUTE AS 子句中指定的 Windows 域帐户的组成员身份。 这将导致模块的执行失败。  
  
 例如，假设条件如下：  
  
-   **CompanyDomain\SQLUsers**组具有访问权限**销售**数据库。  
  
-   **CompanyDomain\SqlUser1**为属于**SQLUsers** ，因此，有权**销售**数据库。  
  
-   创建或更改模块的用户拥有创建主体的权限。  
  
 当运行以下 `CREATE PROCEDURE` 语句时，将隐式创建 `CompanyDomain\SqlUser1` 作为 `Sales` 数据库中的数据库主体。  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>使用 EXECUTE AS CALLER 独立语句  
 使用模块内的 EXECUTE AS CALLER 独立语句将执行上下文设置为模块调用方。  
  
 假定 `SqlUser2` 调用以下存储过程。  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>使用 EXECUTE AS 定义自定义权限集  
 定义自定义权限集时，指定模块的执行上下文非常有用。 例如，某些操作，如 TRUNCATE TABLE，没有可授予的权限。 通过在模块内包含 TRUNCATE TABLE 语句并指定模块作为拥有更改该表权限的用户来执行，可以将截断表的权限扩展到被授予对该模块拥有 EXECUTE 权限的用户。  
  
 若要查看具有指定的执行上下文的模块的定义，请使用[sys.sql_modules &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目录视图。  
  
## <a name="best-practice"></a>最佳实践  
 指定拥有执行模块中定义的操作所需的最低权限的登录或用户。 例如，如果不需要相应的权限，则不要指定数据库所有者帐户。  
  
## <a name="permissions"></a>Permissions  
 若要执行使用 EXECUTE AS 指定的模块，调用方必须拥有对模块的 EXECUTE 权限。  
  
 若要执行使用 EXECUTE AS 指定的 CLR 模块（该模块将访问其他数据库或服务器资源），目标数据库或服务器必须信任从中派生模块的数据库（源数据库）的验证器。  
  
 若要在创建或修改模块时指定 EXECUTE AS 子句，必须对指定的主体拥有 IMPERSONATE 权限以及创建该模块的权限。 可以始终扮演自身。 当不指定任何执行上下文，或指定 EXECUTE AS CALLER 时，则无需 IMPERSONATE 权限。  
  
 若要指定*login_name*或*user_name*具有隐式访问通过 Windows 组成员身份的数据库，必须对数据库具有控制权限。  
  
## <a name="examples"></a>示例  
 以下示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中创建一个存储过程，并将执行上下文分配给 `OWNER`。  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.service_queues &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [还原 &#40;Transact SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
