---
title: "table_constraint (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f5265366f28f302e69a178f45baa4464efa1bfd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-tableconstraint-transact-sql"></a>ALTER TABLE table_constraint (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定为主键、 唯一、 外键、 CHECK 约束或添加到表中使用的默认定义的属性[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>参数  
 CONSTRAINT  
 指定 PRIMARY KEY、UNIQUE、FOREIGN KEY 或 CHECK 约束的开始，或者指定 DEFAULT 定义的开始。  
  
 *constraint_name*  
 约束的名称。 约束名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)，只不过该名称不能以数字符号开头 （#）。 如果未提供 constraint_name，则将系统生成的名称分配给约束。  
  
 PRIMARY KEY  
 通过唯一索引对指定的一列或多列强制实体完整性的约束。 对每个表只能创建一个 PRIMARY KEY 约束。  
  
 UNIQUE  
 通过唯一索引为指定的一列或多列提供实体完整性的约束。  
  
 CLUSTERED | NONCLUSTERED  
 指定为 PRIMARY KEY 或 UNIQUE 约束创建聚集或非聚集索引。 PRIMARY KEY 约束默认为 CLUSTERED。 UNIQUE 约束默认为 NONCLUSTERED。  
  
 如果表中已存在聚集约束或聚集索引，则不能指定 CLUSTERED。 如果表中已存在聚集约束或索引，则 PRIMARY KEY 约束默认为 NONCLUSTERED。  
  
 列的**ntext**，**文本**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**，或**映像**数据类型不能指定为索引的列。  
  
 *列*  
 新约束中使用的一个列或一组列，使用括号指定。  
  
 [ **ASC** |DESC]  
 指定加入到表约束中的一列或多列的排序顺序。 默认值为 ASC。  
  
 使用填充因子 **=** *填充因子*  
 指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]在存储索引数据时使用的每个索引页的填充程度。 用户指定*fillfactor*值可以是从 1 到 100 之间。 如果未指定值，则默认值为 0。  
  
