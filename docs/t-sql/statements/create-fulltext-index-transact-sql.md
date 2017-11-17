---
title: "CREATE FULLTEXT INDEX (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/05/2017
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
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
caps.latest.revision: 110
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92749ed0518de83be07c6a80f9e3306741507166
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内数据库中的表或索引视图创建全文索引。 每个表或索引视图只允许有一个全文索引，并且每个全文索引会应用于单个表或索引视图。 全文索引最多可以包含 1024 个列。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
## <a name="arguments"></a>参数  
 *table_name*  
 包含全文索引中的一列或多列的表或索引视图的名称。  
  
 *column_name*  
 全文索引中包含的列的名称。 只能为的类型列**char**， **varchar**， **nchar**， **nvarchar**，**文本**， **ntext**，**映像**， **xml**，和**varbinary （max)**编制索引，供全文搜索。 若要指定多个列，请重复*column_name*子句，如下所示：  
  
 CREATE FULLTEXT INDEX ON *table_name* (*column_name1* […] *column_name2* […])...  
  
 类型列*type_column_name*  
 指定一个表列的名称*type_column_name*，也就是说，用来保存的文档类型**varbinary （max)**或**映像**文档。 此列（称为类型列）包含用户提供的文件扩展名（.doc、.pdf、.xls 等）。 类型列必须是 **char**、 **nchar**、 **varchar**或 **nvarchar**类型。  
  
 指定类型列*type_column_name*才*column_name*指定**varbinary （max)**或**映像**列中，数据处于存储为二进制数据;否则为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回错误。  
  
