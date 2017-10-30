---
title: "column_definition (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_definition
- column_definition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column_definition
- ALTER TABLE statement
- column properties [SQL Server]
- column definitions [SQL Server]
ms.assetid: a1742649-ca29-4d9b-9975-661cdbf18f78
caps.latest.revision: 78
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c63dcea3473198ded46ebf84053fa9d8b36330f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-columndefinition-transact-sql"></a>ALTER TABLE column_definition (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定通过使用添加到表的列的属性[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
column_name <data_type>  
[ FILESTREAM ]  
[ COLLATE collation_name ]   
[ NULL | NOT NULL ]  
[   
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression [ WITH VALUES ]   
    | IDENTITY [ ( seed , increment ) ] [ NOT FOR REPLICATION ]   
]  
[ ROWGUIDCOL ]   
[ SPARSE ]   
[ ENCRYPTED WITH  
  ( COLUMN_ENCRYPTION_KEY = key_name ,  
      ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
      ALGORITHM =  'AEAD_AES_256_CBC_HMAC_SHA_256'   
  ) ]  
[ MASKED WITH ( FUNCTION = ' mask_function ') ]  
[ <column_constraint> [ ...n ] ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}  
```  
  
## <a name="arguments"></a>参数  
 *column_name*  
 要更改、添加或删除的列的名称。 *column_name*可以包含 1 至 128 个字符。 为新的列，使用时间戳数据类型，创建*column_name*可以省略。 如果没有*column_name*为指定**时间戳**数据类型列中，名称**时间戳**使用。  
  
 [ *type_schema_name***。** ]*类型 _ 名称*  
 是添加的列的数据类型及其所属架构。  
  
 *类型 _ 名称*可以是：  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统数据类型。  
  
-   基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型的别名数据类型。 别名数据类型必须先使用 CREATE TYPE 进行创建，然后才能在表定义中使用。  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]用户定义的类型和它所属的架构。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 用户定义类型必须先使用 CREATE TYPE 进行创建，然后才能在表定义中使用。  
  
 如果*type_schema_name*未指定， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]引用*type_name*按以下顺序：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统数据类型。  
  
-   当前数据库中当前用户的默认架构。  
  
-   当前数据库中的 **dbo** 架构。  
  
*精度*  
 指定的数据类型的精度。 有关有效的精度值的详细信息，请参阅[精度、 小数位数和长度 &#40;Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*小数位数*  
 是指定数据类型的小数位数。 有关有效的缩放值的详细信息，请参阅[精度、 小数位数和长度 &#40;Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**最大值**  
 仅适用于**varchar**， **nvarchar**，和**varbinary**数据类型。 它们用于存储 2^31 个字节的字符和二进制数据，以及 2^30 个字节的 Unicode 数据。  
  
**内容**  
 指定的每个实例**xml**中数据类型*column_name*可包含多个顶级元素。 内容仅适用于**xml**数据类型，并且仅当指定*xml_schema_collection*还指定。 如果未指定，则默认行为是 CONTENT。  
  
DOCUMENT  
 指定的每个实例**xml**中数据类型*column_name*可包含仅有一个顶级元素。 文档仅适用于**xml**数据类型，并且仅当指定*xml_schema_collection*还指定。  
  
 *xml_schema_collection*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于**xml**将 XML 架构集合与类型相关联的数据类型。 键入字词之前**xml**列添加到架构，必须首先会创建的架构在数据库中使用[CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)。  
  
FILESTREAM  
 （可选） 指定列具有 FILESTREAM 存储属性*type_name*的**varbinary （max)**。  
  
 当某一列指定 FILESTREAM 时，表还必须有一列**uniqueidentifier**具有 ROWGUIDCOL 属性的数据类型。 此列不得为空值且必须具有 UNIQUE 或 PRIMARY KEY 单列约束。 该列的 GUID 值必须在插入数据时由应用程序提供，或由使用 NEWID () 函数的 DEFAULT 约束提供。  
  
 如果为表定义了 FILESTREAM 列，则不能删除 ROWGUIDCOL 列并且不能更改相关的约束。 仅当删除了最后一个 FILESTREAM 列后，才能删除 ROWGUIDCOL 列。  
  
 当为某个列指定了 FILESTREAM 存储属性时，该列的所有值都将存储在文件系统上的 FILESTREAM 数据容器中。  
  
 有关演示如何使用列定义的示例，请参阅[FILESTREAM &#40;SQL server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *collation_name*  
 指定列的排序规则。 如果未指定，则为该列分配数据库的默认排序规则。 排序规则名称可以是 Windows 排序规则名称或 SQL 排序规则名称。 列表和详细信息，请参阅[Windows 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 排序规则名称 &#40;Transact SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 COLLATE 子句可以用于指定仅的列的排序规则**char**， **varchar**， **nchar**，和**nvarchar**数据类型.  
  
 有关 COLLATE 子句的详细信息，请参阅[COLLATE &#40;Transact SQL &#41;](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 确定列中是否允许空值。 严格来讲，NULL 不是约束，但可以像指定 NOT NULL 那样指定它。  
  
[约束*constraint_name* ]  
 指定 DEFAULT 值定义的开头。 为了与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本兼容，可以为 DEFAULT 分配约束名称。 *constraint_name*必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)，只不过该名称不能以数字符号开头 （#）。 如果*constraint_name*未指定，则系统生成的名称分配给默认定义。  
  
DEFAULT  
 指定列的默认值的关键字。 DEFAULT 定义可用于为表中现有数据行的新列提供值。 默认值定义不能应用于**时间戳**列或具有 IDENTITY 属性的列。 如果为用户定义的类型列指定默认值，类型必须支持隐式转换*constant_expression*为用户定义的类型。  
  
*constant_expression*  
 用作默认列值的文字值、NULL 或者系统函数。 如果与定义的列结合使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]用户定义类型时，该类型的实现必须支持隐式转换*constant_expression*为用户定义的类型。  
  
WITH VALUES  
 指定在默认给定的值*constant_expression*存储在新列添加到现有行。 如果添加的列允许空值并指定了 WITH VALUES，则在添加到现有行的新列中存储默认值。 如果没有为允许空值的列指定 WITH VALUES，则在现有行的新列中存储 NULL 值。 如果新列不允许 Null 值，那么不论是否指定 WITH VALUES，都将在新行中存储默认值。  
  
IDENTITY  
 指定新列为标识列。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]为该列提供唯一的增量值。 当您向现有表中添加标识符列时，还会将标识号添加到具有种子值和增量值的现有表行中。 无法保证行的更新顺序。 也会为添加的任何新行生成标识号。  
  
 标识列通常与 PRIMARY KEY 约束一起用于用作表的唯一行标识符。 标识属性可以分配给**tinyint**， **smallint**， **int**， **bigint**， **decimal(p,0)**，或**numeric(p,0)**列。 每个表只能创建一个标识列。 DEFAULT 关键字和绑定默认值不能用于标识列。 要么同时指定种子和增量，要么都不指定。 如果都不指定，默认值为 (1，1)。  
  
> [!NOTE]  
>  不能修改现有的表列以添加 IDENTITY 属性。  
  
 不支持向已发布的表添加标识列，因为将列复制到订阅服务器时，这会导致无法收敛。 发布服务器的标识列中的值取决于受影响的表中行的物理存储顺序。 行在订阅服务器中的存储顺序可能会有所不同；因此对于相同的行，标识列的值可能会不同。  
  
 若要禁用通过允许要显式插入值的列的标识属性，使用[SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md)。  
  
*种子*  
 用于表中所加载的第一行的值。  
  
*增量*  
 增加到上一个加载行的标识值的增量值。  
  
NOT FOR REPLICATION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 可以为 IDENTITY 属性指定该子句。 如果为 IDENTITY 属性指定了该子句，则当复制代理执行插入操作时，标识列中的值不会增加。  
  
ROWGUIDCOL  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定该列是一个行全局唯一标识符列。 ROWGUIDCOL 只能分配给**uniqueidentifier**列中，并且只有一个**uniqueidentifier**可以将每个表的列指定为 ROWGUIDCOL 列。 不能为用户定义数据类型分配 ROWGUIDCOL。  
  
 ROWGUIDCOL 并不强制列中所存储值的唯一性。 另外，该属性也不会为插入到表中的新行自动生成值。 若要为每列生成唯一值，则可以在 INSERT 语句中使用 NEWID 函数，也可以将 NEWID 函数指定为列的默认值。 有关详细信息，请参阅[NEWID &#40;Transact SQL &#41;](../../t-sql/functions/newid-transact-sql.md)和[INSERT &#40;Transact SQL &#41;](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 指示列为稀疏列。 稀疏列已针对 NULL 值进行了存储优化。 不能将稀疏列指定为 NOT NULL。 其他限制和稀疏列的详细信息，请参阅[使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。  
  
\<column_constraint >  
 列约束自变量的定义，请参阅[column_constraint &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 使用加密  
 通过使用指定加密列[始终加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 指定的列加密密钥。 有关详细信息，请参阅[CREATE COLUMN ENCRYPTION KEY &#40;Transact SQL &#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = {确定性 |随机}  
 **确定性加密** 使用一种对任何给定的纯文本值始终生成相同的加密值的方法。 使用确定性加密允许搜索使用等同性比较，分组和联接表使用等值联结根据加密值，但也可以允许未经授权的用户通过检查中的模式来猜测有关加密值的信息加密的列。 确定性加密列联接两个表是才有可能，如果两个列使用相同的列加密密钥进行加密。 确定性加密必须使用具有字符列的 binary2 排序顺序的列排序规则。  
  
 **随机加密** 使用一种以更不可预测地方式加密数据的方法。 随机的加密更加安全，但不等式搜索、 分组和联接对加密列。 使用随机的加密的列无法编制索引。  
  
 将搜索参数或分组参数，例如政府身份证号的列使用确定性加密。 使用随机的加密，例如信用卡号的数据，这与其他记录分组在一起，也没有用来联接表和这会为不搜索，因为你使用其他列 （如大量事务） 来查找其中包含已加密的行感兴趣的列。  
  
 列必须是符合条件的数据类型。  
  
算法  
**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
必须是**AEAD_AES_256_CBC_HMAC_SHA_256**。  
  
 包括功能约束的详细信息，请参阅[始终加密 &#40; 数据库引擎 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。  
  
   
添加掩码与 (函数 = *mask_function* )  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定动态数据掩码。 *mask_function*是使用适当的参数的屏蔽函数的名称。 以下函数均可用：  
  
-   default （)  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 函数参数，请参阅[动态数据屏蔽](../../relational-databases/security/dynamic-data-masking.md)。  
  
## <a name="remarks"></a>注释  
 如果将列添加具有**uniqueidentifier**数据类型，它可以定义默认值使用 newid （） 函数提供每个表中的现有行的新列中的唯一标识符值。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不强制在列定义中指定 DEFAULT、IDENTITY、ROWGUIDCOL 或列约束的顺序。  
  
 如果添加列导致数据行大小超过 8060 字节，ALTER TABLE 语句将失败。  
  
## <a name="examples"></a>示例  
 有关示例，请参阅[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  

