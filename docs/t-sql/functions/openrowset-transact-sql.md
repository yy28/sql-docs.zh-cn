---
title: "OPENROWSET (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
caps.latest.revision: 130
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c23ec85299af595305a5f6d5141dbbf3ffab96d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含访问 OLE DB 数据源中的远程数据所需的所有连接信息。 当访问链接服务器中的表时，这种方法是一种替代方法，并且是一种使用 OLE DB 连接并访问远程数据的一次性的临时方法。 对于较频繁引用 OLE DB 数据源的情况，请改为使用链接服务器。 有关详细信息，请参阅 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)。 `OPENROWSET`可以查询的 FROM 子句中引用函数，就像它是表名称。 `OPENROWSET`函数也可以引用的目标表作为`INSERT`， `UPDATE`，或`DELETE`语句，受制于 OLE DB 访问接口的功能。 虽然查询可能返回多个结果集，`OPENROWSET`返回只有第一个。  
  
 `OPENROWSET`此外支持通过内置的大容量提供程序，从文件读取，并将它们作为一个行集返回的数据大容量操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>参数  
 *provider_name*  
 字符串，表示在注册表中指定的 OLE DB 访问接口的友好名称（或 PROGID）。 *provider_name*没有默认值。  
  
 *数据源*  
 对应于特定 OLE DB 数据源的字符串常量。 *数据源*是 DBPROP_INIT_DATASOURCE 属性传递给要初始化的提供程序的提供程序的 IDBProperties 接口。 通常，此字符串包含数据库文件的名称、数据库服务器的名称，或者访问接口能理解的用于定位数据库的名称。  
  
 *user_id*  
 字符串常量，它是传递给指定 OLE DB 访问接口的用户名。 *user_id*指定连接的安全上下文，并作为要初始化的提供程序的 DBPROP_AUTH_USERID 属性传递。 *user_id*不能为 Microsoft Windows 登录名。  
  
 *密码*  
 字符串常量，它是传递给 OLE DB 访问接口的用户密码。 *密码*作为 DBPROP_AUTH_PASSWORD 属性时传入初始化提供程序。 *密码*不能为 Microsoft Windows 密码。  
  
 *provider_string*  
 访问接口特定的连接字符串，作为 DBPROP_INIT_PROVIDERSTRING 属性传入以初始化 OLE DB 访问接口。 *provider_string*通常封装初始化的提供程序所需的所有连接信息。 有关可被识别的关键字的列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序，请参阅[初始化和授权属性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
 *目录*  
 指定对象所在的目录或数据库的名称。  
  
 *架构*  
 架构的名称或指定对象的对象所有者名称。  
  
 *对象*  
 对象名，它唯一地标识出将要操作的对象。  
  
 *查询*  
 字符串常量，发送到访问接口并由访问接口执行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例不处理该查询，但处理由访问接口返回的查询结果（传递查询）。 有些访问接口并不通过表名而是通过命令语言提供其表格格式数据，将传递查询用于这些访问接口是非常有用的。 只要查询提供程序支持的 OLE DB 命令对象和其强制接口在远程服务器上，支持传递查询。 有关详细信息，请参阅[SQL Server Native Client &#40; OLE DB &#41;引用](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)。  
  
 BULK  
 使用 OPENROWSET 的 BULK 行集访问接口读取文件中的数据。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，OPENROWSET 无需将数据文件中的数据加载到目标表，便可读取这些数据。 这样便可在单个 SELECT 语句中使用 OPENROWSET。  
  
 BULK 选项的参数可对何时开始和结束数据读取、如何处理错误以及如何解释数据提供有效控制。 例如，你可以指定数据文件作为类型的单行、 单列行集读取**varbinary**， **varchar**，或**nvarchar**。 默认行为详见随后的参数说明。  
  
 有关如何使用 BULK 选项的信息，请参阅本主题后面部分的“备注”。 有关 BULK 选项所需权限的信息，请参阅本主题后面的“权限”。  
  
> [!NOTE]  
>  当用于以完整恢复模式导入数据时，OPENROWSET (BULK ...) 不优化日志记录。  
  
 有关准备用于大容量导入的数据的信息，请参阅[准备用于大容量导出或导入 &#40; 的数据SQL server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 *data_file*  
 数据文件的完整路径，该文件的数据将被复制到目标表中。   
 **适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
开头[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1 data_file 可以位于 Azure blog 存储。 有关示例，请参阅[示例的大容量访问 Azure Blob 存储中的数据](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。
  
 \<bulk_options >  
 指定 BULK 选项的一个或多个参数。  
  
 代码页 = {ACP |OEM |原始 |*code_page*}  
 指定该数据文件中数据的代码页。 代码页是仅当数据包含相关**char**， **varchar**，或**文本**具有多个 127 或小于 32 的字符值的列。  
  
> [!NOTE]  
>  我们建议你希望 65001 选项会优先于排序规则/代码页规范时，除指定在格式文件中，每个列的排序规则名称。  
  
|CODEPAGE 值|Description|  
|--------------------|-----------------|  
|ACP|将转换的列**char**， **varchar**，或**文本**从 ansi 标准转换的数据类型 /[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 代码页 (ISO 1252) 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代码页。|  
|OEM（默认值）|将转换的列**char**， **varchar**，或**文本**到的系统 OEM 代码页中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代码页。|  
|RAW|不执行从一个代码页到另一个代码页的转换。 这是执行最快的选项。|  
|*code_page*|指示数据文件中字符数据已编码的源代码页，例如 850。<br /><br /> **\*\*重要\* \*** 之前的版本[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]不支持代码页 65001 （utf-8 编码）。|  
  
 ERRORFILE =*file_name*  
 指定用于收集格式有误且不能转换为 OLE DB 行集的行的文件。 这些行将按原样从数据文件复制到此错误文件中。  
  
 错误文件在开始执行命令时创建。 如果该文件已存在，将引发一个错误。 此外，还创建了一个扩展名为 .ERROR.txt 的控制文件。 此文件引用的错误文件中的每一行，并提供错误的诊断。 纠正错误后即可加载数据。  
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。
开头[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]、`error_file_path`可以位于 Azure blog 存储。 

errorfile_data_source_name   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。
已命名的外部数据源将指向执行的将包含导入过程中发现错误的错误文件的 Azure Blob 存储位置。 必须使用创建外部数据源`TYPE = BLOB_STORAGE`选项中添加[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1。 有关详细信息，请参阅[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)。
  
 FIRSTROW =*first_row*  
 指定要加载的第一行的行号。 默认值为 1。 这表示指定数据文件中的第一行。 通过对行终止符进行计数来确定行号。 FIRSTROW 从 1 开始。  
  
 LASTROW =*last_row*  
 指定要加载的最后一行的行号。 默认值为 0。 这表示指定数据文件中的最后一行。  
  
 MAXERRORS =*maximum_errors*  
 指定格式化文件中定义的、在 OPENROWSET 引发异常之前可以发生的语法错误或格式有误行的最大数目。 在达到 MAXERRORS 之前，OPENROWSET 会忽略每个错误行，不加载它，并将其计为一个错误。  
  
 默认值为*maximum_errors*为 10。  
  
> [!NOTE]  
>  MAX_ERRORS 不适用于到 CHECK 约束或转换**money**和**bigint**数据类型。  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 指定数据文件中近似的数据行数量。 该值应与实际行数相同。  
  
 OPENROWSET 始终以单批形式导入数据文件。 但是，如果你指定*rows_per_batch*与值 > 0，查询处理器使用的值*rows_per_batch*作为一个提示，用于分配查询计划中的资源。  
  
 默认情况下，ROWS_PER_BATCH 是未知的。 指定 ROWS_PER_BATCH = 0 相当于忽略 ROWS_PER_BATCH。  
  
 顺序 ({*列*[ASC |DESC]} [，... *n*  ] [UNIQUE])  
 一个用于指定数据文件中数据的排序方式的可选提示。 默认情况下，大容量操作假定数据文件未排序。 如果查询优化器能够利用指定顺序来生成更有效的查询计划，则性能可能会得到改善。 指定一个排序可以取得益处的示例包括：  
  
-   将行插入到具有聚集索引的表，其中行集数据按聚集索引键进行排序。  
  
-   将行集与另一个表联接，其中排序列和联接列匹配。  
  
-   通过排序列聚合行集数据。  
  
-   将行集用作查询的 FROM 子句中的源表，其中排序列和联接列匹配。  
  
 UNIQUE 指定数据文件不能有重复条目。  
  
 如果数据文件中的实际行没有根据指定的顺序进行排序，或者如果指定了 UNIQUE 提示并且存在重复键，则返回错误。  
  
 使用 ORDER 时列别名是必需的。 列别名列表必须引用由 BULK 子句正在访问的派生表。 在 ORDER 子句中指定的列名将引用此列别名列表。 较大的值类型 (**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，和**xml**) 和大型对象 (LOB) 类型 (**文本**， **ntext**，和**映像**) 列不能指定。  
  
 SINGLE_BLOB  
 返回的内容*data_file*作为类型的单行、 单列行集**varbinary （max)**。  
  
> [!IMPORTANT]  
>  我们建议您仅使用 SINGLE_BLOB 选项（而不是 SINGLE_CLOB 和 SINGLE_NCLOB）导入 XML 数据，因为只有 SINGLE_BLOB 支持所有的 Windows 编码转换。  
  
 SINGLE_CLOB  
 通过阅读*data_file*为 ASCII，将内容作为返回类型的单行、 单列行集**varchar （max)**，使用当前数据库的排序规则。  
  
 SINGLE_NCLOB  
 通过阅读*data_file*为 unicode 编码，将内容作为返回类型的单行、 单列行集**nvarchar (max)**，使用当前数据库的排序规则。  

### <a name="input-file-format-options"></a>输入的文件格式选项
  
格式 **=**  CSV   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
指定以逗号分隔的值文件符合[RFC 4180](https://tools.ietf.org/html/rfc4180)标准。

 FORMATFILE =*format_file_path*  
 指定格式化文件的完整路径。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持两种格式化文件类型：XML 和非 XML。  
  
 格式化文件对定义结果集中的列类型是必需的。 唯一的例外情况是指定 SINGLE_CLOB、SINGLE_BLOB 或 SINGLE_NCLOB 时；在这种情况下，不需要格式化文件。  
  
 有关格式化文件的信息，请参阅[使用格式化文件批量导入数据 &#40;SQL server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
开头[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1 format_file_path 可以位于 Azure blog 存储。 有关示例，请参阅[示例的大容量访问 Azure Blob 存储中的数据](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。

FIELDQUOTE  **=**  field_quote   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
指定将用作为 CSV 文件中的引号字符的字符。 如果未指定，引号字符 （"） 中定义将用作引号字符[RFC 4180](https://tools.ietf.org/html/rfc4180)标准。

  
## <a name="remarks"></a>注释  
 `OPENROWSET`可以用于访问远程数据从 OLE DB 数据源时，才**DisallowAdhocAccess**注册表选项显式设置为 0 指定提供程序，并且高级配置选项即席分布式查询启用。 如果未设置这些选项，则默认行为不允许即席访问。  
  
 访问远程 OLE DB 数据源时，服务器不会自动委托可信连接的登录标识，客户端通过此登录标识才能连接到正在查询的服务器。 必须配置身份验证委托。  
  
 如果 OLE DB 访问接口在指定的数据源中支持多个目录和架构，那么就需要目录及架构名称。 值为*目录*和*架构*当 OLE DB 访问接口不支持它们，则可以省略。 如果提供程序支持仅架构名称，该窗体的两部分名称*架构***。***对象*必须指定。 如果提供程序支持仅目录名称，格式的由三部分名称*目录***。***架构***。***对象*必须指定。 必须指定由三部分名称，针对传递查询使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 有关详细信息，请参阅[TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`不接受其自变量的变量。  
  
 任何调用到`OPENDATASOURCE`， `OPENQUERY`，或`OPENROWSET`中`FROM`子句从进行求值单独且独立地对用作目标的更新，这些函数的任何调用即使相同自变量提供给两个调用。 具体而言，应用到上述任一调用的结果的筛选器或联接条件不会影响其他调用的结果。  
  
## <a name="using-openrowset-with-the-bulk-option"></a>使用带有 BULK 选项的 OPENROWSET  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 增强功能支持 OPENROWSET(BULK...) 函数：  
  
-   FROM 子句，用于为`SELECT`可以调用`OPENROWSET(BULK...)`而不是表名称，与完整`SELECT`功能。  
  
     `OPENROWSET`与`BULK`选项在需要相关名称，也称为一个范围变量或别名，`FROM`子句。 可以指定列别名。 如果未指定列别名列表，则格式化文件必须具有列名。 指定列别名会覆盖格式化文件中的列名，例如：  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    未能添加`AS <table_alias>`将导致错误：    
>    消息 491，级别 16，状态 1，第 20 行    
>    必须在 FROM 子句中为大容量行集指定相关名称。    
  
-   A`SELECT...FROM OPENROWSET(BULK...)`语句查询文件中的数据直接，而无需将数据导入到表。 `SELECT…FROM OPENROWSET(BULK...)`语句还可以通过使用格式化文件指定列名称，以及数据类型列出的大容量列别名。  
  
-   使用`OPENROWSET(BULK...)`作为中的源表`INSERT`或`MERGE`语句大容量导入数据从数据文件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 有关详细信息，请参阅[导入批量数据使用 BULK INSERT 或 OPENROWSET &#40;BULK...&#41;&#40;SQL server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   当`OPENROWSET BULK`选项与使用`INSERT`语句，BULK 子句支持表提示。 除了常规表提示，如`TABLOCK`、`BULK`子句可以接受下列专用的表提示： `IGNORE_CONSTRAINTS` (仅忽略`CHECK`和`FOREIGN KEY`约束)， `IGNORE_TRIGGERS`， `KEEPDEFAULTS`，和`KEEPIDENTITY`。 有关详细信息，请参阅[表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 有关如何使用信息`INSERT...SELECT * FROM OPENROWSET(BULK...)`语句，请参阅[大容量导入和导出数据 &#40;SQL server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). 有关何时在事务日志中记录由批量导入执行的行插入操作的信息，请参阅[《Prerequisites for Minimal Logging in Bulk Import》](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)（批量导入的最小日志记录的先决条件）。  
  
> [!NOTE]  
>  当你使用`OPENROWSET`，务必了解如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]处理模拟。 有关安全注意事项的信息，请参阅[导入批量数据使用 BULK INSERT 或 OPENROWSET &#40;BULK...&#41;&#40;SQL server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>大容量导入 SQLCHAR、SQLNCHAR 或 SQLBINARY 数据  
 OPENROWSET(BULK...) 假定（如果未指定）SQLCHAR、SQLNCHAR 或 SQLBINARY 数据的最大长度不会超过 8000 个字节。 如果要导入数据处于 LOB 数据字段包含任何**varchar （max)**， **nvarchar (max)**，或**varbinary （max)**超过 8000 个字节的对象，则必须使用XML 格式文件中定义数据字段的最大长度。 若要指定最大长度，请编辑格式文件并声明 MAX_LENGTH 属性。  
  
> [!NOTE]  
>  自动生成的格式文件不会为 LOB 字段指定长度或最大长度。 不过，您可以手动编辑格式文件并指定长度或最大长度。  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>批量导出或导入 SQLXML 文档  
 若要批量导出或导入 SQLXML 数据，请在格式化文件中使用下列数据类型之一。  
  
|数据类型|效果|  
|---------------|------------|  
|SQLCHAR 或 SQLVARYCHAR|在客户端代码页或排序规则隐含的代码页中发送数据。|  
|SQLNCHAR 或 SQLNVARCHAR|以 Unicode 格式发送数据。|  
|SQLBINARY 或 SQLVARYBIN|不经任何转换即发送数据。|  
  
## <a name="permissions"></a>Permissions  
 `OPENROWSET`权限决定被传递给 OLE DB 提供程序的用户名称的权限。 若要使用`BULK`选项需要`ADMINISTER BULK OPERATIONS`权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. 将 OPENROWSET 与 SELECT 和 SQL Server Native Client OLE DB 访问接口一起使用  
 下面的示例使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序访问`HumanResources.Department`表中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]远程服务器上的数据库`Seattle1`。 （使用 SQLNCLI 并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将重定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口的最新版本。）使用 `SELECT` 语句定义返回的行集。 访问接口字符串包含 `Server` 和 `Trusted_Connection` 关键字。 这些关键字所识别的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
```tsql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. 使用 Microsoft OLE DB Provider for Jet  
 以下示例通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access `Customers` 数据库中的 `Northwind` 表。  
  
> [!NOTE]  
>  此示例假定已经安装了 Access。 若要运行该示例，则必须安装 Northwind 数据库。  
  
```tsql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. 使用 OPENROWSET 和 INNER JOIN 中的另一个表  
 下面的示例选择中的所有数据`Customers`表的本地实例从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`Northwind`数据库和从`Orders`从访问表`Northwind`存储在同一台计算机上的数据库。  
  
> [!NOTE]  
>  此示例假定已经安装了 Access。 若要运行该示例，则必须安装 Northwind 数据库。  
  
```tsql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. 使用 OPENROWSET 将文件数据大容量插入 varbinary(max) 列中  
 以下示例创建一个用于演示的小型表，并将名为 `Text1.txt` 的文件（位于 `C:` 根目录）中的文件数据插入 `varbinary(max)` 列中。  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. 将 OPENROWSET BULK 访问接口用于格式化文件以检索文本文件中的行  
 以下示例使用格式化文件检索用制表符分隔的文本文件 `values.txt` 中的行，该文件包含下列数据：  
  
```tsql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 格式化文件 `values.fmt` 说明 `values.txt` 中的列：  
  
```tsql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 下面的语句是检索此数据的查询：  
  
```tsql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. 指定格式文件和代码页  
 下面的示例演示如何使用在同一时间的格式文件和代码页选项。  
  
```tsql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. 从 CSV 文件格式文件访问数据  
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
```tsql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. 从 CSV 文件没有格式文件访问数据

```tsql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. 从文件存储在 Azure Blob 存储中访问数据   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
下面的示例使用外部数据源指向中将 Azure 存储帐户和数据库范围的凭据为共享的访问签名创建的容器。     

```tsql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
对于完成`OPENROWSET`示例包括配置的凭据和外部数据源，请参阅[示例的大容量访问 Azure Blob 存储中的数据](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。
 
### <a name="additional-examples"></a>其他示例  
 有关显示使用的其他示例`INSERT...SELECT * FROM OPENROWSET(BULK...)`，请参阅以下主题：  
  
-   [批量导入和导出 XML 文档的示例 (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式化文件跳过数据字段 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [批量导入和导出数据 (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40;Transact SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [行集函数 &#40;Transact SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

