---
title: "ALTER TABLE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/07/2017
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
- WAIT_AT_LOW_PRIORITY
- ABORT_AFTER_WAIT
- ABORT_AFTER_WAIT_TSQL
- ALTER_TABLE_TSQL
- ALTER TABLE
- WAIT_AT_LOW_PRIORITY_TSQL
- ALTER_COLUMN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- columns [SQL Server], resizing
- changing column size
- MAXDOP index option, ALTER TABLE statement
- table modifications [SQL Server], ALTER TABLE
- ALTER TABLE statement
- modifying tables
- partitioned tables [SQL Server], lock escalation
- resizing columns
- removing columns
- switching partitions
- reassigning partitions
- removing constraints
- triggers [SQL Server], disabling
- columns [SQL Server], adding
- LOCK_ESCALATION option of ALTER TABLE
- constraints [SQL Server], deleting
- constraints [SQL Server], disabling
- triggers [SQL Server], enabling
- re-enabling constraints
- index modifications [SQL Server]
- disabling constraints
- columns [SQL Server], removing
- max degree of parallelism option
- locking [SQL Server], tables
- ONLINE option
- disabling triggers
- constraints [SQL Server], adding
- deleting constraints
- adding constraints
- adding columns
- SWITCH partitions
- partitioned tables [SQL Server], switching
- lock escalation [SQL Server], option of ALTER TABLE
- constraints [SQL Server], enabling
- dropping constraints
- dropping columns
- table changes [SQL Server]
ms.assetid: f1745145-182d-4301-a334-18f799d361d1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 62bb3df1044b6acc580daefc75ace88bca441e53
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="alter-table-transact-sql"></a>ALTER TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  通过更改、添加或删除列和约束，重新分配和重新生成分区，或者启用或禁用约束和触发器，可以修改表的定义。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
{   
    ALTER COLUMN column_name   
    {   
        [ type_schema_name. ] type_name   
            [ (   
                {   
                   precision [ , scale ]   
                 | max   
                 | xml_schema_collection   
                }   
            ) ]   
        [ COLLATE collation_name ]   
        [ NULL | NOT NULL ] [ SPARSE ]  
      | { ADD | DROP }   
          { ROWGUIDCOL | PERSISTED | NOT FOR REPLICATION | SPARSE | HIDDEN }  
      | { ADD | DROP } MASKED [ WITH ( FUNCTION = ' mask_function ') ]  
    }   
    [ WITH ( ONLINE = ON | OFF ) ]  
    | [ WITH { CHECK | NOCHECK } ]  
  
    | ADD   
    {   
        <column_definition>  
      | <computed_column_definition>  
      | <table_constraint>   
      | <column_set_definition>   
    } [ ,...n ]  
      | [ system_start_time_column_name datetime2 GENERATED ALWAYS AS ROW START   
                   [ HIDDEN ] [ NOT NULL ] [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
            system_end_time_column_name datetime2 GENERATED ALWAYS AS ROW END   
                   [ HIDDEN ] [ NOT NULL ]  [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
         ]  
       PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )  
    | DROP   
     [ {  
         [ CONSTRAINT ]  [ IF EXISTS ]  
         {   
              constraint_name   
              [ WITH   
               ( <drop_clustered_constraint_option> [ ,...n ] )   
              ]   
          } [ ,...n ]  
          | COLUMN  [ IF EXISTS ]  
          {  
              column_name   
          } [ ,...n ]  
          | PERIOD FOR SYSTEM_TIME  
     } [ ,...n ]  
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT   
        { ALL | constraint_name [ ,...n ] }   
  
    | { ENABLE | DISABLE } TRIGGER   
        { ALL | trigger_name [ ,...n ] }  
  
    | { ENABLE | DISABLE } CHANGE_TRACKING   
        [ WITH ( TRACK_COLUMNS_UPDATED = { ON | OFF } ) ]  
  
    | SWITCH [ PARTITION source_partition_number_expression ]  
        TO target_table   
        [ PARTITION target_partition_number_expression ]  
        [ WITH ( <low_priority_lock_wait> ) ]  
    | SET   
        (  
            [ FILESTREAM_ON =   
                { partition_scheme_name | filegroup | "default" | "NULL" } ]  
            | SYSTEM_VERSIONING =   
                  {   
                      OFF   
                  | ON   
                      [ ( HISTORY_TABLE = schema_name . history_table_name   
                          [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] 
                          [, HISTORY_RETENTION_PERIOD = 
                          { 
                               INFINITE | number {DAY | DAYS | WEEK | WEEKS 
                 | MONTH | MONTHS | YEAR | YEARS } 
                          } 
                          ]  
                        )  
                      ]  
                  }  
          )  
    | REBUILD   
      [ [PARTITION = ALL]  
        [ WITH ( <rebuild_option> [ ,...n ] ) ]   
      | [ PARTITION = partition_number   
           [ WITH ( <single_partition_rebuild_option> [ ,...n ] ) ]  
        ]  
      ]  
  
    | <table_option>  
  
    | <filetable_option>  
  
    | <stretch_configuration>  
  
}  
[ ; ]  
  
-- ALTER TABLE options  
  
<column_set_definition> ::=   
    column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
<drop_clustered_constraint_option> ::=    
    {   
        MAXDOP = max_degree_of_parallelism  
      | ONLINE = { ON | OFF }  
      | MOVE TO   
         { partition_scheme_name ( column_name ) | filegroup | "default" }  
    }  
<table_option> ::=  
    {  
        SET ( LOCK_ESCALATION = { AUTO | TABLE | DISABLE } )  
    }  
  
<filetable_option> ::=  
    {  
       [ { ENABLE | DISABLE } FILETABLE_NAMESPACE ]  
       [ SET ( FILETABLE_DIRECTORY = directory_name ) ]  
    }  
  
<stretch_configuration> ::=  
    {  
      SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options>  )  
          | = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED )  
          | ( <table_stretch_options> [, ...n] )  
        }  
            )  
    }  
  
<table_stretch_options> ::=  
    {  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
    }  
  
<single_partition_rebuild__option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ], 
        ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER TABLE [ database_name . [schema_name ] . | schema_name. ] source_table_name   
{  
    ALTER COLUMN column_name  
        {   
            type_name [ ( precision [ , scale ] ) ]   
            [ COLLATE Windows_collation_name ]   
            [ NULL | NOT NULL ]   
        }  
    | ADD { <column_definition> | <column_constraint> FOR column_name} [ ,...n ]  
    | DROP { COLUMN column_name | [CONSTRAINT] constraint_name } [ ,...n ]  
    | REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_option> ] ]
      } 
    | { SPLIT | MERGE } RANGE (boundary_value)  
    | SWITCH [ PARTITION source_partition_number  
        TO target_table_name [ PARTITION target_partition_number ]  
}  
[;]  
  
<column_definition>::=  
{  
    column_name  
    type_name [ ( precision [ , scale ] ) ]   
    [ <column_constraint> ]  
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ]  
}  
  
<column_constraint>::=  
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression  

<rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
```    

   
## <a name="arguments"></a>参数  
 *database_name*  
 要在其中创建表的数据库的名称。  
  
 *schema_name*  
 表所属架构的名称。  
  
 *table_name*  
 要更改的表的名称。 如果表不在当前数据库中，或者不包含在当前用户所拥有的架构中，则必须显式指定数据库和架构。  
  
 ALTER COLUMN  
 指定要更改的命名列。  
  
 修改后的列不能为下列任何一种列：  
  
-   具有的列**时间戳**数据类型。  
  
-   表的 ROWGUIDCOL 列。  
  
-   计算列或用于计算列的列。  
  
-   在生成的 CREATE STATISTICS 语句，除非列是统计信息中使用**varchar**， **nvarchar**，或**varbinary**数据类型，未更改的数据类型，并新的大小为等于或大于旧的大小，或者如果从 not null 到 null，更改列。 首先，用 DROP STATISTICS 语句删除统计信息。 由查询优化器自动生成的统计信息将被 ALTER COLUMN 自动删除。  
  
-   用于 PRIMARY KEY 或 [FOREIGN KEY] REFERENCES 约束中的列。  
  
-   用于 CHECK 或 UNIQUE 约束中的列。 但是，允许更改用于 CHECK 或 UNIQUE 约束中的长度可变的列的长度。  
  
-   与默认定义关联的列。 但是，如果不更改数据类型，则可以更改列的长度、精度或小数位数。  
  
数据类型**文本**， **ntext**和**映像**列可以更改仅在以下方面：  
  
-   **文本**到**varchar （max)**， **nvarchar (max)**，或**xml**  
  
-   **ntext**到**varchar （max)**， **nvarchar (max)**，或**xml**  
  
-   **image** to **varbinary(max)**  
  
更改某些数据类型可能导致更改相关数据。 例如，更改**nchar**或**nvarchar**列**char**或**varchar**可能会导致的扩展字符的转换。 有关详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。 降低列的精度或减少小数位数可能导致数据截断。  
  
> [!NOTE]
> 无法更改已分区表的列的数据类型。  
>  
> 不能更改索引中包含的列的数据类型，除非该列为**varchar**， **nvarchar**，或**varbinary**数据类型，并且新的大小为等于或更大比旧的大小。  
>  
> 无法从更改包含在主键约束，该列**NOT NULL**到**NULL**。  
  
如果正在修改列已加密使用`ENCRYPTED WITH`，可以将该数据类型更改为兼容的数据类型 （如整型转换为 BIGINT），但不能更改任何加密设置。  
  
 column_name  
 要更改、添加或删除的列的名称。 *column_name*最多 128 个字符。 为新的列， *column_name*可以为列创建的省略**时间戳**数据类型。 名称**时间戳**如果没有，则使用*column_name*为指定**时间戳**数据类型列。  
  
 [ *type_schema_name***.** ] *type_name*  
 更改后的列的新数据类型或添加的列的数据类型。 *类型 _ 名称*不能为现有列的已分区表指定。 *类型 _ 名称*可以是以下任何一个：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型。  
  
-   基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型的别名数据类型。 必须先用 CREATE TYPE 语句创建别名数据类型，然后才能将其用于表定义中。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 用户定义类型及其所属架构。 必须先用 CREATE TYPE 语句创建 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 用户定义类型，然后才能将其用于表定义中。  
  
以下是条件*type_name*的更改的列：  
  
-   以前的数据类型必须可以隐式转换为新数据类型。  
-   *类型 _ 名称*不能为**时间戳**。  
-   对于 ALTER COLUMN，ANSI_NULL 默认值始终为 ON；如果没有指定，列可为空。  
-   对于 ALTER COLUMN，ANSI_PADDING 填充始终为 ON。  
-   如果已修改的列是标识列， *new_data_type*必须支持标识属性是数据类型。  
-   当前的 SET ARITHABORT 设置将被忽略。 ALTER TABLE 的操作方式与 ARITHABORT 设置为 ON 时相同。  
  
> [!NOTE]  
> 如果未指定 COLLATE 子句，则更改列的数据类型将导致更改数据库的默认排序规则。  
  
 *精度*  
 指定的数据类型的精度。 有关有效的精度值的详细信息，请参阅[精度、 小数位数和长度 &#40;Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *小数位数*  
 是指定数据类型的小数位数。 有关有效的缩放值的详细信息，请参阅[精度、 小数位数和长度 &#40;Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **max**  
 仅适用于**varchar**， **nvarchar**，和**varbinary**数据类型用于存储 2 ^31-1 个字节的字符，二进制数据和 Unicode 数据。  
  
 *xml_schema_collection*  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 仅适用于**xml**将 XML 架构与类型相关联的数据类型。 键入字词之前**xml**列添加到架构集合，架构集合必须首先创建数据库中使用[CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)。  
  
COLLATE \< *collation_name* > 指定更改的列的新排序规则。 如果未指定，则为该列分配数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 列表和详细信息，请参阅[Windows 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 COLLATE 子句可以用于更改仅的列的排序规则**char**， **varchar**， **nchar**，和**nvarchar**数据类型。 若要更改用户定义别名数据类型列的排序规则，必须执行单独的 ALTER TABLE 语句，将列改为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型，并更改其排序规则，然后重新将列改为别名数据类型。  
  
 如果出现以下一种或多种情况，则 ALTER COLUMN 不能更改排序规则：  
  
-   CHECK 约束、FOREIGN KEY 约束或计算列引用了更改后的列。  
-   已为列创建了索引、统计信息或全文检索。 如果更改了列的排序规则，则将删除为更改后的列自动创建的统计信息。  
-   架构绑定视图或函数引用了列。  
  
有关详细信息，请参阅[排序规则 (Transact-SQL)](~/t-sql/statements/collations.md)。  
  
NULL | NOT NULL  
 指定列是否可接受空值。 如果列不允许空值，则只有在指定了默认值或表为空的情况下，才能用 ALTER TABLE 语句添加该列。 只有同时指定了 PERSISTED 时，才能为计算列指定 NOT NULL。 如果新列允许 Null 值，但没有指定默认值，则新列在表中的每一行都包含一个 Null 值。 如果新列允许 Null 值，并且指定了新列的默认值，则可以使用 WITH VALUES 将默认值存储到表中每个现有行的新列中。  
  
 如果新列不允许 Null 值，并且表不为空，那么 DEFAULT 定义必须与新列一起添加；并且，加载新列时，每个现有行的新列中将自动包含默认值。  
  
 在 ALTER COLUMN 语句中指定 NULL，可以强制 NOT NULL 列允许 Null 值，但 PRIMARY KEY 约束中的列除外。 只有列中不包含空值时，才可以在 ALTER COLUMN 中指定 NOT NULL。 必须将 Null 值更新为某个值后，才允许执行 ALTER COLUMN NOT NULL 语句，例如：  
  
```sql  
UPDATE MyTable SET NullCol = N'some_value' WHERE NullCol IS NULL;  
ALTER TABLE MyTable ALTER COLUMN NullCOl NVARCHAR(20) NOT NULL;  
```  
  
 如果用 CREATE TABLE 或 ALTER TABLE 语句创建或更改表，则数据库或会话设置将影响并且可能覆盖用于列定义的数据类型的为 Null 性。 建议您始终针对非计算列将某一列显式定义为 NULL 或 NOT NULL。  
  
 如果添加具有用户定义的数据类型的列，则建议您将该列定义为与用户定义的数据类型的为 Null 性相同，并为该列指定一个默认值。 有关详细信息，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。  
  
> [!NOTE]  
> 如果为 NULL 或不使用 ALTER COLUMN 指定 NULL *new_data_type* [(*精度*[，*缩放*])] 还必须指定。 如果未更改数据类型、精度和小数位数，则指定当前的列值。  
  
 [ {ADD | DROP} ROWGUIDCOL ]  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定在指定列中添加或删除 ROWGUIDCOL 属性。 ROWGUIDCOL 指示列为行 GUID 列。 只有一个**uniqueidentifier**每个表的列可以指定为 ROWGUIDCOL 列，并且可以只能与分配的 ROWGUIDCOL 属性**uniqueidentifier**列。 不能将 ROWGUIDCOL 分配给用户定义数据类型的列。  
  
 ROWGUIDCOL 不强制要求列中存储的值的唯一性，也不为插入到表中的新行自动生成值。 若要为每列生成唯一值，则可以在 INSERT 语句中使用 NEWID 函数，也可以将 NEWID 函数指定为列的默认值。  
  
 [ {ADD | DROP} PERSISTED ]  
 指定在指定列中添加或删除 PERSISTED 属性。 该列必须是由确定性表达式定义的计算列。 对于指定为 PERSISTED 的列，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将以物理方式在表中存储计算值；并且，当更新了计算列依赖的任何其他列时，这些值也将被更新。 通过将计算列标记为 PERSISTED，可以对确定（但不精确）的表达式中定义的计算列创建索引。 有关详细信息，请参阅 [计算列上的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
 用作已分区表的分区依据列的任何计算列必须显式标记为 PERSISTED。  
  
 DROP NOT FOR REPLICATION  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定当复制代理执行插入操作时，标识列中的值将增加。 仅当可以指定此子句*column_name*是标识列。  
  
 SPARSE  
 指示列为稀疏列。 稀疏列已针对 NULL 值进行了存储优化。 不能将稀疏列指定为 NOT NULL。 将列从稀疏列转换为非稀疏列或者从非稀疏列转换为稀疏列会导致表在命令执行期间被锁定。 您可能需要使用 REBUILD 子句来回收任何节约的空间。 其他限制和稀疏列的详细信息，请参阅[使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。  
  
 添加掩码与 (函数 = *mask_function* )  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定动态数据掩码。 *mask_function*是使用适当的参数的屏蔽函数的名称。 三个函数均可用：  
  
-   default （)  
-   email()  
-   partial()  
-   random()  
  
 若要删除掩码，使用`DROP MASKED`。 函数参数，请参阅[动态数据屏蔽](../../relational-databases/security/dynamic-data-masking.md)。  
  
使用 (ONLINE = ON |OFF)\<是针对更改列 >  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 允许执行多次更改列操作，同时保持表可用。 默认为 OFF。 可以针对与数据类型、列长度或精度、为 Null 性、稀疏性和排序规则相关的列更改对行执行更改列。  
  
 联机更改列允许用户创建的统计信息和自动统计信息在 ALTER COLUMN 操作期间引用更改后的列。 这允许照常执行查询。 操作结束时，将删除引用列的自动统计信息，并且用户创建的统计信息将失效。 完成操作后，用户必须手动更新用户生成的统计信息。 如果列是任何统计信息或索引的筛选表达式的一部分，则无法执行 alter 列操作。  
  
-   联机更改列操作正在运行时，依赖列（索引和视图等）的所有操作都将因相应的错误而阻止或失败。 这保证联机更改列操作不会因在运行操作时引入依赖关系而失败。  
  
-   当更改后的列被非聚集索引引用时，联机操作中不支持将列从 NOT NULL 更改为 NULL。  
  
-   当检查约束引用了列，并且更改操作在限制列的精度（数值或日期时间）时，不支持联机更改。  
  
-   `WAIT_AT_LOW_PRIORITY` 选项不能与联机更改列同时使用。  
  
-   `ALTER COLUMN … ADD/DROP PERSISTED`不支持联机 alter 列。  
  
-   `ALTER COLUMN … ADD/DROP ROWGUIDCOL/NOT FOR REPLICATION`不受影响的联机 alter 列。  
  
-   启用了更改跟踪或作为合并复制的发布者时，联机更改列不支持对表进行更改。  
  
-   联机更改列不支持更改或更改为 CLR 数据类型。  
  
-   联机更改列不支持更改为架构集合不同于当前架构集合的 XML 数据类型。  
  
-   联机更改列不会减少对可更改列的时间的限制。 按索引/统计信息等进行引用可能会导致更改失败。  
  
-   联机更改列不支持同时更改多个列。  
  
-   联机 alter 列不起作用对于系统版本控制的临时表。 无论为 ONLINE 选项指定的值不是执行 ALTER 列。  
  
联机更改列具有与联机索引重新生成类似的要求、限制和功能。 这包括：  
  
-   当表包含旧 LOB 或文件流列，或表具有列存储索引时，不支持联机索引重新生成。 相同的限制也适用于联机更改列。  
  
-   正在更改的现有列需要两倍的空间分配，用于原始列和新创建的隐藏列。  
  
-   联机更改列操作的锁定策略遵循用于联机索引生成的相同锁定模式。  
  
WITH CHECK | WITH NOCHECK  
 指定表中的数据是否用新添加的或重新启用的 FOREIGN KEY 或 CHECK 约束进行验证。 如果未指定，对于新约束，假定为 WITH CHECK，对于重新启用的约束，假定为 WITH NOCHECK。  
  
 如果不想根据现有数据验证新的 CHECK 或 FOREIGN KEY 约束，请使用 WITH NOCHECK。 除极个别的情况外，建议不要进行这样的操作。 在以后所有数据更新中，都将计算该新约束。 如果添加约束时用 WITH NOCHECK 禁止了约束冲突，则将来使用不符合该约束的数据来更新行时，可能导致更新失败。  
  
 查询优化器不考虑使用 WITH NOCHECK 定义的约束。 在使用 `ALTER TABLE table WITH CHECK CHECK CONSTRAINT ALL` 重新启用这些约束之前，将忽略这些约束。  
  
 ADD  
 指定所添加一个或多个列定义、 计算的列定义或表约束，或系统将使用系统版本控制的列。  
  
 PERIOD FOR SYSTEM_TIME （system_start_time_column_name，system_end_time_column_name）  
 **适用于**:[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定系统将用于记录有效记录的期间列的名称。 可以指定现有列，或创建新列作为 ADD PERIOD FOR SYSTEM_TIME 自变量的一部分。 列必须具有数据类型 datetime2 和必须定义为 NOT NULL。 如果时间段列定义为 NULL，则将引发错误。 你可以定义[column_constraint &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)和/或[指定的列的默认值](../../relational-databases/tables/specify-default-values-for-columns.md)system_start_time 和 system_end_time 列。 请参阅示例 A 中的[系统版本控制](#system_versioning)演示 system_end_time 列的默认值用于下面的示例。  
  
 设置 SYSTEM_VERSIONING 参数结合使用此参数，以便在现有的表的系统版本控制。 有关详细信息，请参阅[临时表](../../relational-databases/tables/temporal-tables.md)和[Getting Started with Azure SQL 数据库中的临时表](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)。  
  
 在[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]，用户将能够将标记与一个或两个时间段列**HIDDEN**标志来隐式隐藏这些列以便 **选择\*FROM * * *\<表 >*不返回这些列的值。 默认情况下，未隐藏时间段列。 为了便于使用隐藏的列必须显式包含在直接引用临时表的所有查询。  
  
 DROP  
 指定的一个或多个列定义、 计算的列定义或表约束将被删除，或者若要删除的列，则系统将使用系统版本控制的规范。  
  
 CONSTRAINT *constraint_name*  
 指定*constraint_name*从表中删除。 可以列出多个约束。  
  
 约束的用户定义的或系统提供的名称可以通过查询来确定**sys.check_constraint**， **sys.default_constraints**， **sys.key_constraints**，和**sys.foreign_keys**目录视图。  
  
 如果表中存在 XML 索引，则不能删除 PRIMARY KEY 约束。  
  
 列*column_name*  
 指定*constraint_name*或*column_name*从表中删除。 可以列出多个列。  
  
 无法删除以下列：  
  
-   用于索引的列。  
  
-   用于 CHECK、FOREIGN KEY、UNIQUE 或 PRIMARY KEY 约束的列。  
  
-   与默认值（由 DEFAULT 关键字定义）相关联的列，或绑定到默认对象的列。  
  
-   绑定到规则的列。  
  
> [!NOTE]  
>  删除列并不回收列所占的磁盘空间。 当表的行大小接近或超过其限额时，必须回收已删除的列占用的磁盘空间。 通过对表创建聚集的索引或通过使用重新生成现有聚集的索引回收空间[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)。 有关删除 LOB 数据类型的影响的信息，请参阅此[CSS 博客条目](http://blogs.msdn.com/b/psssql/archive/2012/12/03/how-it-works-gotcha-varchar-max-caused-my-queries-to-be-slower.aspx)。  
  
 PERIOD FOR SYSTEM_TIME  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 将删除系统将使用系统版本控制的列的规范。  
  
 WITH \<drop_clustered_constraint_option>  
 指定设置一个或多个删除聚集约束选项。  
  
 MAXDOP = *max_degree_of_parallelism*  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 重写**最大并行度**仅用于该操作的持续时间的配置选项。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
 使用 MAXDOP 选项来限制执行并行计划时所用的处理器数量。 最大数量为 64 个处理器。  
  
 *max_degree_of_parallelism*可以是以下值之一：  
  
 1  
 取消生成并行计划。  
  
 \>1  
 将并行索引操作中使用的最大处理器数量限制为指定数量。  
  
 0（默认值）  
 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  并行索引操作不可用的每个版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[版本和 SQL Server 2016 的支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 联机 **=**  {ON |**OFF** }\<因为应用于 drop_clustered_constraint_option >  
 指定在索引操作期间基础表和关联的索引是否可用于查询和数据修改操作。 默认为 OFF。 REBUILD 可作为 ONLINE 操作执行。  
  
 ON  
 在索引操作期间不持有长期表锁。 在索引操作的主要阶段，源表上只使用意向共享 (IS) 锁。 这使得能够继续对基础表和索引进行查询或更新。 操作开始时，将对源对象保持极短时间的共享 (S) 锁。 操作结束时，如果创建非聚集索引，将在短期内对源获取 S（共享）锁；当联机创建或删除聚集索引时，以及重新生成聚集或非聚集索引时，将在短期内获取 SCH-M（架构修改）锁。 对本地临时表创建索引时，ONLINE 不能设置为 ON。 仅允许单线程堆重新生成操作。  
  
 若要执行的 DDL**交换机**或联机索引重新生成，所有活动阻止针对特定表运行的事务必须已完成。 在执行时，**交换机**或重新生成操作可以防止启动新事务和可能会有明显的影响的工作负荷吞吐量和临时延迟对基础表的访问。  
  
 OFF  
 在索引操作期间应用表锁。 创建、重新生成或删除聚集索引或者重新生成或删除非聚集索引的脱机索引操作将对表获取架构修改 (Sch-M) 锁。 这样可以防止所有用户在操作期间访问基础表。 创建非聚集索引的脱机索引操作将对表获取共享 (S) 锁。 这样可以防止更新基础表，但允许读操作（如 SELECT 语句）。 允许多线程堆重新生成操作。  
  
 有关详细信息，请参阅[联机索引操作的工作原理](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的各版本中均不提供联机索引操作。 有关详细信息，请参阅[版本和 SQL Server 2016 的支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 MOVE TO { *partition_scheme_name***(***column_name* [ 1**,** ... *n*] **)** | *filegroup* | **"**default**"** }  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定一个位置以移动聚集索引的叶级别中的当前数据行。 表被移至新位置。 此选项仅适用于创建聚集索引的约束。  
  
> [!NOTE]  
>  在此上下文中，default 不是关键字。 它是默认文件组的标识符和必须分隔，如下所示将移至**"**默认**"**或将移至**[**默认**]**。 如果**"**默认**"** QUOTED_IDENTIFIER 选项必须为当前会话中为 ON 的指定。 这是默认设置。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 { CHECK | NOCHECK } CONSTRAINT  
 指定*constraint_name*是启用还是禁用。 此选项只能与 FOREIGN KEY 和 CHECK 约束一起使用。 如果指定了 NOCHECK，则将禁用约束，从而在将来插入或更新列时，不根据约束条件进行验证。 无法禁用 DEFAULT、PRIMARY KEY 和 UNIQUE 约束。  
  
 ALL  
 指定使用 NOCHECK 选项禁用所有约束，或者使用 CHECK 选项启用所有约束。  
  
 { ENABLE | DISABLE } TRIGGER  
 指定*trigger_name*是启用还是禁用。 禁用触发器时，仍会为表定义该触发器；但是，当对表执行 INSERT、UPDATE 或 DELETE 语句时，除非重新启用触发器，否则不会执行触发器中的操作。  
  
 ALL  
 指定启用或禁用表中的所有触发器。  
  
 *trigger_name*  
 指定要启用或禁用的触发器的名称。  
  
 { ENABLE | DISABLE } CHANGE_TRACKING  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是启用还是禁用表的更改跟踪。 默认情况下会禁用更改跟踪。  
  
 只有对数据库启用了更改跟踪，此选项才可用。 有关详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
 若要启用更改跟踪，表必须具有一个主键。  
  
 WITH **(** TRACK_COLUMNS_UPDATED **=** { ON | **OFF** } **)**  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]是否跟踪哪些更改跟踪列已更新。 默认值为 OFF。  
  
 SWITCH [ PARTITION *source_partition_number_expression* ] TO [ *schema_name***.** ] *target_table* [ PARTITION *target_partition_number_expression* ]  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 用下列方式之一切换数据块：  
  
-   将表的所有数据作为分区重新分配给现有的已分区表。  
  
-   将分区从一个已分区表切换到另一个已分区表。  
  
-   将已分区表的一个分区中的所有数据重新分配给现有的未分区的表。  
  
如果*表*是一个已分区的表， *source_partition_number_expression*必须指定。 如果*target_table*已分区， *target_partition_number_expression*必须指定。 如果要将表的数据作为分区重新分配给现有的已分区表，或者将分区由一个已分区表切换到另一个已分区表，则目标分区必须存在，并且必须为空。  
  
 如果重新分配一个分区的数据以组成单个表，则必须已经创建了目标表，并且该表必须为空。 源表或分区以及目标表或分区必须在同一个文件组中。 对应的索引或索引分区也必须在同一个文件组中。 切换分区还有许多其他限制。 *表*和*target_table*不能相同。 *target_table*可以是多个部分组成的标识符。  
  
 *source_partition_number_expression*和*target_partition_number_expression*是可引用变量和函数的常量表达式。 其中包括用户定义类型变量和用户定义函数。 它们不能引用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表达式。  
  
 已分区的表具有聚集的而索引的行为类似分区堆：  
  
-   为主键必须包含分区键。  
  
-   唯一索引必须包含分区键。  请注意，如果包括到现有唯一索引的分区键，就可以更改唯一性。  
  
-   若要切换分区，所有非聚集索引必须包括的分区键。  
  
有关**交换机**限制时使用复制，请参阅[复制 Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
 为生成的非聚集列存储索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 CTP1，和之前版本 V12 已以只读格式的 SQL 数据库。 可以执行任何分区操作之前，则必须为当前格式 （这是可更新） 重新生成非聚集列存储索引。  
  
 SET **(** FILESTREAM_ON = { *partition_scheme_name* | *filestream_filegroup_name* |         **"**default**"** | **"**NULL**"** }**)**  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 |  
  
 指定 FILESTREAM 数据的存储位置。  
  
 带有 SET FILESTREAM_ON 子句的 ALTER TABLE 只有在表不包含任何 FILESTREAM 列时才会成功。 可以通过使用第二个 ALTER TABLE 语句添加 FILESTREAM 列。  
  
 如果*partition_scheme_name*指定的规则[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)应用。 表应该已经对行数据进行了分区，并且其分区方案必须使用与 FILESTREAM 分区方案相同的分区函数和分区列。  
  
 *filestream_filegroup_name*指定 FILESTREAM 文件组的名称。 文件组必须具有一个定义文件组的文件，通过使用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)引发语句或错误。  
  
 **"**默认**"**设置了默认属性中指定的 FILESTREAM 文件组。 如果没有 FILESTREAM 文件组，将引发错误。  
  
 **"**NULL**"**指定将删除对表的 FILESTREAM 文件组的所有引用。 首先必须删除所有 FILESTREAM 列。 你必须使用设置 FILESTREAM_ON**="**NULL**"**中删除所有与表相关联的 FILESTREAM 数据。  
  
 设置**(** SYSTEM_VERSIONING  **=**  {OFF |ON [(HISTORY_TABLE = schema_name。 history_table_name [ , DATA_CONSISTENCY_CHECK = { **ON** | OFF } ]  ) ] } **)**  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 禁用表的系统版本控制，或者启用系统版本控制的表。 若要启用系统版本控制的表，系统将验证满足了数据类型、 可为 null 约束和系统版本控制的主键约束要求。 如果未使用 HISTORY_TABLE 参数，系统将生成架构相匹配的当前表，创建两个表之间的链接的一个新的历史记录表，并使系统可以在历史记录表中的当前表中记录每个记录的历史记录。 此历史记录表的名称将`MSSQL_TemporalHistoryFor<primary_table_object_id>`。 如果 HISTORY_TABLE 自变量用于创建的链接并使用现有的历史记录表，当前表和指定的表之间创建链接。 创建现有历史记录表的链接时，可以选择执行数据一致性检查。 此数据一致性检查可确保现有记录不重叠。 系统默认执行数据一致性检查。 有关详细信息，请参阅 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)。  
  
HISTORY_RETENTION_PERIOD = {**无限**| 数 {天 |天 |周 | 周 |月 |月 |年份 |年}}**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  

在临时表中指定历史数据的有限或 infinte 保留的期。 如果省略，则假定无限期保留。
  
 设置**(** LOCK_ESCALATION = {自动 |表 |禁用} **)**  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定允许的对表的锁进行升级的方法。  
  
 AUTO  
 此选项允许 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]选择适合于表架构的锁升级粒度。  
  
-   如果该表已分区，则允许将锁升级到分区。 锁升级到分区级别之后，该锁以后将不会升级到 TABLE 粒度。  
  
-   如果该表未分区，则会将锁升级到 TABLE 粒度。  
  
TABLE  
 无论表是否已分区，都会在表级粒度完成锁升级。 默认值为 TABLE。  
  
 DISABLE  
 在大多数情况下禁止锁升级。 表级别的锁未完全禁止。 例如，当扫描在可序列化隔离级别下没有聚集索引的表时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]必须使用表锁来保证数据的完整性。  
  
 REBUILD  
 使用 REBUILD WITH 语法可重新生成包含分区表中的所有分区的整个表。 如果表具有聚集索引，则 REBUILD 选项将重新生成该聚集索引。 REBUILD 可作为 ONLINE 操作执行。  
  
 使用 REBUILD PARTITION 语法可重新生成分区表中的单个分区。  
  
 PARTITION = ALL  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 更改分区压缩设置时重新生成所有分区。  
  
 REBUILD WITH ( \<rebuild_option >)  
 为具有聚集索引的表应用所有选项。 如果表没有聚集索引，则只有部分选项会影响堆结构。  
  
 在未使用 REBUILD 操作指定特定的压缩设置时，使用针对分区的当前压缩设置。 若要返回的当前设置，请查询**data_compression**中的列**sys.partitions**目录视图。  
  
 有关重新生成选项的完整说明，请参阅[index_option &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md).  
  
 DATA_COMPRESSION  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 为指定的表、分区号或分区范围指定数据压缩选项。 选项如下所示：  
  
 无  
 不压缩表或指定的分区。 这不适用于列存储表。  
  
 ROW  
 使用行压缩来压缩表或指定的分区。 这不适用于列存储表。  
  
 PAGE  
 使用页压缩来压缩表或指定的分区。 这不适用于列存储表。  
  
 COLUMNSTORE  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 仅适用于列存储表。 COLUMNSTORE 指定对使用 COLUMNSTORE_ARCHIVE 选项压缩的分区进行解压缩。 在还原数据时，将继续通过用于所有列存储表的列存储压缩对数据进行压缩。  
  
 COLUMNSTORE_ARCHIVE  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 仅适用于列存储表，这是使用聚集列存储索引存储的表。 COLUMNSTORE_ARCHIVE 会进一步将指定分区压缩为更小的大小。 这可用于存档，或者用于要求更少存储并且可以付出更多时间来进行存储和检索的其他情形  
  
 若要在同一时间重新生成多个分区，请参阅[index_option &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md). 如果表没有聚集索引，则更改数据压缩会重新生成堆和非聚集索引。 有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
 联机 **=**  {ON |**OFF** }\<因为应用于 single_partition_rebuild_option >  
 指定在索引操作期间基础表的单个分区和关联索引是否可用于查询和数据修改操作。 默认为 OFF。 REBUILD 可作为 ONLINE 操作执行。  
  
 ON  
 在索引操作期间不持有长期表锁。 索引重新生成开始时表上需要一个 S 锁，联机重新生成索引结束时表上需要一个 Sch-M 锁。 不过两个锁都是短的元数据锁，特别是 Sch-M 锁必须等待所有阻塞事务完成。 在等待期间，Sch-M 锁在访问同一表时阻止在此锁后等待的所有其他事务。  
  
> [!NOTE]  
>  联机索引重新生成可以设置*low_priority_lock_wait*此部分后面所述的选项。  
  
 OFF  
 在索引操作期间应用表锁。 这样可以防止所有用户在操作期间访问基础表。  
  
 *column_set_name* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 列集的名称。 列集是一种非类型化的 XML 表示形式，它将表的所有稀疏列合并为一种结构化的输出。 如果某个表包含稀疏列，则不能向该表添加列集。 有关列集的详细信息，请参阅[使用列集](../../relational-databases/tables/use-column-sets.md)。  
  
 { ENABLE | DISABLE } FILETABLE_NAMESPACE  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 启用或禁用针对 FileTable 的系统定义约束。 仅可与 FileTable 一起使用。  
  
 设置 (FILETABLE_DIRECTORY = *directory_name* )  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定与 Windows 兼容的 FileTable 目录名称。 此名称应在数据库的所有 FileTable 目录名称中唯一。 无论 SQL 排序规则如何设置，唯一性比较都不区分大小写。 仅可与 FileTable 一起使用。  
```    
 SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options> )  
          | = OFF_WITHOUT_DATA_RECOVERY  
          ( MIGRATION_STATE = PAUSED ) | ( <table_stretch_options> [, ...n] )  
        } )  
