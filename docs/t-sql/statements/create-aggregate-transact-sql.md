---
title: "创建聚合 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad5cf36e97bf3903cc9d42ec5179de6375624f95
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建用户定义聚合函数，其实现是在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的程序集类中定义的。 对于要将聚合函数绑定到其实现的[!INCLUDE[ssDE](../../includes/ssde-md.md)]，必须首先使用 CREATE ASSEMBLY 语句将包含该实现的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 程序集上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 用户定义聚合函数所属的架构的名称。  
  
 *aggregate_name*  
 要创建的聚合函数的名称。  
  
 **@***param_name*  
 用户定义聚合函数中的一个或多个参数。 在执行聚合函数时，用户必须提供参数的值。 通过使用"at"符号指定参数名称 (**@**) 作为第一个字符。 参数名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 该函数的参数是局部参数。  
  
 *system_scalar_type*  
 要存放输入参数值或返回值的任一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统标量数据类型。 所有标量数据类型可作为参数对于用户定义的聚合，除**文本**， **ntext**，和**映像**。 标量类型，如**光标**和**表**，不能指定。  
  
 *udt_schema_name*  
 CLR 用户定义类型所属的架构的名称。 如果未指定，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引用*udt_type_name*按以下顺序：  
  
-   本机 SQL 类型命名空间。  
  
-   当前数据库中当前用户的默认架构。  
  
-   当前数据库中的 **dbo** 架构。  
  
 *udt_type_name*  
 当前数据库中已创建的 CLR 用户定义类型的名称。 如果*udt_schema_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假定该类型属于当前用户的架构。  
  
 *程序集 _ 名称*[ **。***class_name* ]  
 指定与用户定义的聚合函数绑定在一起的程序集以及（可选）该程序集所属的架构名称和该程序集中实现该用户定义聚合函数的类名称。 必须先使用 CREATE ASSEMBLY 语句在数据库中创建了该程序集。 *class_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符和匹配的程序集中存在的类的名称。 *class_name*可能是命名空间限定名称，如果使用编写类的编程语言使用命名空间，如 C#。 如果*class_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假定它是与相同*aggregate_name*。  
  
## <a name="remarks"></a>注释  
 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法运行 CLR 代码。 你可以创建、 修改和删除引用托管的代码模块的数据库对象，但这些模块中的代码将不会运行的实例中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非[clr enabled 选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)通过使用[sp_配置](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 在引用的程序集的类*程序集 _ 名称*，其方法中，应该可满足所有的用户定义的聚合函数的实例中的实现的要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[clr 用户定义聚合](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 CREATE AGGREGATE 权限以及对 EXTERNAL NAME 子句中指定的程序集的 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
 下面的示例假定编译了 StringUtilities.csproj 示例应用程序。 有关详细信息，请参阅[字符串实用工具函数示例](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c)。  
  
 该示例创建聚合函数 `Concatenate`。 在创建该聚合函数之前，在本地数据库中注册了程序集 `StringUtilities.dll`。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [删除聚合 &#40;Transact SQL &#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  

