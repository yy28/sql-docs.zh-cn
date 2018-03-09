---
title: "ALTER FUNCTION (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4b1008715d9cfd3e48945d0651f454253bc4e4bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  更改先前通过执行 CREATE FUNCTION 语句创建的现有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 CLR 函数，但不更改权限，也不影响任何相关的函数、存储过程或触发器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
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
```  

```
-- Transact-SQL Inline Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
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
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>参数  
 *schema_name*  
 用户定义函数所属的架构的名称。  
  
 *function_name*  
 要更改的用户定义函数。  
  
> [!NOTE]  
>  即使未指定参数，函数名称后也需要加上括号。  
  
 **@***parameter_name*  
 用户定义函数中的参数。 可声明一个或多个参数。  
  
 一个函数最多可以有 2,100 个参数。 执行函数时，如果未定义参数的默认值，则用户必须提供每个已声明参数的值。  
  
 使用指定参数名称 at 符号 (**@**) 作为第一个字符。 参数名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 参数是对应于函数的局部参数；其他函数中可使用相同的参数名称。 参数只能代替常量，而不能用于代替表名、列名或其他数据库对象的名称。  
  
> [!NOTE]  
>  在存储过程和用户定义函数中传递参数，或者在批处理语句中声明和设置变量时，不执行 ANSI_WARNINGS。 例如，如果变量指**char （3)**，然后设置为值大于三个字符，数据将剪裁为定义的大小和插入或更新语句会成功。  
  
 [ *type_schema_name。* ] *parameter_data_type*  
 参数的数据类型及其所属的架构（可选）。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，所有数据类型，包括 CLR 用户定义的类型，允许除**时间戳**数据类型。 对于 CLR 函数，所有数据类型，包括 CLR 用户定义的类型，都允许除**文本**， **ntext**，**映像**，和**时间戳**数据类型。 Nonscalar 类型**光标**和**表**不能指定为参数数据类型中任意一种[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函数。  
  
 如果*type_schema_name*未指定，[!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)]查找*parameter_data_type*按以下顺序：  
  
-   包含 SQL Server 系统数据类型名称的架构。  
  
-   当前数据库中当前用户的默认架构。  
  
-   当前数据库中的 **dbo** 架构。  
  
 [  **=** *默认*]  
 参数的默认值。 如果*默认*定义值，该函数可以执行而无需指定该参数的值。  
  
> [!NOTE]  
>  默认参数值可以为 CLR 函数除外指定**varchar （max)**和**varbinary （max)**数据类型。  
  
 如果函数的参数有默认值，则调用函数来检索默认值时必须指定 DEFAULT 关键字。 此行为与在存储过程中使用具有默认值的参数不同，在后一种情况下，不提供参数同样意味着使用默认值。  
  
 *return_data_type*  
 标量用户定义函数的返回值。 有关[!INCLUDE[tsql](../../includes/tsql-md.md)]函数，所有数据类型，包括 CLR 用户定义的类型，允许除**时间戳**数据类型。 对于 CLR 函数，所有数据类型，包括 CLR 用户定义的类型，都允许除**文本**， **ntext**，**映像**，和**时间戳**数据类型。 Nonscalar 类型**光标**和**表**不能指定为返回的数据类型中任意一种[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函数。  
  
 *function_body*  
 指定一系列定义函数值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，这些语句在一起使用不会产生负面影响（例如修改表）。 *function_body*仅在标量函数和多语句表值函数中使用。  
  
 标量函数中*function_body*是一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]在一起的计算结果为标量值的语句。  
  
 在多语句表值函数中， *function_body*是一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]填充表的语句返回变量。  
  
 *scalar_expression*  
 指定标量函数返回标量值。  
  
 TABLE  
 指定表值函数的返回值为表。 仅常量和 **@**  *local_variables*可以传递给表值函数。  
  
 在内联表值函数中，TABLE 返回值是通过单个 SELECT 语句定义的。 内联函数没有关联的返回变量。  
  
 在多语句表值函数中，  **@**  *return_variable*是用于存储和积累应作为函数的值返回行的表变量。 **@***return_variable*可以仅为指定[!INCLUDE[tsql](../../includes/tsql-md.md)]函数和不能为 CLR 函数。  
  
 *选择语句*  
 定义内联表值函数返回值的单个 SELECT 语句。  
  
 外部名称\<method_specifier >*assembly_name.class_name*。*method_name*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要与函数绑定的程序集的方法。 *程序集 _ 名称*必须匹配中的现有程序集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]带有上的可见性的当前数据库中。 *class_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符，并且为程序集中的类必须存在。 如果类具有使用句点的命名空间限定名称 (**。**) 来分隔命名空间部分，类名必须由使用方括号分隔 (**[]**) 或引号 (**""**). *method_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符，并且必须存在作为指定的类中的静态方法。  
  