```    
**适用于**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 启用或禁用表的 Stretch Database。 有关详细信息，请参阅 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
 **为表启用 Stretch Database**  
  
 如果你启用 Stretch 的表通过指定`ON`，你还必须指定`MIGRATION_STATE = OUTBOUND`开始将数据迁移立即或`MIGRATION_STATE = PAUSED`以推迟数据迁移。 默认值是`MIGRATION_STATE = OUTBOUND`。 有关启用 Stretch 的表的详细信息，请参阅[为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。  
  
 **先决条件**。 为表启用 Stretch 之前，必须在服务器和数据库上启用 Stretch。 有关详细信息，请参阅 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **权限**。 为数据库或表启用 Stretch 需要 db_owner 权限。 为表启用 Stretch 也需要对表的 ALTER 权限。  
  
 **禁用表的 Stretch Database**  
  
 当你禁用表的 Stretch 时，你有两个已迁移到 Azure 的远程数据选项。 有关详细信息，请参阅 [禁用 Stretch Database 并恢复远程数据](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
-   要禁用表的拉伸或将表中的远程数据从 Azure 复制回 SQL Server，请运行以下命令。 此命令不能取消。  
  
    ```sql  
ALTER TABLE \<table name>
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;  
    ```  
  
     此操作会产生数据传输成本，并且不能取消。 有关详细信息，请参阅 [数据传输定价详细信息](https://azure.microsoft.com/en-us/pricing/details/data-transfers/)。  
  
     当所有远程数据已从 Azure 复制回 SQL Server 后，禁用表的“拉伸”。  
  
-   要禁用表的“拉伸”并放弃远程数据，请运行以下命令。  
  
    ```sql  
