---
title: "创建函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
caps.latest.revision: 162
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: c74e3a3322dcc2268fa8e386fda5d55f59be98c5
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中创建用户定义函数。 用户定义函数是接受参数、执行操作（例如复杂计算）并将操作结果以值的形式返回的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或公共语言运行时 (CLR) 例程。 返回值可以是标量（单个）值或表。 使用此语句可以创建可通过以下方式使用的重复使用的例程：  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句（如 SELECT）中  
  
-   在调用该函数的应用程序中  
  
-   在另一个用户定义函数的定义中  
  
-   用于参数化视图或改进索引视图的功能  
  
-   用于在表中定义列  
  
-   用于为列定义 CHECK 约束  
  
-   用于替换存储过程  
  
-   对安全策略作为筛选器谓词使用内联函数  
  
> [!NOTE]  
>  本主题将讨论 SQL Server 的.NET Framework CLR 集成。 CLR 集成不适用于 Azure SQL 数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
```  
  
```  
-- Transact-SQL Inline Table-Valued Function Syntax   
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
  
```  
  
```  
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
  
```  

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  
  
<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```  
  
```  
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
<method_specifier>::=  
    assembly_name.class_name.method_name  
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>参数
*或 ALTER*  
 **适用于**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1)。  
  
 有条件地更改该函数，仅当它已存在。 
 
> [!NOTE]  
>  CLR 的可选 [或 ALTER] 语法是从开始提供[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU1。   
 
 *schema_name*  
 用户定义函数所属的架构的名称。  
  
 *function_name*  
 用户定义函数的名称。 函数名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)并且必须是唯一的在数据库中以及对其架构。  
  
> [!NOTE]  
>  即使未指定参数，函数名称后也需要加上括号。  
  
 @*parameter_name*  
 用户定义函数中的参数。 可声明一个或多个参数。  
  
 一个函数最多可以有 2,100 个参数。 执行函数时，如果未定义参数的默认值，则用户必须提供每个已声明参数的值。  
  
 通过将 at 符号 (@) 用作第一个字符来指定参数名称。 参数名称必须符合标识符规则。 参数是对应于函数的局部参数；其他函数中可使用相同的参数名称。 参数只能代替常量，而不能用于代替表名、列名或其他数据库对象的名称。  
  
> [!NOTE]  
>  在传递存储过程或用户定义函数中的参数时，或在声明和设置批语句中的变量时，不会遵守 ANSI_WARNINGS。 例如，如果变量指**char （3)**，然后设置为值大于三个字符，数据将剪裁为定义的大小和插入或更新语句会成功。  
  
 [ *type_schema_name*。 ] *parameter_data_type*  
 参数的数据类型及其所属的架构，后者为可选项。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，所有数据类型，包括 CLR 用户定义类型和用户定义表类型，允许除**时间戳**数据类型。 对于 CLR 函数，所有数据类型，包括 CLR 用户定义的类型，都允许除**文本**， **ntext**，**映像**、 用户定义表类型和**时间戳**数据类型。 Nonscalar 类型，**光标**和**表**，不能指定为参数数据类型中任意一种[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函数。  
  
 如果*type_schema_name*未指定，[!INCLUDE[ssDE](../../includes/ssde-md.md)]查找*scalar_parameter_data_type*按以下顺序：  
  
-   包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型名称的架构。  
  
-   当前数据库中当前用户的默认架构。  
  
-   当前数据库中的 **dbo** 架构。  
  
 [=*默认*]  
 参数的默认值。 如果*默认*定义值，该函数可以执行而无需指定该参数的值。  
  
> [!NOTE]  
>  默认参数值可以为 CLR 函数除外指定**varchar （max)**和**varbinary （max)**数据类型。  
  
 如果函数的参数有默认值，则调用该函数以检索默认值时，必须指定关键字 DEFAULT。 此行为与在存储过程中使用具有默认值的参数不同，在后一种情况下，不提供参数同样意味着使用默认值。 但在通过使用 EXECUTE 语句调用标量函数时，DEFAULT 关键字不是必需的。  
  
 READONLY  
 指示不能在函数定义中更新或修改参数。 如果参数类型为用户定义的表类型，则应指定 READONLY。  
  
 *return_data_type*  
 标量用户定义函数的返回值。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，所有数据类型，包括 CLR 用户定义的类型，允许除**时间戳**数据类型。 对于 CLR 函数，所有数据类型，包括 CLR 用户定义的类型，都允许除**文本**， **ntext**，**映像**，和**时间戳**数据类型。 Nonscalar 类型，**光标**和**表**，不能指定为返回的数据类型中任意一种[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函数。  
  
 *function_body*  
 指定一系列定义函数值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，这些语句在一起使用不会产生负面影响（例如修改表）。 *function_body*仅在标量函数和多语句表值函数中使用。  
  
 标量函数中*function_body*是一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]在一起的计算结果为标量值的语句。  
  
 在多语句表值函数中， *function_body*是一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]填充表的语句返回变量。  
  
 *scalar_expression*  
 指定标量函数返回的标量值。  
  
 TABLE  
 指定表值函数的返回值为表。 仅常量和 @*local_variables*可以传递给表值函数。  
  
 在内联表值函数中，TABLE 返回值是通过单个 SELECT 语句定义的。 内联函数没有关联的返回变量。  
  
 在多语句表值函数中，@*return_variable*是表变量，用于存储和累积应作为函数的值返回的行。 @*return_variable*可以仅为指定[!INCLUDE[tsql](../../includes/tsql-md.md)]函数和不能为 CLR 函数。  
  
> [!WARNING]  
>  加入多语句表值函数中的**FROM**子句是可行的但将会使性能不佳。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法对可以加入多语句函数的某些语句使用所有优化技术，导致生成的查询计划不佳。 若要获得最佳的性能，尽可能在基表之间使用联接而不是函数。  
  
 *select_stmt*  
 定义内联表值函数返回值的单个 SELECT 语句。  
  
 顺序 (\<order_clause >) 指定顺序从表值函数返回结果的顺序。 有关详细信息，请参阅本主题后面的“有关使用排序顺序的指南”部分。  
  
 外部名称\<method_specifier >*程序集 _ 名称*。*class_name*。*method_name* **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定创建的函数名称应引用的程序集和方法。  
  
-   *程序集 _ 名称*-必须与匹配中的值`name`的列   
    `SELECT * FROM sys.assemblies;`。  
    这是曾在 `CREATE ASSEMBLY` 语句中使用的名称。  
  
-   *class_name* -必须与匹配中的值`assembly_name`的列  
    `SELECT * FROM sys.assembly_modules;`。  
    此值通常包含嵌入的句点或圆点。 在这种情况下 TRANSACT-SQL 语法需要使用一对直接方括号 []，或使用一对双引号括起来的情况下限制值""。  
  
-   *method_name* -必须与匹配中的值`method_name`的列   
    `SELECT * FROM sys.assembly_modules;`。  
    该方法必须是静态方法。  
  
 在典型示例中，对于 MyFood.DLL（其中所有类型都位于 MyFood 命名空间中），`EXTERNAL NAME` 值可以是：   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能执行 CLR 代码。 你可以创建、 修改和删除引用公共语言运行时模块; 的数据库对象但是，无法执行中的这些引用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启用之前[clr enabled 选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。 若要启用此选项，使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 *\<*table_type_definition *>*  ({ \<column_definition > \<column_constraint > |\<computed_column_definition >}   [ \<table_constraint >] [，... *n*  ]) 的表数据类型的定义[!INCLUDE[tsql](../../includes/tsql-md.md)]函数。 表声明包含列定义和列约束（或表约束）。 表始终放在主文件组中。  
  
 \<clr_table_type_definition > ({ *column_name**data_type* } [，... *n*  ])**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([在某些区域以预览版提供](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。 |  
  
 定义 CLR 函数的表数据类型。 表声明仅包含列名称和数据类型。 表始终放在主文件组中。  
  
 NULL |不为 NULL  
 仅支持本机编译标量用户定义函数。 有关详细信息，请参阅[内存中 OLTP 的标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 NATIVE_COMPILATION  
 指示是否已本机编译用户定义函数。 此参数是必需的本机编译标量用户定义函数。  
  
 开始使用原子  
 支持仅用于本机编译标量用户定义函数和是必需的。 有关详细信息，请参阅 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
 SCHEMABINDING  
 SCHEMABINDING 参数是必需的本机编译标量用户定义函数。  
  
 EXECUTE AS  
 EXECUTE AS 是必需的本机编译标量用户定义函数。  
  
 **\<function_option >:: = 和\<clr_function_option >:: =** 
  
 指定函数将具有以下一个或多个选项：  
  
 ENCRYPTION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指示[!INCLUDE[ssDE](../../includes/ssde-md.md)]会将 CREATE FUNCTION 语句的原始文本转换为模糊格式。 模糊代码的输出在任何目录视图中都不能直接显示。 对系统表或数据库文件没有访问权限的用户不能检索模糊文本。 但是，文本将可供既可以通过访问系统表的特权用户[DAC 端口](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)或直接访问数据库文件。 此外，能够向服务器进程附加调试器的用户可在运行时从内存中检索原始过程。 有关访问系统元数据的详细信息，请参阅[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
 使用此选项可防止将函数作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的一部分发布。 不能为 CLR 函数指定此选项。  
  
 SCHEMABINDING  
 指定将函数绑定到其引用的数据库对象。 如果指定了 SCHEMABINDING，则不能按照将影响函数定义的方式修改基对象。 必须首先修改或删除函数定义本身，才能删除将要修改的对象的依赖关系。  
  
 只有发生下列操作之一时，才会删除函数与其引用对象的绑定： 
  
-   删除函数。  
  
-   在未指定 SCHEMABINDING 选项的情况下，使用 ALTER 语句修改函数。  
  
 只有满足以下条件时，函数才能绑定到架构：  
  
-   函数是一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数。  
  
-   该函数引用的用户定义函数和视图也绑定到架构。  
  
-   该函数引用的对象是用由两部分组成的名称引用的。  
  
-   该函数及其引用的对象属于同一数据库。  
  
-   执行 CREATE FUNCTION 语句的用户对该函数引用的数据库对象具有 REFERENCES 权限。  
  
 对 NULL 输入返回 NULL |**对 NULL 输入调用**  
 指定**OnNULLCall**的标量值函数的属性。 如果未指定，则默认为 CALLED ON NULL INPUT。 这意味着即使传递的参数为 NULL，也将执行函数体。  
  
 如果在 CLR 函数中指定了 RETURNS NULL ON NULL INPUT，它指示当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接收到的任何一个参数为 NULL 时，它可以返回 NULL，而无需实际调用函数体。 如果 CLR 函数的方法中指定\<method_specifier > 已有自定义属性，该值指示返回 NULL ON NULL INPUT，但 CREATE FUNCTION 语句指示 CALLED ON NULL INPUT，所执行的 CREATE FUNCTION 语句优先。 **OnNULLCall** CLR 表值函数不能指定属性。 
  
 EXECUTE AS 子句  
 指定用于执行用户定义函数的安全上下文。 所以，您可以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用哪一个用户帐户来验证针对该函数引用的任何数据库对象的权限。  
  
> [!NOTE]  
>  不能为内联用户定义函数指定 EXECUTE AS。  
  
 有关详细信息，请参阅 [EXECUTE AS 子句 (Transact-SQL)](../../t-sql/statements/execute-as-clause-transact-sql.md)。  
  
 **\<column_definition >:: =** 
  
 定义表数据类型。 表声明包含列定义和约束。 对于 CLR 函数，仅*column_name*和*data_type*可以指定。  
  
 *column_name*  
 表中列的名称。 列名称必须遵循标识符的规则，且在表中必须唯一。 *column_name*可以包含 1 至 128 个字符。  
  
 *data_type*  
 指定列数据类型。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，所有数据类型，包括 CLR 用户定义的类型，允许除**时间戳**。 对于 CLR 函数，所有数据类型，包括 CLR 用户定义的类型，都允许除**文本**， **ntext**，**映像**， **char**， **varchar**， **varchar （max)**，和**时间戳**。Nonscalar 类型**光标**不能指定为列数据类型中任意一种[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函数。  
  
 默认*constant_expression*  
 如果在插入过程中未显式提供值，则指定为列提供的值。 *constant_expression*为常量，NULL，或系统函数值。 DEFAULT 定义可以应用于除具有 IDENTITY 属性的列之外的任何列。 不能为 CLR 表值函数指定 DEFAULT。  
  
 COLLATE *collation_name*  
 指定列的排序规则。 如果未指定，则为该列分配数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 列表和有关排序规则的详细信息，请参阅[Windows 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 COLLATE 子句可以用于更改仅的列的排序规则**char**， **varchar**， **nchar**，和**nvarchar**数据类型。  
  
 不能为 CLR 表值函数指定 COLLATE。  
  
 ROWGUIDCOL  
 指示新列是行的全局唯一标识符列。 只有一个**uniqueidentifier**可以将每个表的列指定为 ROWGUIDCOL 列。 可以仅为分配 ROWGUIDCOL 属性**uniqueidentifier**列。  
  
 ROWGUIDCOL 属性并不强制列中所存储值的唯一性。 该属性也不会为插入表的新行自动生成值。 若要为每列生成唯一值，请在 INSERT 语句中使用 NEWID 函数。 可以指定默认值；但是，不能将 NEWID 指定为默认值。  
  
 IDENTITY  
 指示新列是标识列。 在为表添加新行时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为该列提供唯一的增量值。 标识列通常与 PRIMARY KEY 约束一起使用，作为表的唯一行标识符。 标识属性可以分配给**tinyint**， **smallint**， **int**， **bigint**， **decimal(p,0)**，或**numeric(p,0)**列。 每个表只能创建一个标识列。 不能对标识列使用绑定默认值和 DEFAULT 约束。 你必须同时指定*种子*和*递增*或都不。 如果二者都未指定，则取默认值 (1,1)。  
  
 不能为 CLR 表值函数指定 IDENTITY。  
  
 *种子*  
 要分配给表中第一行的整数值。  
  
 *增量*  
 是的整数值将添加到*种子*表中的连续行的值。  
  
 **\<column_constraint >:: = 和\<table_constraint >:: =** 
  
 为指定列或表定义约束。 对于 CLR 函数，允许的唯一约束类型为 NULL。 不允许命名约束。  
  
 NULL | NOT NULL  
 确定列中是否允许空值。 严格来讲，NULL 不是约束，但可以像指定 NOT NULL 那样指定它。 不能为 CLR 表值函数指定 NOT NULL。  
  
 PRIMARY KEY  
 一个约束，该约束通过唯一索引来强制指定列的实体完整性。 在表值用户定义函数中，只能对每个表中的一列创建 PRIMARY KEY 约束。 不能为 CLR 表值函数指定 PRIMARY KEY。  
  
 UNIQUE  
 一个约束，该约束通过唯一索引为一个或多个指定列提供实体完整性。 一个表可以有多个 UNIQUE 约束。 不能为 CLR 表值函数指定 UNIQUE。  
  
 CLUSTERED | NONCLUSTERED  
 指示为 PRIMARY KEY 或 UNIQUE 约束创建聚集索引还是非聚集索引。 PRIMARY KEY 约束使用 CLUSTERED，而 UNIQUE 约束使用 NONCLUSTERED。  
  
 只能为一个约束指定 CLUSTERED。 如果为 UNIQUE 约束指定了 CLUSTERED，并且指定了 PRIMARY KEY 约束，则 PRIMARY KEY 使用 NONCLUSTERED。  
  
 不能为 CLR 表值函数指定 CLUSTERED 和 NONCLUSTERED。  
  
 CHECK  
 一个约束，该约束通过限制可输入一列或多列中的可能值来强制实现域完整性。 不能为 CLR 表值函数指定 CHECK 约束。  
  
 *logical_expression*  
 返回 TRUE 或 FALSE 的逻辑表达式。  
  
 **\<computed_column_definition >:: =**  
  
 指定计算列。 有关计算列的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 计算列的名称。  
  
 *computed_column_expression*  
 定义计算列的值的表达式。  
  
 **\<index_option >:: =**  
  
 为 PRIMARY KEY 或 UNIQUE 索引指定索引选项。 有关索引选项的详细信息，请参阅[CREATE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON |**OFF** }  
 指定索引填充。 默认为 OFF。  
  
 填充因子 =*填充因子*  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或更改索引的过程中，应将每个索引页面的叶级填充到什么程度。 *填充因子*必须是介于 1 到 100 的整数值。 默认值为 0。  
  
 IGNORE_DUP_KEY = {ON |**OFF** }  
 指定在插入操作尝试向唯一索引插入重复键值时的错误响应。 IGNORE_DUP_KEY 选项仅适用于创建或重新生成索引后发生的插入操作。 默认为 OFF。  
  
 STATISTICS_NORECOMPUTE = {ON |**OFF** }  
 指定是否重新计算分布统计信息。 默认为 OFF。  
  
 ALLOW_ROW_LOCKS = { **ON** |关闭}  
 指定是否允许行锁。 默认值为 ON。  
  
 ALLOW_PAGE_LOCKS = { **ON** |关闭}  
 指定是否允许使用页锁。 默认值为 ON。  
  
## <a name="best-practices"></a>最佳实践  
 如果用户定义函数不是使用 SCHEMABINDING 子句创建的，则对基础对象进行的任何更改可能会影响函数定义并在调用函数时可能导致意外结果。 我们建议您实现以下方法之一，以便确保函数不会由于对于其基础对象的更改而过期：  
  
-   在您创建函数时指定 WITH SCHEMABINDING 子句。 这确保除非也修改了函数，否则无法修改在函数定义中引用的对象。  
  
-   执行[sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)后修改的函数定义中指定任何对象的存储过程。  
  
## <a name="data-types"></a>数据类型  
 如果在 CLR 函数中指定参数，则应将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型标记为定义过*scalar_parameter_data_type*。 有关比较[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统数据类型与 CLR 集成数据类型或[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时数据类型，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要引用的正确方法重载类中时，该方法中所示\<method_specifier > 必须具有以下特征： 
  
-   接收相同数量的参数中指定 [，...*n* ].  
  
-   通过值而不是引用来接收所有参数。  
  
-   使用与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函数中指定的类型兼容的参数类型。  
  
 如果 CLR 函数的返回数据类型指定表类型 （返回表） 中的方法的返回数据类型\<method_specifier > 的类型应该是**IEnumerator**或**IEnumerable**，并假设，该函数的创建者通过实现该接口。 与不同[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，CLR 函数不能包含中的主键的键、 唯一、 或检查约束\<table_type_definition >。 中指定的列的数据类型\<table_type_definition > 必须与中的方法所返回的结果集的相应列的类型匹配\<method_specifier > 在执行时。 创建函数时不执行上述类型检查。 
  
 有关如何对程序 CLR 函数的详细信息，请参阅[clr 用户定义函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)。  
  
## <a name="general-remarks"></a>一般备注  
 可在使用标量表达式的位置调用标量值函数。 这包括计算列和 CHECK 约束定义。 此外可以通过使用在执行标量值函数[执行](../../t-sql/language-elements/execute-transact-sql.md)语句。 必须使用至少由两部分组成名称的函数来调用标量值函数。 有关多部分名称的详细信息，请参阅[TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 在允许表表达式的情况下，可在 SELECT、INSERT、UPDATE 或 DELETE 语句的 FROM 子句中调用表值函数。 有关详细信息，请参阅[执行用户定义函数](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)。  
  
## <a name="interoperability"></a>互操作性  
 下列语句在函数内有效：  
  
-   赋值语句。  
  
-   TRY...CATCH 语句以外的流控制语句。  
  
-   定义局部数据变量和局部游标的 DECLARE 语句。  
  
-   SELECT 语句，其中的选择列表包含为局部变量分配值的表达式。  
  
-   游标操作，该操作引用在函数中声明、打开、关闭和释放的局部游标。 只允许使用以 INTO 子句向局部变量赋值的 FETCH 语句；不允许使用将数据返回到客户端的 FETCH 语句。  
  
-   修改本地表变量的 INSERT、UPDATE 和 DELETE 语句。  
  
-   调用扩展存储过程的 EXECUTE 语句。  
  
-   有关详细信息，请参阅[创建用户定义函数 &#40; 数据库引擎 &#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)。  
  
### <a name="computed-column-interoperability"></a>计算列互操作性  
 函数具有下列属性。 这些属性的值确定了函数是否可用于持久化计算列或索引计算列。  
  
|属性|Description|说明|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|函数是确定性函数还是不确定性函数。|确定性函数中允许本地数据访问。 例如，如果每次使用一组特定输入值和相同数据库状态调用函数时，函数都返回相同结果，则该函数将被标记为确定性函数。|  
|**IsPrecise**|函数是精确函数还是不精确函数。|不精确函数包含浮点运算之类的运算。|  
|**IsSystemVerified**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可验证函数的精度和确定性属性。||  
|**将 SystemDataAccess**|函数可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的系统数据（系统目录或虚拟系统表）。||  
|**UserDataAccess**|函数可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的用户数据。|包含用户定义表和临时表，但不包含表变量。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数的精度和确定性属性由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动确定。 CLR 函数的数据访问权限和确定性属性可由用户指定。 有关详细信息，请参阅[CLR 集成自定义属性概述](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)。  
  
 若要显示这些属性的当前值，请使用[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)。  
  
 必须使用确定性的架构绑定创建函数。  
  
 如果用户定义函数具有下列属性值，则可以在索引中使用调用用户定义函数的计算列：  
  
-   **IsDeterministic** = true  
  
-   **IsSystemVerified** （除非计算的列 persisted) = true  
  
-   **UserDataAccess** = false  
  
-   **将 SystemDataAccess** = false  
  
 有关详细信息，请参阅 [计算列上的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>从函数中调用扩展存储过程  
 如果在函数中调用扩展存储过程，则该过程不能向客户端返回结果集。 向客户端返回结果集的任何 ODS API 都将返回 FAIL。 扩展存储过程可以连接回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例；不过，该过程不应尝试与调用扩展存储过程的函数同时联接到同一事务。  
  
 与通过批处理或存储过程进行调用相似，扩展存储过程在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Windows 安全帐户的上下文中执行。 存储过程的所有者在授予用户 EXECUTE 权限时应考虑这一点。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 用户定义函数不能用于执行修改数据库状态的操作。  
  
 用户定义函数不能包含将表作为其目标的 OUTPUT INTO 子句。  
  
 下列 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 语句不能包含在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数的定义中：  
  
-   BEGIN DIALOG CONVERSATION  
  
-   END CONVERSATION  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   SEND  
  
 用户定义函数可以嵌套；也就是说，用户定义函数可相互调用。 被调用函数开始执行时，嵌套级别将增加；被调用函数执行结束后，嵌套级别将减少。 用户定义函数的嵌套级别最多可达 32 级。 如果超出最大嵌套级别数，整个调用函数链将失败。 从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数对托管代码的任何引用都将根据 32 级嵌套限制计入一个级别。 从托管代码内部调用的方法不根据此限制进行计数。  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>在 CLR 表值函数中使用排序顺序  
 在 CLR 表值函数中使用 ORDER 子句时请遵循以下准则：  
  
-   必须确保始终按指定的顺序对结果进行排序。 如果没有按指定的顺序对结果进行排序，则在执行查询时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将生成一条错误消息。  
  
-   如果指定了 ORDER 子句，则必须根据列（显式或隐式）的排序规则对表值函数的输出进行排序。 例如，如果列排序规则为中文（在表值函数的 DDL 中指定或从数据库排序规则中获取），则必须根据中文排序规则对返回的结果进行排序。  
  
-   如果指定了 ORDER 子句，则在返回结果时始终由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 验证 ORDER 子句，而不管查询处理器是否会使用该子句执行进一步的优化。 只有您知道 ORDER 子句对查询处理器有用时才使用它。  
  
-   在以下情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询处理器将自动使用 ORDER 子句：  
  
    -   其中 ORDER 子句与索引兼容的“插入”查询。  
  
    -   与 ORDER 子句兼容的 ORDER BY 子句。  
  
    -   其中 GROUP BY 与 ORDER 子句兼容的聚合。  
  
    -   其中不同列与 ORDER 子句兼容的 DISTINCT 聚合。  
  
 除非在查询中还指定了 ORDER BY，否则 ORDER 子句不保证在执行 SELECT 查询时得到有序结果。 请参阅[sys.function_order_columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md)有关如何为表值函数的排序顺序中包含的列的查询的信息。  
  
## <a name="metadata"></a>元数据  
 下表列出可用于返回与用户定义函数有关的元数据的系统目录视图。  
  
|系统视图|Description|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|请参阅下面的示例部分中的示例 E。|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|显示 CLR 用户定义函数的有关信息。|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|显示用户定义函数中定义的参数的有关信息。|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|显示函数所引用的基础对象。|  
  
## <a name="permissions"></a>Permissions  
 需要在数据库中具有 CREATE FUNCTION 权限，并对创建函数时所在的架构具有 ALTER 权限。 如果函数指定用户定义类型，则需要对该类型具有 EXECUTE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. 使用计算 ISO 周的标量值用户定义函数  
 下面的示例将创建用户定义函数 `ISOweek`。 此函数使用日期参数来计算 ISO 周数。 要使此函数能正确计算，必须在调用该函数前调用 `SET DATEFIRST 1`。  
  
 该示例还演示使用[EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md)子句，以指定可以在其中执行存储的过程的安全上下文。 在该示例中，`CALLER` 选项指定该过程将在调用该过程的用户的上下文中执行。 你可以指定其他选项都是自行，所有者，和*user_name*。  
  
 下面是函数调用。 请注意，`DATEFIRST` 设置为 `1`。  
  
```tsql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. 创建内联表值函数  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中返回内联表值函数。 它返回三列`ProductID`，`Name`和由存储为年度截止到现在总计的聚合`YTD Total`的形式销售给存储每个产品。  
  
```tsql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 若要调用该函数，请运行此查询。    

```tsql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. 创建多语句表值函数  
 下面的示例在 AdventureWorks2012 数据库中创建表值函数 `fn_FindReports(InEmpID)`。 如果提供一个有效雇员 ID，该函数将返回一个表，该表对应于直接或间接向该雇员报告的所有雇员。 该函数使用递归公用表表达式 (CTE) 来生成雇员的层次结构列表。 有关递归 Cte 的详细信息，请参阅[使用 common_table_expression &#40;Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```tsql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. 创建 CLR 函数  
 该示例创建 CLR 函数`len_s`。 在创建该函数之前，程序集 `SurrogateStringFunction.dll` 已在本地数据库中注册。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```tsql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 有关如何创建 CLR 表值函数的示例，请参阅[CLR Table-Valued 函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)。  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. 显示的定义[!INCLUDE[tsql](../../includes/tsql-md.md)]用户定义函数  
  
```tsql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 不能使用 sys.sql_modules 查看使用 ENCRYPTION 选项创建的函数定义；不过，可显示有关加密函数的其他信息。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [删除函数 &#40;Transact SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [CLR 用户定义函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [创建安全策略 &#40;Transact SQL &#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 