> [!NOTE]  
>  在创建索引时，全文引擎使用缩写类型列中的每个表行来标识要用于中的文档的全文搜索筛选器*column_name*。 筛选器按二进制流加载文档，并删除格式设置信息，然后将文档中的文本发送到断字器组件。 有关详细信息，请参阅 [配置和管理搜索筛选器](../../relational-databases/search/configure-and-manage-filters-for-search.md)。  
  
 语言*language_term*  
 是中存储的数据的语言*column_name*。  
  
 *language_term*是可选的可以指定为字符串、 整数或与区域设置标识符 (LCID) 的一种语言对应的十六进制值。 如果未指定任何值，则使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的默认语言。  
  
 如果*language_term*指定，它表示的语言将用于索引数据存储在**char**， **nchar**， **varchar**， **nvarchar**，**文本**，和**ntext**列。 这种语言是如果在查询时使用的默认语言*language_term*未指定针对列的全文谓词的一部分。  
  
 当指定为一个字符串， *language_term*对应于 syslanguages 系统表中的别名列值。 字符串必须括在单引号中，以作为在*language_term*。 如果为一个整数，指定*language_term*是实际标识的语言的 LCID。 当指定为十六进制值， *language_term* 0x 后跟 LCID 的十六进制值。 十六进制值不能超过八位（包括前导零在内）。  
  
 如果该值是双字节字符集 (DBCS) 格式，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将其转换为 Unicode 格式。  
  
 为指定的语言，必须启用资源，如断字符和词干分析器， *language_term*。 如果这些资源不支持指定的语言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。  
  
 使用 sp_configure 存储过程可访问有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的默认全文语言的信息。 有关详细信息，请参阅本主题后面的 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)不熟悉的读者。  
  
 如果非 BLOB 和非 XML 列包含多种语言的文本数据，或者列中存储的文本的语言未知，则可能适合使用非特定 (0x0) 语言资源。 但是，您应该先了解使用非特定 (0x0) 语言资源的可能后果。 有关的可能的解决方案和后果的使用非特定区域性的 (0x0) 语言资源的信息，请参阅[语言创建时选择的全文索引](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
 对于存储在 XML 或 BLOB 类型列中的文档，在创建索引时，将使用文档内的语言编码。 例如，在 XML 列**xml: lang** XML 文档中的属性将标识语言。 在查询时，以前中指定的值*language_term*将成为用于全文查询，除非的默认语言*language_term*指定为全文查询的一部分。  
  
 STATISTICAL_SEMANTICS  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 创建作为统计语义索引一部分的附加关键短语和文档相似性索引。 有关详细信息，请参阅[语义搜索 (SQL Server)](../../relational-databases/search/semantic-search-sql-server.md)。  
  
 密钥索引*index_name*  
 是唯一的键索引的名称上*table_name*。 KEY INDEX 必须是唯一的单键列，不可为 Null。 为全文唯一键选择最小的唯一键索引。  为获得最佳性能，建议全文键使用整数数据类型。  
  
 *fulltext_catalog_name*  
 用于全文索引的全文目录。 数据库中必须已存在该目录。 此子句为可选项。 如果未指定，则使用默认目录。 如果默认目录不存在，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。  
  
 文件组*filegroup_name*  
 针对指定的文件组创建指定的全文索引。 该文件组必须已存在。 如果未指定 FILEGROUP 子句，则全文索引位于与基表或视图相同的文件组中（对于非分区表），或者位于主文件组中（对于分区表）。  
  
 CHANGE_TRACKING [=] {手动 |**自动**|关闭 [，不进行填充]}  
 指定是否由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对全文索引所覆盖的表列所做的更改（更新、删除或插入）传播到全文索引。 通过 WRITETEXT 和 UPDATETEXT 所做的数据更改不会反映到全文索引中，也不能使用更改跟踪方法拾取。  
  
 MANUAL  
 指定必须通过调用 ALTER FULLTEXT INDEX … START UPDATE POPULATION[!INCLUDE[tsql](../../includes/tsql-md.md)]语句 (*手动填充*)。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来定期调用此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
 **自动**  
 指定，在基表中修改数据时自动传播跟踪的更改 (*自动填充*)。 尽管是自动传播更改，但这些更改可能不会立即反映到全文索引中。 默认值为 AUTO。  
  
 OFF [ `,` NO POPULATION]  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保留对索引数据的更改的列表。 如果未指定 NO POPULATION，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建索引后将对其进行完全填充。  
  
 仅当 CHANGE_TRACKING 为 OFF 时，才能使用 NO POPULATION 选项。 如果指定了 NO POPULATION，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在创建索引后不会对其进行填充。 仅当用户使用 START FULL POPULATION 或 START INCREMENTAL POPULATION 子句执行 ALTER FULLTEXT INDEX 命令之后，才会填充索引。  
  
 非索引字表 [=] {OFF |**系统** | *stoplist_name* }  
 将全文非索引字表与索引关联起来。 不使用属于指定非索引字表的任何标记填充索引。 如果未指定 STOPLIST，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将系统全文非索引字表与索引关联起来。  
  
 OFF  
 指定没有与全文索引关联的非索引字表。  
  
 **系统**  
 指定应对此全文索引使用默认的全文系统 STOPLIST。  
  
 *stoplist_name*  
 指定要与全文索引关联的非索引字表的名称。  
  
 搜索属性列表 [=] *property_list_name*  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将搜索属性列表与索引相关联。  
  
 OFF  
 指定不会将任何属性列表与全文索引相关联。  
  
 *property_list_name*  
 指定要与全文索引关联的搜索属性列表的名称。  
  
## <a name="remarks"></a>注释  
 有关全文索引的详细信息，请参阅[创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。  
  
 上**xml**列，你可以创建一个全文索引，它的 XML 元素，对内容进行索引，但将忽略 XML 标记。 不为数值的属性值都会进行全文索引。 元素标记用作标记边界。 支持包含多种语言的格式正确的 XML 或 HTML 文档和片段。 有关详细信息，请参阅 [结合使用具有全文搜索和 XML 列](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)。  
  
 建议索引键列为整数数据类型。 这可在执行查询时提供优化。  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>更改跟踪和 NO POPULATION 参数的交互  
 是否填充全文索引取决于是否启用了更改跟踪以及在 ALTER FULLTEXT INDEX 语句中是否指定了 WITH NO POPULATION。 下表概述了其交互结果。  
  
|更改跟踪|WITH NO POPULATION|结果|  
|---------------------|------------------------|------------|  
|未启用|未指定|对索引执行完全填充。|  
|未启用|Specified|在发出 ALTER FULLTEXT INDEX...START POPULATION 语句之前，不会进行任何索引填充。|  
|已启用|指定|引发错误，并且不会更改索引。|  
|已启用|未指定|对索引执行完全填充。|  
  
 有关填充的全文索引的详细信息，请参阅[填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
## <a name="permissions"></a>Permissions  
 用户必须对全文目录拥有 REFERENCES 权限，对表或索引视图拥有 ALTER 权限，或者必须是 sysadmin 固定服务器角色、db_owner 或 db_ddladmin 固定数据库角色的成员。  
  
 如果指定了 SET STOPLIST，则用户必须具有指定非索引字表的 REFERENCES 权限。 此 STOPLIST 的所有者可授予此权限。  
  
> [!NOTE]  
>  授予 public 对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 随附的默认非索引字表的 REFERENCE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. 创建唯一索引、全文目录和全文索引  
 以下示例对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库中 `JobCandidateID` 表的 `HumanResources.JobCandidate` 列创建全文索引。 然后，该示例创建一个默认全文目录 `ft`。 最后，该示例使用 `Resume` 目录和系统非索引字表对 `ft` 列创建全文索引。  
  
```  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. 为多个表列创建全文索引  
 以下示例在 `production_catalog` 示例数据库中创建一个全文目录 `AdventureWorks`。 然后，该示例创建一个使用该新目录的全文索引。 此全文索引位于 `ReviewerName` 的 `EmailAddress`、`Comments` 和 `Production.ProductReview` 列上。 对于每个列，该示例指定英语的 LCID `1033`，这是列中的数据语言。 该全文索引使用现有的唯一键索引 `PK_ProductReview_ProductReviewID`。 根据建议，此索引键位于整数列 `ProductReviewID` 中。  
  
```  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. 使用搜索属性列表创建全文索引而不填充该索引  
 以下示例为 `Title` 表的 `DocumentSummary`、`Document` 和 `Production.Document` 列创建全文索引。 该示例指定英语的 LCID `1033`，这是列中的数据语言。 此全文索引使用默认的全文目录和现有的唯一键索引 `PK_Document_DocumentID`。 根据建议，此索引键位于整数列 `DocumentID` 中。  
  
 该示例指定 SYSTEM 非索引字表。 它还指定的搜索属性列表， `DocumentPropertyList`; 例如，创建此属性列表，请参阅[CREATE SEARCH PROPERTY LIST &#40;Transact SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
 该示例指定关闭更改跟踪并且不进行填充。 随后，在非峰值时间，该示例使用 ALTER FULLTEXT INDEX 语句对新索引开始进行完全填充，并启用自动更改跟踪。  
  
```  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 随后，在非峰值时间，填充索引：  
  
```  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