ALTER TABLE \<table_name>
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ;  
    ```  
  
 禁用表的 Stretch Database 之后，将停止数据迁移，查询结果不再包括远程表中的结果。  
  
 禁用 Stretch 不会删除远程表。 如要删除远程表，必须使用 Azure 管理门户进行删除。  
  
[ FILTER_PREDICATE = { null | *predicate* } ]  
 **适用于**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 （可选） 指定筛选器谓词以选择要从表包含历史和当前数据迁移的行。 该谓词必须调用的确定性内联表值函数。 有关详细信息，请参阅[为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)和[选择要使用筛选器函数 &#40; 迁移的行Stretch Database &#41;](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).   
  
> [!IMPORTANT]  
>  如果提供的筛选器谓词性能不佳，则数据迁移性能也不佳。 Stretch Database 通过使用 CROSS APPLY 运算符将筛选器谓词应用到表。  
  
 如果未指定筛选器谓词，则将迁移整个表。  
  
 当指定筛选器谓词时，你还必须指定*MIGRATION_STATE*。  
  
 MIGRATION_STATE = {出站 | 入站 |暂停}  
 **适用于**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   指定`OUTBOUND`将数据从 SQL Server 迁移到 Azure。  
  
-   指定`INBOUND`复制远程数据从 Azure 表备份到 SQL Server 并以禁用该表的 Stretch。 有关详细信息，请参阅 [禁用 Stretch Database 并恢复远程数据](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
     此操作会产生数据传输成本，并且不能取消。  
  
-   指定`PAUSED`若要暂停或推迟数据迁移。 有关详细信息，请参阅[暂停和恢复数据迁移 &#40;Stretch Database &#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
WAIT_AT_LOW_PRIORITY  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 联机索引重新生成必须等待对此表执行的阻塞操作。 **WAIT_AT_LOW_PRIORITY**指示联机索引重新生成操作将等待低优先级锁，从而允许同时联机索引生成操作正在等待继续其他操作。 省略**等待在低优先级**选项等同于`WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。  
  
 MAX_DURATION = *time* [**MINUTES** ]  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 在等待时间 （以分钟为单位指定的整数值），**交换机**或执行 DDL 命令时，联机索引重新生成锁将等待低优先级。 如果该操作被阻止的**MAX_DURATION**时间、 之一**ABORT_AFTER_WAIT**将执行操作。 **MAX_DURATION**时间始终是以分钟和 word**分钟**可以省略。  
  
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
 **适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 无  
 继续以普通（常规）优先级等待锁。  
  
 SELF  
 退出**交换机**或联机索引重新生成 DDL 操作当前正在执行而不采取任何操作。  
  
 BLOCKERS  
 终止当前阻止的所有用户事务**交换机**或联机索引重新生成 DDL 操作，以便可以继续该操作。  
  
 需要**ALTER ANY CONNECTION**权限。  
  
