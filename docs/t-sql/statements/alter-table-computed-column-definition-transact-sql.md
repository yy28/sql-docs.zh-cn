---
title: "computed_column_definition (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
ms.assetid: 746eabda-3b4f-4940-b0b5-1c379f5cf7a5
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70972816a0b7259dd7c455e2c65c45491d31e5f0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-computedcolumndefinition-transact-sql"></a>ALTER TABLE computed_column_definition (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定的属性的计算列，通过使用添加到表[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
column_name AS computed_column_expression  
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [ WITH FILLFACTOR = fillfactor ]  
        [ WITH ( <index_option> [, ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ) | filegroup   
            | "default" } ]  
    | [ FOREIGN KEY ]   
        REFERENCES ref_table [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
]  
```  
  
## <a name="arguments"></a>参数  
*column_name*  
 要更改、添加或删除的列的名称。 *column_name*可以是 1 到 128 个字符。 为新的列， *column_name*可以为列创建的省略**时间戳**数据类型。 如果没有*column_name*为指定**时间戳**数据类型列中，名称**时间戳**使用。  
  
*computed_column_expression*  
 定义计算列的值的表达式。 计算列是以非物理方式存储在表中的虚拟列，该列是通过使用同一表中的其他列的表达式计算得出的。 例如，计算的列无法具有定义： 成本按价格 * 数量。表达式可以是非计算列的名称、常量、函数、变量以及通过一个或多个运算符连接的上述元素的任意组合。 表达式不能是子查询，否则包括别名数据类型。  
  
 计算列可用于选择列表、WHERE 子句、ORDER BY 子句或其他任何可以使用正则表达式的位置，但下列情况除外：  
  
-   计算列不能用作 DEFAULT 或 FOREIGN KEY 约束定义，也不能与 NOT NULL 约束定义一起使用。 但是，如果计算列值由具有确定性的表达式定义，并且索引列中允许使用计算结果的数据类型，则可将该列用作索引中的键列，或用作 PRIMARY KEY 或 UNIQUE 约束的一部分。  
  
     例如，如果表中包含整数列 a 和 b，则可以对计算列 a + b 创建索引。但不能对计算列 a+DATEPART(dd, GETDATE()) 创建索引，因为在以后的调用中，其值可能发生更改。  
  
-   计算列不能作为 INSERT 或 UPDATE 语句的目标。  
  
    > [!NOTE]  
    >  由于表中计算列所用列中的各行可能有不同的值，因此计算列的每一行可能有不同的值。  
  
PERSISTED  
 指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在表中物理存储计算值，并在计算列依赖的任何其他列发生更新时对这些计算值进行更新。 将计算列标记为 PERSISTED，便可对具有确定性、但不精确的计算列创建索引。 有关详细信息，请参阅 [计算列上的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。 用作已分区表的分区依据列的所有计算列都必须显式标记为 PERSISTED。 *computed_column_expression*指定持久化时必须具有确定性。  
NULL | NOT NULL  
 指定列中是否允许使用空值。 NULL 并不是严格意义上的约束，但可以使用与指定 NOT NULL 类似的方法指定。 只有同时指定了 PERSISTED 时，才能为计算列指定 NOT NULL。  
  
CONSTRAINT  
 指定 PRIMARY KEY 或 UNIQUE 约束的定义起点。  
  
*constraint_name*  
 新约束。 约束名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)，只不过该名称不能以数字符号开头 （#）。 如果*constraint_name*是未提供，系统生成的名称分配给该约束。  
  
PRIMARY KEY  
 通过唯一索引对指定的一列或多列强制实体完整性的约束。 对每个表只能创建一个 PRIMARY KEY 约束。  
  
UNIQUE  
 是通过唯一索引为特定的一列或多列提供实体完整性的约束。  
  
CLUSTERED | NONCLUSTERED  
 指定为 PRIMARY KEY 或 UNIQUE 约束创建聚集或非聚集索引。 PRIMARY KEY 约束默认为 CLUSTERED。 UNIQUE 约束默认为 NONCLUSTERED。  
  
 如果表中已存在聚集约束或聚集索引，则不能指定 CLUSTERED。 如果表中已存在聚集约束或索引，则 PRIMARY KEY 约束默认为 NONCLUSTERED。  
  
填充因子为*填充因子*  
 指定[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]在存储索引数据时使用的每个索引页的填充程度。 用户指定*fillfactor*值可以是从 1 到 100 之间。 如果未指定值，则默认值为 0。  
  
> [!IMPORTANT]  
>  生成文档与 FILLFACTOR = *fillfactor*作为适用于 PRIMARY KEY 或 UNIQUE 约束的唯一索引选项保留是为了向后兼容，但将不会记录在这种方式在将来释放。 可以在指定了其他索引选项[index_option &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md)子句的 ALTER TABLE。  
  
FOREIGN KEY REFERENCES  
 为列中的数据提供引用完整性的约束。 FOREIGN KEY 约束要求列中的每个值在所引用的表中对应的被引用列中都存在。 FOREIGN KEY 约束只能引用在所引用的表中是 PRIMARY KEY 或 UNIQUE 约束的列，或所引用的表中在 UNIQUE INDEX 内的被引用列。 计算列上的外键也必须标记为 PERSISTED。  
  
*ref_table*  
 FOREIGN KEY 约束所引用的表名。  
  
(*ref_column* )  
 FOREIGN KEY 约束所引用的表中的列。  
  
ON DELETE {**任何操作**|级联}  
 指定当表中的行具有引用关系，而被引用行已从父表中删除时，要对这些行执行的操作。 默认值为 NO ACTION。  
  
NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误，并回滚对父表中行的删除操作。  
CASCADE  
 如果从父表中删除一行，则将从引用表中删除相应行。  
  
 例如，在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中，ProductVendor 表与 Vendor 表有引用关系。 ProductVendor.BusinessEntityID 外键引用 Vendor.BusinessEntityID 主键。  
  
 如果对 Vendor 表的某行执行 DELETE 语句，并且为 ProductVendor.BusinessEntityID 指定 ON DELETE CASCADE 操作，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将检查 ProductVendor 表中的一个或多个依赖行。 如果存在依赖行，则 ProductVendor 表中的依赖行将随 Vendor 表中的被引用行一同删除。  
  
 相反，如果指定了 NO ACTION，则在 ProductVendor 表中至少有一行引用 Vendor 行时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误并回滚对 Vendor 行的删除操作。  
  
 如果该表将包含在使用逻辑记录的合并发布中，则不要指定 CASCADE。 有关逻辑记录的详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
在更新 {**任何操作**}  
 指定如果已创建表中的行具有引用关系，并且被引用行已从父表中更新时，要对该行采取的操作。 反之，如果指定了 NO ACTION，并且 ProductVendor 表中至少有一行引用 Vendor 行，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误，并回滚对 Vendor 行的更新操作。  
  
NOT FOR REPLICATION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 可以为 FOREIGN KEY 约束和 CHECK 约束指定该参数。 如果为约束指定了此子句，则当复制代理执行插入、更新或删除操作时，将不会强制执行此约束。  
  
CHECK  
 一个约束，该约束通过限制可输入一列或多列中的可能值来强制实现域完整性。 计算列上的 CHECK 约束也必须标记为 PERSISTED。  
  
*logical_expression*  
 返回 TRUE 或 FALSE 的逻辑表达式。 该表达式不能包含对别名数据类型的引用。  
  
ON { *partition_scheme_name*(*partition_column_name*) |*文件组*|"默认"}  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定为约束创建的索引的存储位置。 如果*partition_scheme_name*指定，则索引进行分区和分区映射到由指定的文件组*partition_scheme_name*。 如果*文件组*索引创建在指定的文件组中的指定。 如果指定了 "default" 或者根本没有指定 ON，将在创建表的同一个文件组中创建索引。 当为 PRIMARY KEY 约束或 UNIQUE 约束添加聚集索引时，如果指定了 ON，则创建聚集索引时将把整个表移动到指定的文件组中。  
  
> [!NOTE]  
>  在此上下文中，default 不是关键字。 它是默认文件组的标识符，并且必须进行分隔（类似于 ON "default" 或 ON [default]）。 如果指定了 "default"，则当前会话的 QUOTED_IDENTIFIER 选项必须为 ON。 这是默认设置。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 每个 PRIMARY KEY 和 UNIQUE 约束都将生成一个索引。 UNIQUE 和 PRIMARY KEY 约束的数目不能导致表上非聚集索引的数目大于 999，也不能导致聚集索引的数目大于 1。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

