---
title: "创建函数 （SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55f1b7e612a1c7d120e06078b0fdba45d6409d36
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-function-sql-data-warehouse"></a>创建函数 （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 中创建用户定义函数。 用户定义函数是[!INCLUDE[tsql](../../includes/tsql-md.md)]接受参数，例程执行的操作，例如复杂计算，并返回一个值作为该操作的结果。 返回值必须是标量 （单个） 值。 使用此语句可以创建可通过以下方式使用的重复使用的例程：  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（如 SELECT）中  
  
-   在调用该函数的应用程序中  
  
-   在另一个用户定义函数的定义中  
  
-   用于为列定义 CHECK 约束  
  
-   用于替换存储过程  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 用户定义函数所属的架构的名称。  
  
 *function_name*  
 用户定义函数的名称。 函数名称必须符合标识符的规则，并且必须是唯一的在数据库中以及对其架构。  
  
> [!NOTE]  
>  即使未指定参数，函数名称后也需要加上括号。  
  
 @*parameter_name*  
 用户定义函数中的参数。 可声明一个或多个参数。  
  
 一个函数最多可以有 2,100 个参数。 执行函数时，如果未定义参数的默认值，则用户必须提供每个已声明参数的值。  
  
 通过将 at 符号 (@) 用作第一个字符来指定参数名称。 参数名称必须符合标识符规则。 参数是对应于函数的局部参数；其他函数中可使用相同的参数名称。 参数只能代替常量，而不能用于代替表名、列名或其他数据库对象的名称。  
  
> [!NOTE]  
>  在传递存储过程或用户定义函数中的参数时，或在声明和设置批语句中的变量时，不会遵守 ANSI_WARNINGS。 例如，如果变量指**char （3)**，然后设置为值大于三个字符，数据将剪裁为定义的大小和插入或更新语句会成功。  
  
 *parameter_data_type*  
 为参数数据类型。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数、 中支持的所有标量数据类型[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]允许。 时间戳 (rowversion) 数据类型不是受支持的类型。  
  
 [=*默认*]  
 参数的默认值。 如果*默认*定义值，该函数可以执行而无需指定该参数的值。  
  
 如果函数的参数有默认值，则调用该函数以检索默认值时，必须指定关键字 DEFAULT。 此行为与在存储过程中使用具有默认值的参数不同，在后一种情况下，不提供参数同样意味着使用默认值。  
  
 *return_data_type*  
 标量用户定义函数的返回值。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数、 中支持的所有标量数据类型[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]允许。 时间戳 (rowversion) 数据类型不是受支持的类型。 不允许的光标和表的 nonscalar 类型。  
  
 *function_body*  
 系列[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。  Function_body 不能包含 SELECT 语句，并且不能引用数据库数据。  Function_body 不能引用表或视图。 函数体可以调用其他确定性函数，但不能调用具有不确定性函数。 
  
 标量函数中*function_body*是一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]在一起的计算结果为标量值的语句。  
  
 *scalar_expression*  
 指定标量函数返回的标量值。  
  
 **\<function_option >:: =** 
  
 指定函数将具有以下一个或多个选项：  
  
 SCHEMABINDING  
 指定将函数绑定到其引用的数据库对象。 如果指定了 SCHEMABINDING，则不能按照将影响函数定义的方式修改基对象。 必须首先修改或删除函数定义本身，才能删除将要修改的对象的依赖关系。  
  
 只有发生下列操作之一时，才会删除函数与其引用对象的绑定：  
  
-   删除函数。  
  
-   在未指定 SCHEMABINDING 选项的情况下，使用 ALTER 语句修改函数。  
  
 只有满足以下条件时，函数才能绑定到架构：  
  
-   该函数引用的任何用户定义函数是也绑定到架构的。  
  
-   使用一部分或两个部分构成的名称引用函数和该函数引用的其他 Udf。  
  
-   仅在 Udf 的正文中可以引用内置函数和相同的数据库中的其他 Udf。  
  
-   执行 CREATE FUNCTION 语句的用户对该函数引用的数据库对象具有 REFERENCES 权限。  
  
 若要删除架构绑定使用 ALTER  
  
 对 NULL 输入返回 NULL |**对 NULL 输入调用**  
 指定**OnNULLCall**的标量值函数的属性。 如果未指定，则默认为 CALLED ON NULL INPUT。 这意味着即使传递的参数为 NULL，也将执行函数体。  
  
## <a name="best-practices"></a>最佳实践  
 如果用户定义函数不是使用 SCHEMABINDING 子句创建的，则对基础对象进行的任何更改可能会影响函数定义并在调用函数时可能导致意外结果。 我们建议您实现以下方法之一，以便确保函数不会由于对于其基础对象的更改而过期：  
  
-   在您创建函数时指定 WITH SCHEMABINDING 子句。 这确保除非也修改了函数，否则无法修改在函数定义中引用的对象。  
  
## <a name="interoperability"></a>互操作性  
 下列语句在函数内有效：  
  
-   赋值语句。  
  
-   TRY...CATCH 语句以外的流控制语句。  
  
-   声明语句定义本地数据变量。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 用户定义函数不能用于执行修改数据库状态的操作。  
  
 用户定义函数可以嵌套；也就是说，用户定义函数可相互调用。 被调用函数开始执行时，嵌套级别将增加；被调用函数执行结束后，嵌套级别将减少。 用户定义函数的嵌套级别最多可达 32 级。 如果超出最大嵌套级别数，整个调用函数链将失败。   
  
## <a name="metadata"></a>元数据  
 本部分列出了可用于返回有关用户定义的函数元数据的系统目录视图。  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ： 显示的定义[!INCLUDE[tsql](../../includes/tsql-md.md)]用户定义函数。 例如：  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) ： 显示有关用户定义函数中定义的参数的信息。  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) ： 显示函数所引用的基础对象。  
  
## <a name="permissions"></a>Permissions  
 需要在数据库中具有 CREATE FUNCTION 权限，并对创建函数时所在的架构具有 ALTER 权限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. 使用标量值用户定义函数来更改数据类型  
 此简单函数采用**int**数据类型作为输入，并返回**decimal(10,2)**作为输出数据类型。  
  
```  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [删除函数 (SQL Server PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  