如果存在  
 **适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)) 和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 有条件地删除列或约束，仅当它已存在。  
  
## <a name="remarks"></a>注释  
 若要添加新的数据行，使用[插入](../../t-sql/statements/insert-transact-sql.md)。 若要删除的数据行，使用[删除](../../t-sql/statements/delete-transact-sql.md)或[TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md)。 若要更改现有行中的值，使用[更新](../../t-sql/queries/update-transact-sql.md)。  
  
 如果过程高速缓存中存在引用表的执行计划，ALTER TABLE 会将这些执行计划标记为下次执行时重新编译。  
  
## <a name="changing-the-size-of-a-column"></a>更改列的大小  
 可以通过在 ALTER COLUMN 子句中指定列数据类型的新大小来更改列的长度、精度或小数位数。 如果列中存在数据，则新大小不能小于数据的最大大小。 此外，不能将列定义在索引中，除非列是**varchar**， **nvarchar**，或**varbinary**数据类型和索引并不是主键的结果约束。 请参见示例 P。  
  
## <a name="locks-and-alter-table"></a>锁和 ALTER TABLE  
 ALTER TABLE 语句指定的更改将立即实现。 如果这些更改需要修改表中的行，ALTER TABLE 将更新这些行。 ALTER TABLE 将获取表上的架构修改 (SCH-M) 锁，以确保在更改期间没有其他连接引用（甚至是该表的元数据，也不引用），但可在结束时执行需要一个极短的 SCH-M 锁的联机索引操作。 在`ALTER TABLE…SWITCH`操作，锁获取对源和目标表。 对表进行的更改将记录于日志中，并且可以完整恢复。 影响在非常大的表中，如删除列，或在某些版本上的所有行的更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，添加具有默认值的 NOT NULL 列，可能需要很长时间才能完成并生成大量日志记录。 像慎重执行影响许多行的任何 INSERT、UPDATE 或者 DELETE 语句一样，应慎重执行这些 ALTER TABLE 语句。  
  
### <a name="adding-not-null-columns-as-an-online-operation"></a>以联机操作的形式添加 NOT NULL 列  
 从开始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Enterprise Edition 中，添加具有默认值的 NOT NULL 列一个联机操作的默认值时*运行时常量*。 这意味着不论表中有多少行都几乎可以在瞬间完成该操作。 这是因为表中的现有行在操作期间不更新；相反，默认值仅存储在该表的元数据中，并且按需在访问这些行的查询中查找该值。 这种行为是自动的；无需在 ADD COLUMN 语法之外额外执行其他语法来执行该联机操作。 运行时常量是一个表达式，它可以在运行时为表中的每行生成相同的值，而与其确定性无关。 例如，常量表达式“My temporary data”或系统函数 GETUTCDATETIME() 均为运行时常量。 相比之下，函数`NEWID()`或`NEWSEQUENTIALID()`不运行时常量，因为针对表中的每一行生成唯一值。 添加具有非运行时常量的默认值的 NOT NULL 列始终脱机执行，并且在该操作期间需要一个排他 (SCH-M) 锁。  
  
 尽管现有行引用元数据中存储的值，但对于插入的任何新行，默认值存储在该行中，并且不为该列指定其他值。 更新现有行时（即便在 UPDATE 语句中未指定实际列），或是重新生成表或聚集索引时，存储在元数据中的默认值将移至该行。  
  
 类型的列**varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**，**文本**， **ntext**，**映像**， **hierarchyid**，**几何图形**， **geography**，或 CLR UDT，不能在联机操作中添加。 如果在联机操作中添加这些列，将导致最大可能行大小超过 8,060 字节的限制。 在这种情况下将在脱机操作中添加列。  
  
## <a name="parallel-plan-execution"></a>并行计划执行  
 在[!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)]和更高版本，处理器数运行所使用单个 ALTER TABLE ADD （索引基于） 约束或约束，DROP （聚集索引） 语句由**最大并行度**配置选项和当前的工作负荷。 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]检测到系统正忙，则在语句执行开始之前将自动降低操作并行度。 可以通过指定 MAXDOP 选项，手动配置用于运行此语句的处理器数。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
## <a name="partitioned-tables"></a>已分区表  
 除了执行涉及到已分区表的 SWITCH 操作外，ALTER TABLE 还可用于更改已分区表的列、约束和触发器的状态，就像它用于非分区表一样。 但是，该语句不能用于更改表本身进行分区的方式。 若要进行重新分区已分区的表，使用[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)和[ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)。 此外，不能更改已分区表中列的数据类型。  
  
