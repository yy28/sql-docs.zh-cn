---
title: "创建类型 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: 92
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4e7f411871d98fc6854b97478402567017d28222
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的当前数据库中创建别名数据类型或用户定义类型。 别名数据类型的实现基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机系统类型。 通过中的程序集的类实现的用户定义的类型[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR)。 若要绑定到其实现的用户定义的类型，包含该类型实现的 CLR 程序集必须首先注册中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)。  
  
 默认情况下，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行 CLR 代码的功能处于关闭状态。 但你可以创建、 修改和删除引用托管的代码模块的数据库对象中将不执行这些引用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非[clr enabled 选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)通过使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  本主题将讨论 SQL Server 的.NET Framework CLR 集成。 CLR 集成不适用于 Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 别名数据类型或用户定义类型所属架构的名称。  
  
 *类型 _ 名称*  
 别名数据类型或用户定义类型的名称。 类型名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 *base_type*  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供此别名数据类型所基于的数据类型。 *base_type*是**sysname**，无默认值，并且可为以下值之一：  
  
|||||  
|-|-|-|-|  
|**bigint**|**二进制 (**  *n*  **)**|**bit**|**char (**  *n*  **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar (**  *n*  **)**|**ntext**|**numeric**|  
|**nvarchar (**  *n*  &#124;**最大值)**|**real**|**smalldatetime**|**int**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary (**  *n*  &#124;**最大值)**|**varchar (**  *n*  &#124;**最大值)**|  
  
 *base_type*也可以是映射到这些系统数据类型之一的任何数据类型同义词。  
  
 *精度*  
 有关**十进制**或**数值**，是一个非负整数，指示可能会存储，同时向左和小数点右侧的十进制数字的最大的总数。 有关详细信息，请参阅[小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *小数位数*  
 有关**十进制**或**数值**，是一个非负整数，指示可以向在小数点右存储的十进制数字的最大数目，且它必须小于或等于精度. 有关详细信息，请参阅[小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** |不为 NULL  
 指定此类型是否可容纳空值。 如果未指定，则默认值为 NULL。  
  
 *程序集 _ 名称*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]程序集引用的公共语言运行时中的用户定义类型的实现。 *程序集 _ 名称*应匹配中的现有程序集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当前数据库中。  
  
> [!NOTE]  
>  EXTERNAL_NAME 在包含数据库中不可用。  
  
 **[.** *class_name***]**   
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定实现用户定义类型的程序集内的类。 *class_name*必须是有效的标识符，并且必须具有程序集可见性的作为程序集中的类存在。 *class_name*区分大小写，而不考虑数据库排序规则，必须完全匹配中的相应程序集的类名称。 类名称可以是命名空间限定名称括在方括号 (**[]**) 如果用于编写类的编程语言使用的命名空间，如 C# 的概念。 如果*class_name*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假定它是与相同*type_name*。  
  
 \<column_definition >  
 定义用户定义表类型的列。  
  
 \<数据类型 >  
 定义用户定义表类型的列中的数据类型。 有关数据类型的详细信息，请参阅[数据类型 &#40;Transact SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md). 有关表的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint >  
 定义用户定义表类型的列约束。 支持的约束包括 PRIMARY KEY、UNIQUE 和 CHECK。 有关表的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<computed_column_definition >  
 将计算列表达式定义为用户定义表类型中的列。 有关表的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint >  
 定义用户定义表类型的表约束。 支持的约束包括 PRIMARY KEY、UNIQUE 和 CHECK。  
  
 \<index_option >  
 指定对唯一聚集索引或唯一非聚集索引执行多行插入操作时出现重复键值的错误响应。 有关索引选项的详细信息，请参阅[CREATE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 必须在 CREATE TABLE 语句中指定列索引和表索引。 内存优化表不支持 CREATE INDEX 和 DROP INDEX。  
  
 MEMORY_OPTIMIZED  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指示表类型是否为内存优化表。 默认情况下，此选项处于关闭状态；表（类型）不是内存优化表（类型）。 内存优化表类型是内存优化用户表，它保留在磁盘上的架构与其他用户表类似。  
  
 BUCKET_COUNT  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指示应在哈希索引中创建的存储桶数。 哈希索引中 BUCKET_COUNT 的最大值为 1,073,741,824。 有关存储桶计数的详细信息，请参阅[内存优化表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。 *bucket_count*参数是必需的。  
  
 HASH  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指示创建哈希索引。 仅在内存优化表中支持哈希索引。  
  
## <a name="remarks"></a>注释  
 在中引用的程序集的类*程序集 _ 名称*，以及其方法中，应该可满足所有的实现中的用户定义的类型的要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关这些要求的详细信息，请参阅[clr 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
 其他注意事项包括以下几点：  
  
-   类可以具有重载方法，但只能从托管代码内而不能从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用这些方法。  
  
-   必须将任何静态成员声明为**const**或**readonly**如果*程序集 _ 名称*安全或 EXTERNAL_ACCESS。  
  
 在数据库内，任何从 CLR 上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的指定类型都只能注册一个用户定义类型。 如果数据库中已存在 CLR 类型的用户定义类型，则在对 CLR 类型创建用户定义类型时，CREATE TYPE 会因错误而失败。 如果一个 CLR 类型可被映射到多个用户定义类型，则要求使用此限制来避免 SQL 类型解析过程中的混乱情况。  
  
 如果类型中的任何赋值函数方法不返回*void*，CREATE TYPE 语句不会执行。  
  
 若要修改用户定义类型，必须使用 DROP TYPE 语句除去该类型，然后重新创建它。  
  
 与通过使用创建的用户定义的类型不同**sp_addtype**、**公共**数据库角色不会自动授予 REFERENCES 权限通过使用 CREATE TYPE 创建的类型。 此权限必须单独授予。  
  
 在用户定义表类型中，结构化在中使用的用户定义类型*column_name* \<数据类型 > 是在其中定义表类型的数据库架构范围的一部分。 若要访问数据库不同作用域中的结构化用户定义类型，请使用由两部分组成的名称。  
  
 在用户定义表类型中，计算列的主键必须是 PERSISTED 和 NOT NULL。  
  
## <a name="memory-optimized-table-types"></a>内存优化表类型  
 从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 开始，可在主内存中而不是磁盘上执行表类型中的数据的处理。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。 有关演示如何创建内存优化表类型的代码示例，请参阅[创建内存优化表和本机编译的存储过程](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
## <a name="permissions"></a>Permissions  
 要求在当前数据库中具有 CREATE TYPE 权限，以及具有对 *schema_name*的 ALTER 权限。 如果未指定 *schema_name* ，则将应用用于确定当前用户的架构的默认名称解析规则。 如果*程序集 _ 名称*指定，则用户必须拥有该程序集或在其上具有 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. 基于 varchar 数据类型创建别名类型  
 以下示例基于系统提供的 `varchar` 数据类型创建别名类型。  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. 创建的用户定义的类型  
 下面的示例创建类型`Utf8String`引用类`utf8string`集中`utf8string`。 创建类型之前，应在本地数据库中注册程序集 `utf8string`。 将 CREATE ASSEMBLY 语句的二进制部分替换为有效描述。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. 创建用户定义表类型  
 下面的示例创建一个具有两列的用户定义表类型。 有关如何创建和使用表值参数的详细信息，请参阅[使用表值参数 &#40; 数据库引擎 &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建程序集 &#40;Transact SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [拖放类型 &#40;Transact SQL &#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

