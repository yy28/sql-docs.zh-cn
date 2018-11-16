---
title: CONTAINSTABLE (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONTAINSTABLE
- CONTAINSTABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- fuzzy (less precise) word or phrase search [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- values [SQL Server], ranked
- LANGUAGE option
- NEAR option [full-text search]
- RANK column
- phrase searches [full-text search]
- conditions [SQL Server], CONTAINSTABLE
- relevance ranking values [full-text search]
- proximity searches [full-text search]
- CONTAINSTABLE function (Transact-SQL)
- ranked results [full-text search]
- rankings [full-text search]
- less precise (fuzzy) searches [full-text search]
ms.assetid: e580c210-cf57-419d-9544-7f650f2ab814
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3614abd1e02425dcda0943f3e4b3773eeb8b4499
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660100"
---
# <a name="containstable-transact-sql"></a>CONTAINSTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个表的零个、 一个或多个行的这些列包含的精确或模糊 （不太精确） 匹配项将单个单词和短语，词、 一定范围内的相近或加权匹配项。 CONTAINSTABLE 用[FROM 子句](../../t-sql/queries/from-transact-sql.md)的[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 语句和引用，就好象它是一个常规表名。 它执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]全文搜索的全文索引包含基于字符的数据类型的列。  
  
 CONTAINSTABLE 可用于相同类型的匹配项作为[CONTAINS 谓词](../../t-sql/queries/contains-transact-sql.md)和使用与 CONTAINS 相同的搜索条件。  
  
 但与 CONTAINS 不同，使用 CONTAINSTABLE 的查询对每一行返回一个相关性排名值 (RANK) 和全文键 (KEY)。  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的全文搜索形式的信息，请参阅[使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CONTAINSTABLE   
( table , { column_name | ( column_list ) | * } , ' <contains_search_condition> '   
     [ , LANGUAGE language_term]   
  [ , top_n_by_rank ]   
)   
  
<contains_search_condition> ::=   
    { <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    |  <weighted_term>   
    }   
    | { ( <contains_search_condition> )   
    { { AND | & } | { AND NOT | &! } | { OR | | } }   
     <contains_search_condition> [ ...n ]   
    }  
  
<simple_term> ::=   
     { word | "phrase" }  
<prefix term> ::=   
     { "word*" | "phrase*" }   
<generation_term> ::=   
     FORMSOF ( { INFLECTIONAL | THESAURUS } , <simple_term> [ ,...n ] )   
  
<generic_proximity_term> ::=   
     { <simple_term> | <prefix_term> } { { { NEAR | ~ }   
     { <simple_term> | <prefix_term> } } [ ...n ] }  
  
<custom_proximity_term> ::=   
  NEAR (   
     {  
        { <simple_term> | <prefix_term> } [ ,…n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,…n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
     ISABOUT  
    ( { {   
  <simple_term>   
  | <prefix_term>   
  | <generation_term>   
  | <proximity_term>   
  }   
   [ WEIGHT ( weight_value ) ]   
   } [ ,...n ]   
    )  
  
```  
  
## <a name="arguments"></a>参数  
 *table*  
 已进行了全文索引的表的名称。 *表*可以是由一个、 两个、 三个或四个部分组成的数据库对象名称。 查询视图时，仅能涉及一个全文索引的基表。  
  
 *表*不能指定服务器名称和不能对链接服务器的查询中使用。  
  
 column_name  
 是为进行全文搜索而编制了索引的一个或多个列的名称。 列可以是 char、varchar、nchar、nvarchar、text、ntext、image、xml、varbinary 或 varbinary(max) 类型。  
  
 *column_list*  
 指示可以指定多个列（以逗号分隔）。 column_list 必须用括号括起来。 除非指定 language_term，否则 column_list 中所有列的语言必须相同。  
  
 \*  
 指定所有全文都索引中的列*表*应该用于搜索给定的搜索条件。 除非指定 language_term，否则表的所有列的语言必须相同。  
  
 LANGUAGE language_term  
 是其资源将用于断字、 词干分析、 同义词库和干扰词的语言 (或[非索引字](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 删除，因为查询的一部分。 此参数是可选的，可以将其指定为与语言区域设置标识符 (LCID) 对应的字符串、整数或十六进制值。 如果指定了 language_term，则它表示的语言将应用于搜索条件的所有元素。 如果未指定值，则使用该列的全文语言。  
  
 如果将不同语言的文档一起作为二进制大型对象 (BLOB) 存储在单个列中，则指定文档的区域设置标识符 (LCID) 将决定对其内容编制索引时使用哪种语言。 在对这种列进行查询时，指定 LANGUAGElanguage_term 可增大找到有效匹配项的可能性。  
  
 当指定为字符串， *language_term*对应于**别名**中列的值[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)兼容性视图。  字符串必须用单引号引起来，如 'language_term'。 如果指定为整数，则 language_term 就是标识该语言的实际 LCID。 如果指定为十六进制值，则 language_term 将以 0x 开头，后跟 LCID 的十六进制值。 十六进制值不能超过八位（包括前导零在内）。  
  
 如果该值是双字节字符集 (DBCS) 格式，则 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将其转换为 Unicode 格式。  
  
 如果指定的语言无效，或者未安装对应于该语言的资源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。 若要使用非特定语言资源，请将 0x0 指定为 language_term。  
  
 *top_n_by_rank*  
 指定仅*n*最高排名的匹配项，按降序返回。 仅适用于整数值， *n*，指定。 如果 *top_n_by_rank* 与其他参数组合使用，则查询返回的行数可能会少于实际与所有谓词都匹配的行数。 *top_n_by_rank*允许您通过调取仅最相关的命中项来提高查询性能。  
  
 <contains_search_condition>  
 指定要在 column_name 中搜索的文本和匹配条件。 有关搜索条件的信息，请参阅[包含&#40;TRANSACT-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
## <a name="remarks"></a>备注  
 全文谓词和函数作用于 FROM 谓词所示的单个表。 若要对多个表进行搜索，请在 FROM 子句中使用联接表，以搜索由两个或更多个表的乘积构成的结果集。  
  
 返回表中有一个名为列**密钥**，其中包含全文键值。 每个全文索引的表包含的列的值一定是唯一的和中返回的值**密钥**列是全文索引键值的行中指定的选择条件匹配的包含搜索条件。 **TableFulltextKeyColumn**属性，从 OBJECTPROPERTYEX 函数获取提供此唯一键列的标识。 若要获取与全文索引的全文键相关联的列的 ID，请使用**sys.fulltext_indexes**。 有关详细信息，请参阅[sys.fulltext_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)。  
  
 若要从原始表中获得所需要的行，请指定与 CONTAINSTABLE 行的联接。 使用 CONTAINSTABLE 的 SELECT 语句的 FROM 子句的典型形式为：  
  
```  
SELECT select_list  
FROM table AS FT_TBL INNER JOIN  
   CONTAINSTABLE(table, column, contains_search_condition) AS KEY_TBL  
   ON FT_TBL.unique_key_column = KEY_TBL.[KEY];  
```  
  
 CONTAINSTABLE 生成的表包括一个名为**排名**。 **排名**列对于每个行，该值指示行与选择条件的匹配程度为一个值 （介于 0 到 1000 之间)。 在 SELECT 语句中，此排名值通常按照下列方法之一使用：  
  
-   在 ORDER BY 子句中返回排名最高的行作为表的第一行。  
  
-   在选择列表中查看分配给每一行的排名值。  
  
## <a name="permissions"></a>Permissions  
 只有对表或被引用表的列具有适当 SELECT 权限的用户才具有执行权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example"></a>A. 简单示例  
 下面的示例创建并填充一个简单的表的两个列，其中列出了 3 个所在国家/地区和其标志中的颜色。 It 创建并填充全文目录和索引的表。 然后**CONTAINSTABLE**语法进行了演示。 此示例演示如何在搜索值满足多个时间时更高版本增长的排名值。 在最后一个查询中，其中包含绿色和黑色坦桑尼亚具有比意大利，其中包含一个查询颜色较高的排名。  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green') ORDER BY RANK DESC;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green or Black') ORDER BY RANK DESC;  
```  
  
### <a name="b-returning-rank-values"></a>B. 返回排名值  
 下面的示例搜索包含词“frame”、“wheel”或“tire”的所有产品名称，并为每个词指定了不同的权重。 对于满足这些搜索条件的每个返回行，都将显示匹配的相关程度（排名值）。 此外，排名最高的行将首先返回。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Name, KEY_TBL.RANK  
    FROM Production.Product AS FT_TBL   
        INNER JOIN CONTAINSTABLE(Production.Product, Name,   
        'ISABOUT (frame WEIGHT (.8),   
        wheel WEIGHT (.4), tire WEIGHT (.2) )' ) AS KEY_TBL  
            ON FT_TBL.ProductID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="c-returning-rank-values-greater-than-a-specified-value"></a>C. 返回大于指定值的排名值  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
 下面的示例使用 NEAR 搜索 `bracket` 表中彼此相近的“`reflector`”和“`Production.Document`”。 仅返回排名值为 50 或排名值更高的行。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  如果全文查询没有指定一个整数作为最大距离，则只包含相隔距离大于 100 个逻辑词的匹配项的文档将不满足 NEAR 要求，其排名将为 0。  
  
### <a name="d-returning-top-5-ranked-results-using-topnbyrank"></a>D. 使用 top_n_by_rank 返回排名前 5 位的结果  
 下面的示例返回前 5 个产品的说明，其中 `Description` 列在单词“light”或“lightweight”附近包含字词“aluminum”。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
 `GO`  
  
### <a name="e-specifying-the-language-argument"></a>E. 指定 LANGUAGE 参数  
 以下示例说明了如何使用 `LANGUAGE` 参数。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      LANGUAGE N'English',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
> [!NOTE]  
>  语言*language_term*不使用所需的 argumentis *top_n_by_rank。*  
  
## <a name="see-also"></a>请参阅  
 [使用 RANK 限制搜索结果](../../relational-databases/search/limit-search-results-with-rank.md)   
 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)   
 [创建全文搜索查询 (Visual Database Tools)](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS (Transact-SQL)](../../t-sql/queries/contains-transact-sql.md)   
 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)  
  
  