## <a name="restrictions-on-tables-with-schema-bound-views"></a>对包含绑定到架构视图的表的限制  
 应用于包含架构绑定视图的表的 ALTER TABLE 语句的限制，与当前修改包含简单索引的表时应用的限制相同。 允许添加列。 但是，不允许删除或更改参与任何绑定到架构视图的列。 如果 ALTER TABLE 语句要求更改用于架构绑定视图中的列，ALTER TABLE 将失败，并且[!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误消息。 有关架构绑定和索引的视图的详细信息，请参阅[创建的视图 &#40;Transact SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 创建引用表的架构绑定视图不会影响为基表添加或删除触发器。  
  
## <a name="indexes-and-alter-table"></a>索引和 ALTER TABLE  
 删除约束时，作为约束的一部分而创建的索引也将被删除。 必须使用 DROP INDEX 删除由 CREATE INDEX 创建的索引。 ALTER INDEX 语句可用于重新生成约束定义的索引部分；而不必再使用 ALTER TABLE 来删除和添加约束。  
  
 必须在删除所有基于列的索引和约束之后，才能删除列。  
  
 如果删除了创建聚集索引的约束，则存储在聚集索引叶级别的数据行将存储在非聚集表中。 通过指定 MOVE TO 选项，可以在单个事务中删除聚集索引并将生成的表移动到另一个文件组或分区方案。 MOVE TO 选项有以下限制：  
  
-   MOVE TO 对索引视图或非聚集索引无效。  
-   分区方案或文件组必须已经存在。  
-   如果没有指定 MOVE TO，则表将位于为聚集索引定义的同一分区方案或文件组中。  
  
当删除聚集的索引时，你可以指定联机 **=** 上选项，以便 DROP INDEX 事务不会阻止查询和修改对基础数据和关联的非聚集的索引。  
  
联机 **=** 上具有以下限制：  
 
-   联机 **=**  ON 无效，不能也被禁用的聚集索引。 必须使用联机删除禁用的索引 **=**  OFF。  
-   一次只能删除一个索引。  
-   联机 **=**  ON 对索引的视图、 非聚集索引或本地临时表的索引无效。  
-   联机 **=**  ON 不是有效的列存储索引。  
  
删除聚集索引时，需要大小等于现有聚集索引的大小的临时磁盘空间。 操作完成后，即可释放此额外空间。  
  
> [!NOTE]  
>  下面列出的选项 *\<drop_clustered_constraint_option >*应用于表的聚集索引并不能应用于聚集的索引视图或多个非聚集的索引。  
  
## <a name="replicating-schema-changes"></a>复制架构更改  
 默认情况下，当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器中对发布的表运行 ALTER TABLE 时，此更改将传播到所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。 此功能存在一些限制并可禁用。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="data-compression"></a>Data Compression  
 不能为系统表启用压缩功能。 如果表是堆，ONLINE 模式的重新生成操作将在单个线程内完成。 请为多线程堆重新生成操作使用 OFFLINE 模式。 有关数据压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
 若要评估更改压缩状态将对表、索引或分区有何影响，请使用 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 存储过程。  
  
 以下限制适用于已分区表：  
  
-   如果表具有非对齐索引，则无法更改单个分区的压缩设置。  
-   ALTER TABLE\<表 > 重新生成分区...语法重新生成指定的分区。  
-   ALTER TABLE\<表 > REBUILD WITH...语法重新生成所有分区。  
  
## <a name="dropping-ntext-columns"></a>删除 NTEXT 列  
 删除 NTEXT 列时，将以序列化操作的形式在所有行中清除所删除的数据。 此过程可能耗时漫长。 在有大量行的表中删除 NTEXT 列时，首先将 NTEXT 列更新为 NULL 值，然后再删除该列。 此操作可同时与其他操作一起执行，这样做可大幅提高速度。  
  
## <a name="online-index-rebuild"></a>联机索引重新生成  
 要执行联机索引重新生成的 DDL 语句，必须完成对某一特定表运行的所有活动阻塞事务。 在联机索引重新生成执行时，它会阻塞准备对此表执行的所有新事务。 尽管联机索引重新生成锁的持续时间非常短，但等待某一给定表的所有打开的事务完成并阻塞新事务启动可能对吞吐量造成很大影响，导致工作负荷变慢或超时，并严重限制对基础表的访问。 **WAIT_AT_LOW_PRIORITY**选项允许数据库管理员的管理所需的联机索引重新生成，并允许他们选择 3 个选项之一的 S 锁和 SCH-M 锁。 在所有 3 种情况下，如果等待期间 ( `(MAX_DURATION =n [minutes])` ) 没有阻塞活动，则联机索引重新生成会立即执行，而不等待 DDL 语句完成。  
  
## <a name="compatibility-support"></a>兼容性支持  
 ALTER TABLE 语句只允许两部分的表名称 (schema.object)。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用以下格式指定表名称时，在编译时会出现错误 117。  
  
-   server.database.schema.table  
-   .database.schema.table  
-   ..schema.table  
  
在早期版本中指定格式 server.database.schema.table 会返回错误 4902。 指定格式 .database.schema.table 或 ..schema.table 则会成功。  
  
要解决此问题，请不要使用 4 部分的前缀。  
  
## <a name="permissions"></a>权限  
 需要对表的 ALTER 权限。  
  
 ALTER TABLE 权限适用于 ALTER TABLE SWITCH 语句涉及的两个表。 任何已切换的数据都将继承目标表的安全性。  
  
 如果将 ALTER TABLE 语句中的任何列定义为公共语言运行时 (CLR) 用户定义类型或别名数据类型，都需要对该类型有 REFERENCES 权限。  
  
 添加将更新表的行的列，则需要**更新**对表的权限。 例如，添加**NOT NULL**与默认值或表不为空时添加标识列的列。  
  
##  <a name="Example_Top"></a> 示例  
  
|类别|作为特征的语法元素|  
|--------------|------------------------------|  
|[添加列和约束](#add)|ADD • PRIMARY KEY 以及索引选项 • 稀疏列和列集 •|  
|[删除列和约束](#Drop)|DROP|  
|[更改列定义](#alter_column)|更改数据类型 • 更改列大小 • 排序规则|  
|[更改表定义](#alter_table)|DATA_COMPRESSION • SWITCH PARTITION • LOCK ESCALATION • 更改跟踪|  
|[禁用和启用的约束和触发器](#disable_enable)|CHECK • NO CHECK • ENABLE TRIGGER • DISABLE TRIGGER|  
  
###  <a name="add"></a>添加列和约束  
 本节中的示例说明将列和约束添加到表中。  
  
#### <a name="a-adding-a-new-column"></a>A. 添加新列  
 以下示例将添加一个允许 Null 值的列，而且没有通过 DEFAULT 定义提供的值。 在该新列中，每一行都将有 `NULL` 值。  
  
```sql  
CREATE TABLE dbo.doc_exa (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL ;  
GO  
```  
  
#### <a name="b-adding-a-column-with-a-constraint"></a>B. 添加包含约束的列  
 以下示例将添加一个包含 `UNIQUE` 约束的新列。  
  
```sql  
CREATE TABLE dbo.doc_exc (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exc ADD column_b VARCHAR(20) NULL   
    CONSTRAINT exb_unique UNIQUE ;  
GO  
EXEC sp_help doc_exc ;  
GO  
DROP TABLE dbo.doc_exc ;  
GO  
```  
  
#### <a name="c-adding-an-unverified-check-constraint-to-an-existing-column"></a>C. 在现有列中添加一个未经验证的 CHECK 约束  
 下面的示例将在表中的现有列中添加一个约束。 该列包含一个违反约束的值。 因此，将使用 `WITH NOCHECK` 以避免根据现有行验证该约束，从而允许添加该约束。  
  
```sql  
CREATE TABLE dbo.doc_exd ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exd VALUES (-1) ;  
GO  
ALTER TABLE dbo.doc_exd WITH NOCHECK   
ADD CONSTRAINT exd_check CHECK (column_a > 1) ;  
GO  
EXEC sp_help doc_exd ;  
GO  
DROP TABLE dbo.doc_exd ;  
GO  
```  
  
#### <a name="d-adding-a-default-constraint-to-an-existing-column"></a>D. 在现有列中添加一个 DEFAULT 约束  
 下面的示例将创建一个包含两列的表，在第一列插入一个值，另一列保持为 NULL。 然后在第二列中添加一个 `DEFAULT` 约束。 验证是否已应用了默认值，另一个值是否已插入第一列以及是否已查询表。  
  
```sql  
CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
GO  
INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
GO  
ALTER TABLE dbo.doc_exz  
ADD CONSTRAINT col_b_def  
DEFAULT 50 FOR column_b ;  
GO  
INSERT INTO dbo.doc_exz (column_a) VALUES ( 10 ) ;  
GO  
SELECT * FROM dbo.doc_exz ;  
GO  
DROP TABLE dbo.doc_exz ;  
GO  
```  
  
#### <a name="e-adding-several-columns-with-constraints"></a>E. 添加多个包含约束的列  
 以下示例将添加多个包含随新列定义的约束的列。 第一个新列具有 `IDENTITY` 属性。 表中的每一行在标识列中都有新的增量值。  
  
```sql  
CREATE TABLE dbo.doc_exe ( column_a INT CONSTRAINT column_a_un UNIQUE) ;  
GO  
ALTER TABLE dbo.doc_exe ADD   
  
-- Add a PRIMARY KEY identity column.  
column_b INT IDENTITY  
CONSTRAINT column_b_pk PRIMARY KEY,   
  
-- Add a column that references another column in the same table.  
column_c INT NULL    
CONSTRAINT column_c_fk   
REFERENCES doc_exe(column_a),  
  
-- Add a column with a constraint to enforce that   
-- nonnull data is in a valid telephone number format.  
column_d VARCHAR(16) NULL   
CONSTRAINT column_d_chk  
CHECK   
(column_d LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' OR  
column_d LIKE  
'([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]'),  
  
-- Add a nonnull column with a default.  
column_e DECIMAL(3,3)  
CONSTRAINT column_e_default  
DEFAULT .081 ;  
GO  
EXEC sp_help doc_exe ;  
GO  
DROP TABLE dbo.doc_exe ;  
GO  
```  
  
#### <a name="f-adding-a-nullable-column-with-default-values"></a>F. 添加包含默认值的可为空的列  
 下面的示例将添加一个包含 `DEFAULT` 定义的可为 Null 的列，并使用 `WITH VALUES` 为表中的各个现有行提供值。 如果没有使用 WITH VALUES，那么每一行的新列中都将包含 NULL 值。  
  
```sql  
CREATE TABLE dbo.doc_exf ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exf VALUES (1) ;  
GO  
ALTER TABLE dbo.doc_exf   
ADD AddDate smalldatetime NULL  
CONSTRAINT AddDateDflt  
DEFAULT GETDATE() WITH VALUES ;  
GO  
DROP TABLE dbo.doc_exf ;  
GO  
```  
  
#### <a name="g-creating-a-primary-key-constraint-with-index-options"></a>G. 创建包含索引选项的 PRIMARY KEY 约束  
 下面的示例将创建 PRIMARY KEY 约束 `PK_TransactionHistoryArchive_TransactionID`，并设置 `FILLFACTOR`、`ONLINE` 和 `PAD_INDEX` 选项。 生成的聚集索引将与约束同名。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK   
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);  
GO  
```  
  
#### <a name="h-adding-a-sparse-column"></a>H. 添加稀疏列  
 下面的示例演示如何在表 T1 中添加和修改稀疏列。 创建表 `T1` 的代码如下所示。  
  
```sql  
CREATE TABLE T1  
(C1 int PRIMARY KEY,  
C2 varchar(50) SPARSE NULL,  
C3 int SPARSE NULL,  
C4 int ) ;  
GO  
```  
  
 若要添加另一个稀疏列 `C5`，请执行以下语句。  
  
```sql  
ALTER TABLE T1  
ADD C5 char(100) SPARSE NULL ;  
GO  
```  
  
 若要将 `C4` 非稀疏列转换为稀疏列，请执行以下语句。  
  
```sql  
ALTER TABLE T1  
ALTER COLUMN C4 ADD SPARSE ;  
GO  
```  
  
 要转换`C4`稀疏列的稀疏列，执行以下语句。  
  
```sql  
ALTER TABLE T1  
ALTER COLUMN C4 DROP SPARSE;  
GO  
```  
  
#### <a name="i-adding-a-column-set"></a>I. 添加列集  
 下面的示例演示如何向表 `T2` 中添加一列。 如果表已包含稀疏列，则不能向该表添加列集。 创建表 `T2` 的代码如下所示。  
  
```sql  
CREATE TABLE T2  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 下面的三个语句添加名为 `CS` 的列集，然后将列 `C2` 和 `C3` 修改为 `SPARSE`。  
  
```sql  
ALTER TABLE T2  
ADD CS XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ;  
GO  
  
ALTER TABLE T2  
ALTER COLUMN C2 ADD SPARSE ;   
GO  
  
ALTER TABLE T2  
ALTER COLUMN C3 ADD SPARSE ;  
GO  
```  
  
#### <a name="j-adding-an-encrypted-column"></a>J. 添加加密的列  
 以下语句将添加名为的加密的列`PromotionCode`。  
  
```sql  
ALTER TABLE Customers ADD  
    PromotionCode nvarchar(100)   
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
    ENCRYPTION_TYPE = RANDOMIZED,  
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;  
```  
  
###  <a name="Drop"></a>删除列和约束  
 本节中的示例说明如何删除列和约束。  
  
#### <a name="a-dropping-a-column-or-columns"></a>A. 删除一列或多列  
 第一个示例将修改一个表以删除列。 第二个示例删除多列。  
  
```sql  
CREATE TABLE dbo.doc_exb   
    (column_a INT  
     ,column_b VARCHAR(20) NULL  
     ,column_c datetime  
     ,column_d int) ;  
GO  
-- Remove a single column.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
GO  
-- Remove multiple columns.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;  
```  
  
#### <a name="b-dropping-constraints-and-columns"></a>B. 删除约束和列  
 第一个示例将从表中删除 `UNIQUE` 约束。 第二个示例将删除两个约束和一列。  
  
```sql  
CREATE TABLE dbo.doc_exc ( column_a int NOT NULL CONSTRAINT my_constraint UNIQUE) ;  
GO  
  
-- Example 1. Remove a single constraint.  
ALTER TABLE dbo.doc_exc DROP my_constraint ;  
GO  
  
DROP TABLE dbo.doc_exc;  
GO  
  
CREATE TABLE dbo.doc_exc ( column_a int    
                          NOT NULL CONSTRAINT my_constraint UNIQUE  
                          ,column_b int   
                          NOT NULL CONSTRAINT my_pk_constraint PRIMARY KEY) ;  
GO  
  
-- Example 2. Remove two constraints and one column  
-- The keyword CONSTRAINT is optional. The keyword COLUMN is required.  
ALTER TABLE dbo.doc_exc   
  
    DROP CONSTRAINT CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;  
GO  
```  
  
#### <a name="c-dropping-a-primary-key-constraint-in-the-online-mode"></a>C. 在 ONLINE 模式下删除 PRIMARY KEY 约束  
 下面的示例在 `ONLINE` 选项设置为 `ON` 的情况下删除 PRIMARY KEY 约束。  
  
```sql  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
GO  
```  
  
#### <a name="d-adding-and-dropping-a-foreign-key-constraint"></a>D. 添加和删除 FOREIGN KEY 约束  
 下面的示例将创建 `ContactBackup` 表，然后更改此表。首先添加引用 `FOREIGN KEY` 表的 `Person.Person` 约束，然后再删除 `FOREIGN KEY` 约束。  
  
```sql  
CREATE TABLE Person.ContactBackup  
    (ContactID int) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
ADD CONSTRAINT FK_ContactBacup_Contact FOREIGN KEY (ContactID)  
    REFERENCES Person.Person (BusinessEntityID) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
DROP CONSTRAINT FK_ContactBacup_Contact ;  
GO  
  
DROP TABLE Person.ContactBackup ;  
```  
  
 ![用于回顶部链接的箭头图标](../../analysis-services/instances/media/uparrow16x16.gif "用于回顶部链接的箭头图标")[示例](#Example_Top)  
  
###  <a name="alter_column"></a>更改列定义  
  
#### <a name="a-changing-the-data-type-of-a-column"></a>A. 更改列的数据类型  
 下面的示例将表中列的数据类型由 `INT` 改为 `DECIMAL`。  
  
```sql  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
GO  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
#### <a name="b-changing-the-size-of-a-column"></a>B. 更改列的大小  
 下面的示例会增加的大小**varchar**列的精度和小数位数**十进制**列。 因为列包含数据，所以只能增加列的大小。 此外，请注意：`col_a` 是在一个唯一索引中定义的。 大小`col_a`因为数据类型仍可以增加**varchar**和索引不是 PRIMARY KEY 约束的结果。  
  
```sql  
-- Create a two-column table with a unique index on the varchar column.  
CREATE TABLE dbo.doc_exy ( col_a varchar(5) UNIQUE NOT NULL, col_b decimal (4,2));  
GO  
INSERT INTO dbo.doc_exy VALUES ('Test', 99.99);  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
GO  
-- Increase the size of the varchar column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_a varchar(25);  
GO  
-- Increase the scale and precision of the decimal column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_b decimal (10,4);  
GO  
-- Insert a new row.  
INSERT INTO dbo.doc_exy VALUES ('MyNewColumnSize', 99999.9999) ;  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
```  
  
#### <a name="c-changing-column-collation"></a>C. 更改列排序规则  
 下面的示例说明了如何更改列的排序规则。 首先，我们创建一个表以及默认的用户排序规则：  
  
```sql  
CREATE TABLE T3  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 接着，将列 `C2` 排序规则更改为 Latin1_General_BIN。 请注意，需要数据类型，即使排序规则未更改也不例外。  
  
```sql  
ALTER TABLE T3  
ALTER COLUMN C2 varchar(50) COLLATE Latin1_General_BIN;  
GO  
```  
  
###  <a name="alter_table"></a>更改表定义  
 本节中的示例说明如何更改表定义。  
  
#### <a name="a-modifying-a-table-to-change-the-compression"></a>A. 修改表以更改压缩  
 下面的示例更改未分区表的压缩。 将会重新生成堆或聚集索引。 如果表是一个堆，将重新生成所有非聚集索引。  
  
```sql  
ALTER TABLE T1   
REBUILD WITH (DATA_COMPRESSION = PAGE);  
```  
  
 下面的示例更改已分区表的压缩。 `REBUILD PARTITION = 1` 语法仅仅导致重新生成编号为 `1` 的分区。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  NONE) ;  
GO  
```  
  
使用以下替代语法的相同操作则会导致重新生成表中的所有分区。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = ALL   
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1) ) ;  
```  
  
 有关其他数据压缩示例，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
#### <a name="b-modifying-a-columnstore-table-to-change-archival-compression"></a>B. 修改列存储表以便更改存档压缩  
 下面的示例通过应用附加的压缩算法，进一步压缩列存储表分区。 这会缩小表大小，但也增加了存储和检索所需的时间。 这可用于存档，或者用于要求更少空间并且可以付出更多时间来进行存储和检索的其他情形。  
  
**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
GO  
```  
  
下面的示例解压缩已使用 COLUMNSTORE_ARCHIVE 选项进行了压缩的列存储表分区。 在还原数据时，将继续通过用于所有列存储表的列存储压缩对数据进行压缩。  
  
**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
GO  
```  
  
#### <a name="c-switching-partitions-between-tables"></a>C. 在表之间切换分区  
 以下示例创建一个已分区表，并假定在数据库中已经创建了分区方案 `myRangePS1`。 然后，在 `PARTITION 2` 表的 `PartitionTable` 所在的同一文件组中，创建与已分区表结构相同的未分区的表。 最后，将 `PARTITION 2` 表的 `PartitionTable` 中的数据切换到 `NonPartitionTable` 表中。  
  
```sql  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
ON myRangePS1 (col1) ;  
GO  
CREATE TABLE NonPartitionTable (col1 int, col2 char(10))  
ON test2fg ;  
GO  
ALTER TABLE PartitionTable SWITCH PARTITION 2 TO NonPartitionTable ;  
GO  
```  
  
#### <a name="d-allowing-lock-escalation-on-partitioned-tables"></a>D. 允许已分区表中的锁升级  
 以下示例在已分区表的分区级别启用锁升级。 如果该表未分区，则会在 TABLE 级别设置锁升级。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE dbo.T1 SET (LOCK_ESCALATION = AUTO);  
GO  
```  
  
#### <a name="e-configuring-change-tracking-on-a-table"></a>E. 配置表的更改跟踪  
 下面的示例对 `Person.Person` 表启用了更改跟踪。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
USE AdventureWorks2012;  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING;  
```  
  
下面的示例启用更改跟踪，并启用在进行某项更改期间会进行更新的列的跟踪。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
下面的示例对 `Person.Person` 表禁用更改跟踪。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
USE AdventureWorks2012;  
Go  
ALTER TABLE Person.Person  
DISABLE CHANGE_TRACKING;  
```  

###  <a name="disable_enable"></a>禁用和启用的约束和触发器  
  
#### <a name="a-disabling-and-re-enabling-a-constraint"></a>A. 禁用和重新启用约束  
 以下示例中禁用了用于限制数据中所接受薪水的约束。 `NOCHECK CONSTRAINT` 与 `ALTER TABLE` 一起使用以禁用该约束，从而允许执行通常会违反约束的插入操作。 `CHECK CONSTRAINT` 重新启用约束。  
  
```sql  
CREATE TABLE dbo.cnst_example   
(id INT NOT NULL,  
 name VARCHAR(10) NOT NULL,  
 salary MONEY NOT NULL  
    CONSTRAINT salary_cap CHECK (salary < 100000)  
);  
  
-- Valid inserts  
INSERT INTO dbo.cnst_example VALUES (1,'Joe Brown',65000);  
INSERT INTO dbo.cnst_example VALUES (2,'Mary Smith',75000);  
  
-- This insert violates the constraint.  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Disable the constraint and try again.  
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Re-enable the constraint and try another insert; this will fail.  
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (4,'Eric James',110000) ;  
```  
  
#### <a name="b-disabling-and-re-enabling-a-trigger"></a>B. 禁用和重新启用触发器  
 下面的示例将使用 `DISABLE TRIGGER` 的 `ALTER TABLE` 选项来禁用触发器，以允许执行通常会违反此触发器的插入操作。 然后，使用 `ENABLE TRIGGER` 重新启用触发器。  
  
```sql  
CREATE TABLE dbo.trig_example   
(id INT,   
name VARCHAR(12),  
salary MONEY) ;  
GO  
-- Create the trigger.  
CREATE TRIGGER dbo.trig1 ON dbo.trig_example FOR INSERT  
AS  
IF (SELECT COUNT(*) FROM INSERTED  
WHERE salary > 100000) > 0  
BEGIN  
    print 'TRIG1 Error: you attempted to insert a salary > $100,000'  
    ROLLBACK TRANSACTION  
END ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (1,'Pat Smith',100001) ;  
GO  
-- Disable the trigger.  
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;  
GO  
-- Try an insert that would typically violate the trigger.  
INSERT INTO dbo.trig_example VALUES (2,'Chuck Jones',100001) ;  
GO  
-- Re-enable the trigger.  
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (3,'Mary Booth',100001) ;  
GO  
```  
 
### <a name="online"></a>联机操作  
  
#### <a name="a-online-index-rebuild-using-low-priority-wait-options"></a>A. 使用低优先级等待选项的联机索引重新生成  
 下面的示例显示如何执行指定低优先级等待选项的联机索引重新生成。  
  
**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
ALTER TABLE T1   
REBUILD WITH   
(  
    PAD_INDEX = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, 
                                         ABORT_AFTER_WAIT = BLOCKERS ) )  
)  
;  
```  
  
#### <a name="b-online-alter-column"></a>B. 联机更改列  
 下面的示例显示使用“联机”选项执行更改列操作。  
  
**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy   
    ALTER COLUMN column_a DECIMAL (5, 2) WITH (ONLINE = ON);  
GO  
sp_help doc_exy;  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
###  <a name="system_versioning"></a>系统版本控制  
 下面四个示例将帮助你熟悉使用系统版本控制的语法。 有关其他帮助，请参阅[系统版本控制临时表入门](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)。  
  
**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
#### <a name="a-add-system-versioning-to-existing-tables"></a>A. 将系统版本控制添加到现有表  
 下面的示例演示如何向现有表添加系统版本控制并创建将来的历史记录表。 此示例假定是现有表调用`InsurancePolicy`与定义主键。 此示例将填充新创建的时间段列的开始和结束时间为使用默认值，因为这些值不能为 null 的系统版本控制。 此示例使用 HIDDEN 子句以确保不会影响当前表与之进行交互的现有应用程序。  它还使用可在找到的 HISTORY_RETENTION_PERIOD[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]仅。 
  
```sql  
--Alter non-temporal table to define periods for system versioning  
ALTER TABLE InsurancePolicy  
ADD PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime),   
SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL 
    DEFAULT GETUTCDATE(),   
SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL 
    DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.99999999');  
--Enable system versioning with 1 year retention for historical data
ALTER TABLE InsurancePolicy 
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 1 YEAR));  
```  
  
#### <a name="b-migrate-an-existing-solution-to-use-system-versioning"></a>B. 迁移现有解决方案使用系统版本控制  
 下面的示例演示如何从使用触发器来模拟临时支持解决方案迁移到系统版本控制。 该示例假定没有现有解决方案使用`ProjectTaskCurrent`表和`ProjectTaskHistory`表及其现有的解决方案，用于更改日期和修订日期列其时间，这些期限列，并不使用 datetime2 数据类型并且`ProjectTaskCurrent`表具有主键定义。  
  
```sql  
-- Drop existing trigger  
DROP TRIGGER ProjectTaskCurrent_Trigger;  
-- Adjust the schema for current and history table  
-- Change data types for existing period columns  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
-- Add SYSTEM_TIME period and set system versioning with linking two existing tables  
-- (a certain set of data checks happen in the background)  
ALTER TABLE ProjectTaskCurrent  
ADD PERIOD FOR SYSTEM_TIME ([Changed Date], [Revised Date])  
  
ALTER TABLE ProjectTaskCurrent  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))  
```  
  
#### <a name="c-disabling-and-re-enabling-system-versioning-to-change-table-schema"></a>C. 禁用并重新启用系统版本控制，若要更改表架构  
 此示例演示如何在上禁用系统版本控制`Department`表、 添加一个列，并重新启用系统版本控制。 禁用系统版本控制则需要修改表架构。 执行这些步骤在事务来更新表架构，它使 DBA 要跳过数据一致性检查时重新启用系统版本控制和获得的性能受益时阻止对这两个表进行更新。 请注意，如创建统计信息、 切入分区或将压缩应用于一个或两个表的任务不需要禁用系统版本控制。  
  
```sql  
BEGIN TRAN  
/* Takes schema lock on both tables */  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
/* expand table schema for temporal table */  
ALTER TABLE Department  
     ADD Col5 int NOT NULL DEFAULT 0;  
/* Expand table schema for history table */  
ALTER TABLE DepartmentHistory  
    ADD Col5 int NOT NULL DEFAULT 0;  
/* Re-establish versioning again  */
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE=dbo.DepartmentHistory, 
                                 DATA_CONSISTENCY_CHECK = OFF));  
COMMIT   
```  
  
#### <a name="d-removing-system-versioning"></a>D. 删除系统版本控制  
 此示例演示如何从部门表和 drop 中完全删除系统版本控制`DepartmentHistory`表。 （可选） 你可能也要删除系统用于记录系统版本控制信息的时间段列。 请注意，您不能删除`Department`或`DepartmentHistory`表启用系统版本控制时。  
  
```sql  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
ALTER TABLE Department  
DROP PEROD FOR SYSTEM_TIME;  
DROP TABLE DepartmentHistory;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 通过 C 使用下面的示例 A`FactResellerSales`表中[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]数据库。  
  
### <a name="a-determining-if-a-table-is-partitioned"></a>A. 确定对表进行分区  
 如果表 `FactResellerSales` 已分区，以下查询将返回一个或多个行。 如果表未分区，则不返回任何行。  
  
```sql  
SELECT * FROM sys.partitions AS p  
JOIN sys.tables AS t  
    ON  p.object_id = t.object_id  
WHERE p.partition_id IS NOT NULL  
    AND t.name = 'FactResellerSales';  
```  
  
### <a name="b-determining-boundary-values-for-a-partitioned-table"></a>B. 确定已分区表的边界值  
 以下查询对于 `FactResellerSales` 表中的每个分区返回边界值。  
  
```sql  
SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, 
    p.partition_id, i.data_space_id, f.function_id, f.type_desc, 
    r.boundary_id, r.value AS BoundaryValue   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.partitions AS p  
    ON i.object_id = p.object_id AND i.index_id = p.index_id   
JOIN  sys.partition_schemes AS s   
    ON i.data_space_id = s.data_space_id  
JOIN sys.partition_functions AS f   
    ON s.function_id = f.function_id  
LEFT JOIN sys.partition_range_values AS r   
    ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
WHERE t.name = 'FactResellerSales' AND i.type <= 1  
ORDER BY p.partition_number;  
```  
  
### <a name="c-determining-the-partition-column-for-a-partitioned-table"></a>C. 确定已分区表的分区列  
 以下查询返回表的分区列的名称。 `FactResellerSales`中创建已分区表或索引。  
  
```sql  
SELECT t.object_id AS Object_ID, t.name AS TableName, 
    ic.column_id as PartitioningColumnID, c.name AS PartitioningColumnName   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.columns AS c  
    ON t.object_id = c.object_id  
JOIN sys.partition_schemes AS ps  
    ON ps.data_space_id = i.data_space_id  
JOIN sys.index_columns AS ic  
    ON ic.object_id = i.object_id 
    AND ic.index_id = i.index_id AND ic.partition_ordinal > 0  
WHERE t.name = 'FactResellerSales'  
AND i.type <= 1  
AND c.column_id = ic.column_id;  
```  
  
### <a name="d-merging-two-partitions"></a>D. 合并两个分区  
下面的示例合并两个分区的表。  
  
`Customer`表具有以下定义：  
  
```sql  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100)));  
```  
  
 以下命令将组合的 10 到 25 的分区边界。  
  
```sql  
ALTER TABLE Customer MERGE RANGE (10);  
```  
  
 用于表的新 DDL 是：  
  
```sql  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 25, 50, 100)));  
```  
  
### <a name="e-splitting-a-partition"></a>E. 将分区拆分  
 下面的示例将拆分表上的分区。  
  
 `Customer`表具有以下 DDL:  
  
```sql  
DROP TABLE Customer;  
  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100 )));  
