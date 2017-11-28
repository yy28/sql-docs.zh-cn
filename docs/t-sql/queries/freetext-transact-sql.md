---
title: "FREETEXT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREETEXT
- FREETEXT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXT predicate (Transact-SQL)
- words in predicate [full-text search]
- column searches [full-text search]
ms.assetid: 2f199d3c-440e-4bcf-bdb5-82bb3994005d
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9c7475e73cbd5022bf5c243fbd4e7a35dc115cf0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="freetext-transact-sql"></a>FREETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  是一个谓词中使用[!INCLUDE[tsql](../../includes/tsql-md.md)] [WHERE 子句](../../t-sql/queries/where-transact-sql.md)的[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 语句以执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的全文搜索上的全文索引列中包含基于字符的数据类型。 该谓词将搜索含义与搜索条件中的单词相同但不完全匹配的值。 使用 FREETEXT 时，全文查询引擎内部执行下列操作上*freetext_string*、 分配的权重，每个字词，然后查找匹配项：  
  
-   基于单词边界（断字）将字符串分隔成单独的单词。  
  
-   生成单词的词形变化形式（词干处理）。  
  
-   基于同义词库中的匹配项标识字词的扩展或替换的列表。  
  
> [!NOTE]  
>  有关支持的全文搜索的窗体信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
FREETEXT ( { column_name | (column_list) | * }   
          , 'freetext_string' [ , LANGUAGE language_term ] )  
```  
  
## <a name="arguments"></a>参数  
 *column_name*  
 FROM 子句中指定表的一个或多个全文索引列的名称。 列可以是类型**char**， **varchar**， **nchar**， **nvarchar**，**文本**， **ntext**，**映像**， **xml**， **varbinary**，或**varbinary （max)**。  
  
 *column_list*  
 指示可以指定多个列（以逗号分隔）。 *column_list*必须括在括号中。 除非*language_term*指定的所有列的语言*column_list*必须相同。  
  
 \*  
 指定已为全文搜索注册的所有列应该都用于搜索给定*freetext_string*。 如果多个表在 FROM 子句中，\*必须由表名进行限定。 除非*language_term*表的所有列的语言必须相同的指定。  
  
 *freetext_string*  
 是要在中搜索文本*column_name*。 可以输入任何文本，包括单词、短语或句子。 只要在全文索引中找到任何术语或术语格式，就会生成匹配项。  
  
 与不同在 CONTAINS 和 CONTAINSTABLE 搜索条件的位置和中使用时，是关键字， *freetext_string*单词和被视为干扰词，或[非索引字](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)，并且将被放弃。  
  
 不允许使用 WEIGHT、FORMSOF、通配符、NEAR 和其他语法。 *freetext_string* wordbroken，词干，并通过同义词库。  
  
 *freetext_string*是**nvarchar**。 将另一个字符数据类型用作输入时，将发生隐式转换。 不能使用大的字符串数据类型 nvarchar （max） 和 varchar （max）。 在下面的示例中，`@SearchWord` 变量（被定义为 `varchar(30)`）导致 `FREETEXT` 谓词中发生隐式转换。  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 由于"参数查找"无法跨转换，使用**nvarchar**以提高性能。 在示例中，声明`@SearchWord`作为`nvarchar(30)`。  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 在其中生成并非最佳计划的情况下，你还可以使用 OPTIMIZE FOR 查询提示。  
  
 语言*language_term*  
 特定的语言，查询时，其资源将用于断字、词干分析、同义词库查询以及非索引字删除。 此参数是可选的，可以将其指定为与语言区域设置标识符 (LCID) 对应的字符串、整数或十六进制值。 如果*language_term*指定，它表示的语言将应用到的搜索条件的所有元素。 如果未指定值，则使用该列的全文语言。  
  
 如果将不同语言的文档一起作为二进制大型对象 (BLOB) 存储在单个列中，则指定文档的区域设置标识符 (LCID) 将决定对其内容编制索引时使用哪种语言。 在查询这样的列时，指定*语言**language_term*可以增加很好的匹配项的概率。  
  
 当指定为一个字符串， *language_term*对应于**别名**中他列值[sys.syslanguages &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)兼容性视图。  在情况下，字符串必须括在单引号中，*language_term*。 如果为一个整数，指定*language_term*是实际标识的语言的 LCID。 当指定为十六进制值， *language_term* 0x 后跟 LCID 的十六进制值。 十六进制值不能超过八位（包括前导零在内）。  
  
 如果值为双字节字符集 (dbcs) 格式， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会将它转换为 Unicode。  
  
 如果指定的语言不是有效，或者将没有资源将安装对该语言对应[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回错误。 若要使用的非特定语言资源，指定为 0x0 *language_term*。  
  
## <a name="general-remarks"></a>一般备注  
 全文谓词和函数作用于 FROM 谓词所示的单个表。 若要对多个表进行搜索，请在 FROM 子句中使用联接表，以搜索由两个或更多个表的乘积构成的结果集。  
  
使用 FREETEXT 的全文查询没有使用 CONTAINS 的全文查询精度高。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文搜索引擎识别重要的字词和短语。 没有特殊含义授予给任何保留的关键字或通常有含义时中指定的通配符字符的\<contains_search_condition > CONTAINS 谓词的参数。
  
 中不允许使用全文谓词[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md)当数据库兼容级别设置为 100。  
  
> [!NOTE]  
>  FREETEXTTABLE 函数用来搜索的匹配项的种类与 FREETEXT 谓词相同。 你可以引用常规表名中所示的此函数[FROM 子句](../../t-sql/queries/from-transact-sql.md)SELECT 语句。 有关详细信息，请参阅[FREETEXTTABLE &#40;Transact SQL &#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md).  
  
## <a name="querying-remote-servers"></a>查询远程服务器  
 你可以使用中的四部分名称[CONTAINS](../../t-sql/queries/contains-transact-sql.md)或 FREETEXT 谓词来查询的全文索引的链接服务器上的目标表的列。 若要准备远程服务器以接收全文查询，请在远程服务器上的目标表和列上创建全文索引，然后将该远程服务器添加为链接服务器。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE 与全文搜索的比较  
 与全文搜索不同，[LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 谓词仅对字符模式有效。 另外，不能使用 LIKE 谓词来查询格式化的二进制数据。 此外，对大量非结构化的文本数据执行 LIKE 查询要比对相同数据执行同样的全文查询慢得多。 对数百万行文本数据进行的 LIKE 查询可能需要几分钟的时间才能返回结果；而对于同样的数据，全文查询只需要几秒甚至更少的时间，具体取决于返回的行数。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-freetext-to-search-for-words-containing-specified-character-values"></a>A. 使用 FREETEXT 搜索包含指定字符值的单词  
 以下示例搜索包含与 vital、safety、components 相关的单词的所有文档。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components' );  
GO  
```  
  
### <a name="b-using-freetext-with-variables"></a>B. 通过变量使用 FREETEXT  
 以下示例使用变量替代具体的搜索词。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30);  
SET @SearchWord = N'high-performance';  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索入门](../../relational-databases/search/get-started-with-full-text-search.md)   
 [创建和管理全文索引目录](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [创建 FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)   
 [创建全文搜索查询 (Visual Database Tools)](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS (Transact-SQL)](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