> [!NOTE]  
>  默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能执行 CLR 代码。 你可以创建、 修改和删除引用公共语言运行时模块; 的数据库对象但是，无法执行中的这些引用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启用之前[clr enabled 选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。 若要启用该选项，使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 *\<*table_type_definition*>***(** { \<column_definition > \<column_constraint > |\<computed_column_definition >}[ \<table_constraint >] [ **，**...*n* ]**)**  
 定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数的表数据类型。 表声明包含列定义和列约束（或表约束）。  
  
\<clr_table_type_definition > **(** { *column_name**data_type* } [ **，**... *n*  ] **)** **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([在某些预览区域](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。  
  
 定义 CLR 函数的表数据类型。 表声明仅包含列名称和数据类型。  
  
 NULL |不为 NULL  
 仅支持本机编译标量用户定义函数。 有关详细信息，请参阅[内存中 OLTP 的标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 NATIVE_COMPILATION  
 指示是否已本机编译用户定义函数。 此参数是必需的本机编译标量用户定义函数。  
  
 NATIVE_COMPILATION 参数时需要 ALTER 函数，并可以仅使用，如果函数的创建具有 NATIVE_COMPILATION 自变量。  
  
 开始使用原子  
 支持仅用于本机编译标量用户定义函数和是必需的。 有关详细信息，请参阅 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
 SCHEMABINDING  
 SCHEMABINDING 参数是必需的本机编译标量用户定义函数。  
  
 **\<function_option >:: = 和\<clr_function_option >:: =**  
  
 指定函数将具有以下一个或多个选项：  
  
 ENCRYPTION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指示[!INCLUDE[ssDE](../../includes/ssde-md.md)]对目录视图中包含 ALTER FUNCTION 语句文本的列进行加密。 使用 ENCRYPTION 可以防止将函数作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的一部分发布。 不能为 CLR 函数指定 ENCRYPTION。  
  
 SCHEMABINDING  
 指定将函数绑定到其引用的数据库对象。 如果其他架构绑定对象也在引用该函数，此条件可防止更改该函数。  
  
 只有发生下列操作之一时，才会删除函数与其引用对象的绑定：  
  
-   删除函数。  
  
-   在未指定 SCHEMABINDING 选项的情况下，使用 ALTER 语句修改函数。  
  
函数可以是架构绑定之前，必须满足的条件的列表，请参阅[CREATE FUNCTION &#40;Transact SQL &#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 指定**OnNULLCall**的标量值函数的属性。 如果未指定，则默认为 CALLED ON NULL INPUT。 这意味着即使传递的参数为 NULL，也将执行函数体。  
  
 如果在 CLR 函数中指定了 RETURNS NULL ON NULL INPUT，它指示当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接收到的任何一个参数为 NULL 时，它可以返回 NULL，而无需实际调用函数体。 如果在指定的方法\<method_specifier > 已有自定义属性，该值指示返回 NULL ON NULL INPUT，但 ALTER FUNCTION 语句指示 CALLED ON NULL INPUT，ALTER FUNCTION 语句将优先。 **OnNULLCall** CLR 表值函数不能指定属性。  
  
 EXECUTE AS 子句  
 指定用于执行用户定义函数的安全上下文。 所以，您可以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用哪一用户帐户来验证针对该函数引用的任何数据库对象的权限。  
  
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
 指定列的排序规则。 如果未指定，则为该列分配数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 列表和详细信息，请参阅[Windows 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
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
  
 PAD_INDEX = { ON | OFF }  
 指定索引填充。 默认为 OFF。  
  
 填充因子 =*填充因子*  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或更改索引的过程中，应将每个索引页面的叶级填充到什么程度。 *填充因子*必须是介于 1 到 100 的整数值。 默认值为 0。  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 指定在插入操作尝试向唯一索引插入重复键值时的错误响应。 IGNORE_DUP_KEY 选项仅适用于创建或重新生成索引后发生的插入操作。 默认为 OFF。  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 指定是否重新计算分布统计信息。 默认为 OFF。  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 指定是否允许行锁。 默认值为 ON。  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 指定是否允许使用页锁。 默认值为 ON。  
  
## <a name="remarks"></a>注释  
 不能用 ALTER FUNCTION 将标量值函数更改为表值函数，反之亦然。 同样，也不能用 ALTER FUNCTION 将内联函数更改为多语句函数，反之亦然。 不能使用 ALTER FUNCTION 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数更改为 CLR 函数，反之亦然。  
  
 中的定义不能包含以下的 Service Broker 语句[!INCLUDE[tsql](../../includes/tsql-md.md)]用户定义函数：  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Permissions  
 需要对函数或架构具有 ALTER 权限。 如果函数指定用户定义类型，则需要对该类型具有 EXECUTE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [删除函数 &#40;Transact SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