```  
  
 以下命令将创建新的分区值 75，50%到 100 之间的绑定。  
  
```sql  
ALTER TABLE Customer SPLIT RANGE (75);  
```  
  
 用于表的新 DDL 是：  
  
```sql  
CREATE TABLE Customer (  
   id int NOT NULL,  
   lastName varchar(20),  
   orderCount int,  
   orderDate date)  
   WITH DISTRIBUTION = HASH(id),  
   PARTITION ( orderCount (RANGE LEFT  
      FOR VALUES (1, 5, 10, 25, 50, 75, 100 )));  
```  
  
### <a name="f-using-switch-to-move-a-partition-to-a-history-table"></a>F. 使用交换机将分区移到历史记录表  
 下面的示例将数据移动的分区中`Orders`到分区中的表`OrdersHistory`表。  
  
 `Orders`表具有以下 DDL:  
  
```sql  
CREATE TABLE Orders (  
    id INT,  
    city VARCHAR (25),  
    lastUpdateDate DATE,  
    orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ('2004-01-01', '2005-01-01', '2006-01-01', '2007-01-01' )));  
```  
  
 在此示例中，`Orders`表具有以下分区。 每个分区包含数据。  
  
|分区|具有数据？|边界范围|  
|---------------|---------------|--------------------|  
|1|是|订购日期 < 2004年-01-01|  
|2|是|2004年-01-01 < = OrderDate < 2005年-01-01|  
|3|是|2005年-01-01 < = OrderDate < 2006年-01-01|  
|4|是|2006年-01-01 < = OrderDate < ' 2007年-01-01|  
|5|是|'2007-01-01' <= OrderDate|  
  
-   分区 1 （具有数据）： OrderDate < 2004年-01-01  
-   分区 2 （具有数据）: 2004年-01-01 < = OrderDate < 2005年-01-01  
-   分区 3 （具有数据）: 2005年-01-01 < = OrderDate < 2006年-01-01  
-   分区 4 （具有数据）: 2006年-01-01 < = OrderDate < ' 2007年-01-01  
-   分区 5 （具有数据）: 2007年-01-01 < = 订购日期  
  
`OrdersHistory`表具有以下 DDL，它具有相同的列和列名称作为`Orders`表。 两者都在哈希分布式`id`列。  
  
```sql  
CREATE TABLE OrdersHistory (  
   id INT,  
   city VARCHAR (25),  
   lastUpdateDate DATE,  
   orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ( '2004-01-01' )));  