> [!IMPORTANT]  
>  生成文档与 FILLFACTOR = *fillfactor*作为适用于 PRIMARY KEY 或 UNIQUE 约束的唯一索引选项保留是为了向后兼容，但将不会记录在这种方式在将来释放。 可以在指定了其他索引选项[index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md)子句的 ALTER TABLE。  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *文件组* |  **"**默认**"** }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定为约束创建的索引的存储位置。 如果*partition_scheme_name*指定，则索引进行分区和分区映射到由指定的文件组*partition_scheme_name*。 如果*文件组*索引创建在指定的文件组中的指定。 如果**"**默认**"**指定或根本未指定 ON，如果在表所在的文件组中创建索引。 当为 PRIMARY KEY 约束或 UNIQUE 约束添加聚集索引时，如果指定了 ON，则创建聚集索引时将把整个表移动到指定的文件组中。  
  
 在此上下文中，默认不是一个关键字;它是默认文件组的标识符和必须分隔，如下所示 ON **"**默认**"**或亮**[**默认**]**。 如果**"**默认**"** QUOTED_IDENTIFIER 选项必须为当前会话中为 ON 的指定。 这是默认设置。  
  
 FOREIGN KEY REFERENCES  
 为列中数据提供引用完整性的约束。 FOREIGN KEY 约束要求列中的每个值在引用的表中对应的被引用列中都存在。  
  
 *referenced_table_name*  
 FOREIGN KEY 约束引用的表。  
  
 *ref_column*  
 新 FOREIGN KEY 约束引用的一个列或一组列（置于括号中）。  
  
 ON DELETE {**任何操作**|级联 |SET NULL |SET DEFAULT}  
 指定哪些操作时将发生改变，如果这些行有引用关系，并且从父表中删除引用的行的表中的行。 默认值为 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]将引发错误，并回滚对父表中行的删除操作。  
  
 CASCADE  
 如果从父表中删除一行，则将从引用表中删除相应行。  
  
 SET NULL  
 如果删除父表中与外键相对应的行，组成外键的所有值都将设置为 NULL。 若要执行此约束，外键列必须可为空值。  
  
 SET DEFAULT  
 如果删除父表中与外键相对应的行，组成外键的所有值都将设置为其默认值。 若要执行此约束，所有外键列都必须有默认定义。 如果某个列可为空值，并且未设置显式的默认值，则将使用 NULL 作为该列的隐式默认值。  
  
 如果该表将包含在使用逻辑记录的合并发布中，则不要指定 CASCADE。 有关逻辑记录的详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果被更改的表已有 INSTEAD OF 触发器 ON DELETE，则不能定义 ON DELETE CASCADE。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库， **ProductVendor**表具有引用关系**供应商**表。 **ProductVendor.VendorID**外键引用**Vendor.VendorID**主键。  
  
 如果在行上执行 DELETE 语句**供应商**表和 ON DELETE CASCADE 操作为指定**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]检查中的一个或多个相关行**ProductVendor**表。 如果存在任何，依赖项的行中**ProductVendor**将删除表中引用的行除了**供应商**表。  
  
 相反，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引发错误，并回滚删除操作上**供应商**行中的至少有一行时**ProductVendor**引用它的表。  
  
 在更新 {**任何操作**|级联 |SET NULL |SET DEFAULT}  
 指定在发生更改的表中，如果行有引用关系且引用的行在父表中被更新，则对这些行采取什么操作。 默认值为 NO ACTION。  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]将引发错误，并回滚对父表中相应行的更新操作。  
  
 CASCADE  
 如果在父表中更新了一行，则将在引用表中更新相应的行。  
  
 SET NULL  
 如果更新了父表中的相应行，则会将构成外键的所有值设置为 NULL。 若要执行此约束，外键列必须可为空值。  
  
 SET DEFAULT  
 如果更新了父表中的相应行，则会将构成外键的所有值都设置为其默认值。 若要执行此约束，所有外键列都必须有默认定义。 如果某个列可为空值，并且未设置显式的默认值，则将使用 NULL 作为该列的隐式默认值。  
  
 如果该表将包含在使用逻辑记录的合并发布中，则不要指定 CASCADE。 有关逻辑记录的详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 如果要更改的表已存在 INSTEAD OF 触发器 ON UPDATE，则不能定义 ON UPDATE CASCADE、SET NULL 或 SET DEFAULT 操作。  
  
 例如，在[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库， **ProductVendor**表具有引用关系**供应商**表。 **ProductVendor.VendorID**外键引用**Vendor.VendorID**主键。  
  
 如果在行上执行 UPDATE 语句**供应商**表和 ON UPDATE CASCADE 操作为指定**ProductVendor.VendorID**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]检查中的一个或多个相关行**ProductVendor**表。 如果存在任何中的相关行**ProductVendor**将更新表中引用的行以及**供应商**表。  
  
 相反，如果指定了 NO ACTION，[!INCLUDE[ssDE](../../includes/ssde-md.md)]引发错误，并回滚更新操作上**供应商**行中的至少有一行时**ProductVendor**引用它的表。  
  
 NOT FOR REPLICATION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 可以为 FOREIGN KEY 约束和 CHECK 约束指定该参数。 如果为约束指定了此子句，则当复制代理执行插入、更新或删除操作时，将不会强制执行此约束。  
  
 DEFAULT  
 指定列的默认值。 DEFAULT 定义可用于为表中现有数据行的新列提供值。 无法将默认定义添加到具有列**时间戳**数据类型、 IDENTITY 属性、 现有的默认值定义或绑定的默认值。 如果列已有默认值，则必须删除旧默认值后才能添加新默认值。 如果为用户定义的类型列指定默认值，类型应支持隐式转换*constant_expression*为用户定义的类型。 为了与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本兼容，可以为 DEFAULT 分配约束名称。  
  
 *constant_expression*  
 用作默认列值的文字值、NULL 或系统函数。 如果*constant_expression*一起用于定义可为列[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]用户定义类型时，该类型的实现必须支持隐式转换*constant_表达式*为用户定义的类型。  
  
 有关*列*  
 指定与表级 DEFAULT 定义相关联的列。  
  
 WITH VALUES  
 指定在默认给定的值*constant_expression*存储在新列添加到现有行。 只有在 ADD 列子句中指定了 DEFAULT 的情况下，才能指定 WITH VALUES。 如果所添加的列允许 Null 值且指定了 WITH VALUES，则默认值将存储在添加到现有行的新列中。 如果没有为允许空值的列指定 WITH VALUES，则 NULL 值将存储在现有行的新列中。 如果新列不允许 Null 值，那么不论是否指定 WITH VALUES，都将在新行中存储默认值。  
  
 CHECK  
 一个约束，该约束通过限制可输入一列或多列中的可能值来强制实现域完整性。  
  
 *logical_expression*  
 用于 CHECK 约束的逻辑表达式，返回 TRUE 或 FALSE。 *logical_expression*使用带有检查约束不能引用另一个表，但可以引用同一行的同一表中的其他列。 该表达式不能引用别名数据类型。  
  
## <a name="remarks"></a>注释  
 当添加 FOREIGN KEY 或 CHECK 约束时，所有现有数据都要进行约束违反验证，除非指定了 WITH NOCHECK 选项。 如果违反了约束，ALTER TABLE 将失败并返回一个错误。 当在现有列上添加新 PRIMARY KEY 或 UNIQUE 约束时，该列中的数据必须唯一。 如果存在重复值，ALTER TABLE 语句将失败。 当添加 PRIMARY KEY 或 UNIQUE 约束时，WITH NOCHECK 选项不起作用。  
  
 每个 PRIMARY KEY 和 UNIQUE 约束都将生成一个索引。 UNIQUE 和 PRIMARY KEY 约束的数目不能导致表上非聚集索引的数目大于 999，也不能导致聚集索引的数目大于 1。 外键约束不会自动生成索引。 然而，经常在查询的联接条件中使用外键列，方法是将一个表的外键约束中的列与另一个表中的主键列或唯一键列匹配。 针对外键列的索引使[!INCLUDE[ssDE](../../includes/ssde-md.md)]可以在外键表中快速查找相关数据。  
  
## <a name="examples"></a>示例  
 有关示例，请参阅[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