```  
  
 尽管列和列名称必须相同，但不需要的分区边界相同。 在此示例中，`OrdersHistory`表具有以下两个分区，这两个分区都为空：  
  
-   分区 1 （不包含数据）： OrderDate < 2004年-01-01  
-   分区 2 （空）: 2004年-01-01 < = 订购日期  
  
对于以前的两个表，以下命令将所有行都移与`OrderDate < '2004-01-01'`从`Orders`表`OrdersHistory`表。  
  
```sql  
ALTER TABLE Orders SWITCH PARTITION 1 TO OrdersHistory PARTITION 1;  
```  
  
 因此，第一个分区中`Orders`为空且中的第一个分区`OrdersHistory`包含数据。 表现在显示，如下所示：  
  
 `Orders`表  
  
-   分区 1 （空）： OrderDate < 2004年-01-01  
-   分区 2 （具有数据）: 2004年-01-01 < = OrderDate < 2005年-01-01  
-   分区 3 （具有数据）: 2005年-01-01 < = OrderDate < 2006年-01-01  
-   分区 4 （具有数据）: 2006年-01-01 < = OrderDate < ' 2007年-01-01  
-   分区 5 （具有数据）: 2007年-01-01 < = 订购日期  
  
 `OrdersHistory`表  
  
-   分区 1 （具有数据）： OrderDate < 2004年-01-01  
-   分区 2 （空）: 2004年-01-01 < = 订购日期  
  
若要清理`Orders`表，可以删除空的分区合并分区 1 和 2，如下所示：  
  
```sql  
ALTER TABLE Orders MERGE RANGE ('2004-01-01');  
```  
  
 合并后`Orders`表具有下列分区：  
  
 `Orders`表  
  
-   分区 1 （具有数据）： OrderDate < 2005年-01-01  
-   分区 2 （具有数据）: 2005年-01-01 < = OrderDate < 2006年-01-01  
-   分区 3 （具有数据）: 2006年-01-01 < = OrderDate < ' 2007年-01-01  
-   分区 4 （具有数据）: 2007年-01-01 < = 订购日期  
  
假设另一年将传递，你就可以存档 2005 年。 你可以将空分区分配为 2005 年在`OrdersHistory`表中的，将拆分空分区，如下所示：  
  
```sql  
ALTER TABLE OrdersHistory SPLIT RANGE ('2005-01-01');  
```  
  
 拆分、 后`OrdersHistory`表具有下列分区：  
  
 `OrdersHistory`表  
  
-   分区 1 （具有数据）： OrderDate < 2004年-01-01  
-   分区 2 （空）: 2004年-01-01 < 2005年-01-01  
-   分区 3 （空）: 2005年-01-01 < = 订购日期  
  
## <a name="see-also"></a>另请参阅  
 [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [ALTER 分区方案 &#40;Transact SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

