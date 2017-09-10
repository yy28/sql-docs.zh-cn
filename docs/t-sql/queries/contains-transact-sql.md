---
title: "包含 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- CONTAINS predicate (Transact-SQL)
- conditions [SQL Server], CONTAINS
- fuzzy (less precise) word or phrase search [full-text search]
- word weighting values [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- LANGUAGE option
- word inflectionally generated from another [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- word near another word search [full-text search]
- full-text search [SQL Server], searching on a property
- proximity searches [full-text search]
- less precise (fuzzy) searches [full-text search]
- property searching [SQL Server], searching on a property
- inflectional forms [full-text search]
- prefix searches [full-text search]
ms.assetid: 996c72fc-b1ab-4c96-bd12-946be9c18f84
caps.latest.revision: 117
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 67d85ab09ac28beca984372e3df2bd6a1ca0bfa3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="contains-transact-sql"></a>CONTAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中搜索单个词和短语的精确或模糊（不太精确的）匹配项、在一定差别范围内的相近词或加权匹配项。 CONTAINS 是采用一个谓词[WHERE 子句](../../t-sql/queries/where-transact-sql.md)的[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 语句以执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的全文搜索上的全文索引列中包含基于字符的数据类型。  
  
 CONTAINS 谓词可以搜索：  
  
-   词或短语。  
  
-   词或短语的前缀。  
  
-   与另一个词相邻的词。  
  
-   由另一个词的词形变化而生成的词（例如，drive 一词是 drives、drove、driving 和 driven 词形变化的词干）。  
  
-   使用同义词库确定的另一个词的同义词（例如，“metal”一词可能有“aluminum”和“steel”等同义词）。  
  
 有关支持的全文搜索的窗体信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)。  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CONTAINS (   
     {   
        column_name | ( column_list )   
      | *   
      | PROPERTY ( { column_name }, 'property_name' )    
     }   
     , '<contains_search_condition>'  
     [ , LANGUAGE language_term ]  
   )   
  
<contains_search_condition> ::=   
  {   
      <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    | <weighted_term>   
    }   
  |   
    { ( <contains_search_condition> )   
        [ { <AND> | <AND NOT> | <OR> } ]   
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
   ( {   
        {   
          <simple_term>   
        | <prefix_term>   
        | <generation_term>   
        | <proximity_term>   
        }   
      [ WEIGHT ( weight_value ) ]   
      } [ ,...n ]   
   )   
  
<AND> ::=   
  { AND | & }  
  
<AND NOT> ::=   
  { AND NOT | &! }  
  
<OR> ::=   
  { OR | | }  
  
```  
  
## <a name="arguments"></a>参数  
 *column_name*  
 FROM 子句中所指定的表的全文索引列的名称。 列可以是类型**char**， **varchar**， **nchar**， **nvarchar**，**文本**， **ntext**，**映像**， **xml**， **varbinary**，或**varbinary （max)**。  
  
 *column_list*  
 指定以逗号分隔的两个或更多个列。 *column_list*必须括在括号中。 除非*language_term*指定的所有列的语言*column_list*必须相同。  
  
 \*  
 指定查询给定的搜索条件的 FROM 子句中指定的表中搜索所有全文索引的列。 CONTAINS 子句中的列必须来自包含全文索引的单个表。 除非*language_term*表的所有列的语言必须相同的指定。  
  
 属性 ( *column_name* ，*property_name*)  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定在其中搜索指定搜索条件的文档属性。  
  
> [!IMPORTANT]  
>  要返回任何行，使查询*property_name*必须指定在搜索属性中的全文索引和全文索引列表必须包含的特定属性条目*property_name*。 有关详细信息，请参阅 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
 语言*language_term*  
 是要用于断字、 词干分析、 同义词库扩展和替换和干扰词的语言 (或[非索引字](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 作为查询的一部分删除。 此参数可选。  
  
 如果将采用不同语言的文档一起作为二进制大型对象 (BLOB) 存储在单个列中，则给定文档的区域设置标识符 (LCID) 将决定为其内容编制索引时使用的语言。 在查询这样的列时，指定语言*language_term*可以增加很好的匹配项的概率。  
  
 *language_term*可以指定为字符串、 整数或与一种语言的 LCID 对应的十六进制值。 如果*language_term*指定，它表示的语言应用到的搜索条件的所有元素。 如果未指定值，则使用该列的全文语言。  
  
 当指定为一个字符串， *language_term*对应于**别名**中的列值[sys.syslanguages &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)兼容性视图。 在情况下，字符串必须括在单引号中，*language_term*。 如果为一个整数，指定*language_term*是实际标识的语言的 LCID。 当指定为十六进制值， *language_term* 0x 后跟 LCID 的十六进制值。 十六进制值不能超过八位（包括前导零在内）。  
  
 如果值为双字节字符集 (dbcs) 格式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将其转换为 Unicode。  
  
 如果指定的语言无效，或者未安装对应于该语言的资源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。 若要使用的非特定语言资源，指定为 0x0 *language_term*。  
  
 \<*contains_search_condition*>  
 指定要在中搜索的文本*column_name*匹配项的条件。  
  
*\<contains_search_condition >*是**nvarchar**。 将另一个字符数据类型用作输入时，将发生隐式转换。 在下面的示例中，`@SearchWord` 变量（被定义为 `varchar(30)`）导致 `CONTAINS` 谓词中发生隐式转换。
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 由于"参数查找"无法跨转换，使用**nvarchar**以提高性能。 在示例中，声明`@SearchWord`作为`nvarchar(30)`。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 对于生成非最佳计划的情况，还可以使用 OPTIMIZE FOR 查询提示。  
  
 *word*  
 不带空格或标点符号的字符串。  
  
 *短语*  
 在每个词之间有空格的一个或多个词。  
  
> [!NOTE]  
>  某些语言（如亚洲一些地区的书面语言）的短语可以由彼此之间没有空格的一个或多个词组成。  
  
\<simple_term >  
指定词或短语的完全匹配项。 有效的简单字词示例有 "blue berry"、blueberry 和 "Microsoft SQL Server"。 应该使用双引号 ("") 将短语引起来。 短语中的词必须中指定相同的顺序出现 *\<contains_search_condition >*在数据库列中显示。 搜索词或短语中的字符时不区分大小写。 干扰词 (或[非索引字](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) (如，和，或) 的全文索引中未存储在全文索引列。 如果在单个词搜索中使用了干扰词，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误消息，指出查询仅包含干扰词。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 \Mssql\Binn\FTERef 目录下有一个标准的干扰词列表。  
  
 标点将被忽略。 因此，`CONTAINS(testing, "computer failure")` 将匹配包含 "Where is my computer?  Failure to find it would be expensive" 这个值的行。 有关断字符行为的详细信息，请参阅[配置和管理断字符和词干分析器以便搜索](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 \<prefix_term >  
 指定以指定文本开始的词或短语的匹配项。 将前缀词括在双引号 ("") 并添加一个星号 (\*) 之前在结束引号，以便从开始简单词的所有文本前面都指定星号匹配。 该子句应按以下方式指定：`CONTAINS (column, '"text*"')`。 星号可匹配词或短语所含根词的 0 个、1 个或多个字符。 如果文本和星号不用英文双引号分隔，则谓词将读取 `CONTAINS (column, 'text*')`，全文搜索会将星号看作字符，搜索 `text*` 的完全匹配项。 全文引擎将找不到带星号的单词 (\*) 字符因为断字符通常忽略此类字符。  
  
 当 *\<prefix_term >*是短语，短语中包含每个词都被看作是一个单独的前缀。 因此，指定了一个 "local wine*" 前缀字词的查询，将匹配所有包含 "local winery"、"locally wined and dined" 等文本的行。  
  
 \<generation_term >  
 包含的简单字词包括要搜索的原始词的变体时，指定词的匹配项。  
  
 INFLECTIONAL  
 指定要对指定的简单字词使用与语言相关的词干分析器。 词干分析器的行为是根据每种具体语言的词干确定规则定义的。 非特定语言没有关联的词干分析器。 使用被查询的列的列语言来引用所需的词干分析器。 如果*language_term*指定，则对应于使用语言的词干分析器。  
  
 给定 *\<simple_term >*内 *\<generation_term >*名词和动词将不匹配。  
  
 THESAURUS  
 指定使用对应于列全文语言或指定的查询语言的同义词库。 最长的模式或从模式 *\<simple_term >*针对同义词库匹配并生成附加条款的展开或替换原始的模式。 如果为所有或部分找不到匹配项 *\<simple_term >*，不匹配部分将被视为*simple_term*。 全文搜索同义词库的详细信息，请参阅[为配置和管理同义词库文件的全文搜索](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
 \<generic_proximity_term >  
 指定词或短语的匹配项必须处于所搜索的文档中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我们建议你使用\<custom_proximity_term >。  
  
 NEAR | ~  
 指示 NEAR 或 ~ 运算符两侧的词或短语必须存在于某个文档中，才能返回匹配项。 您必须指定两个搜索词。 给定的搜索词可以是单个单词或由双引号分隔的短语 ("*短语*")。  
  
 可将多个邻近词链接起来，例如 `a NEAR b NEAR c` 或 `a ~ b ~ c`。 链接在一起的邻近词必须均存在于文档中才能返回匹配项。  
  
 例如，`CONTAINS(*column_name*, 'fox NEAR chicken')`和`CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')`将同时返回任何文档指定列中包含"fox"和"小鸡"。 此外，CONTAINSTABLE 还会按照 "fox" 和 "chicken" 的邻近程度返回每个文档的排名。 例如，如果文档包含句子“The fox ate the chicken”，该文档的排名将很高，因为这两个词比其他文档近。  
  
 了解通用邻近术语的详细信息，请参阅[邻近的词到另一个单词使用 NEAR 搜索](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<custom_proximity_term >  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
 指定词或短语的匹配项，并且可以选择指定搜索词之间允许的最大距离。 你还可以指定搜索词必须位于指定它们的确切顺序 (\<match_order >)。  
  
 给定的搜索词可以是单个单词或由双引号分隔的短语 ("*短语*")。 文档中必须包含每个指定的词才能返回匹配项。 您必须至少指定两个搜索词。 最大的搜索词数为 64 个。  
  
 默认情况下，自定义近似词返回包含指定词的行，而不考虑间隔的距离及其顺序。 例如，若要匹配下面的查询，文档只需包含 `term1` 和 "`term3 term4`"，它们可以处于任意位置以及采用任意顺序：  
  
```  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 可选的参数如下：  
  
 \<maximum_distance >  
 指定要使字符串作为匹配项，字符串开头和结尾处的搜索词之间允许的最大距离。  
  
 *integer*  
 指定 0 到 4294967295 之间的正整数。 该值控制第一个和最后一个搜索词之间可以包含多少个非搜索词，不包括任何其他指定的搜索词。  
  
 例如，以下查询将搜索`AA`和`BB`，按任意顺序中的五个最大距离。  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 字符串`AA one two three four five BB`将匹配项。 在下面的示例中，该查询指定为三个搜索词， `AA`， `BB`，和`CC`内最大距离为 5:  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 此查询将匹配以下字符串（总距离为 5）：  
  
 `BB   one two   CC   three four five A  A`  
  
 请注意内部搜索词， `CC`，不会进行计数。  
  
 **最大值**  
 返回所有包含指定词的行，而不考虑它们之间距离。 这是默认设置。  
  
 \<match_order >  
 指定词是否必须按指定顺序出现，搜索查询才会返回这些词。 若要指定\<match_order >，则还必须指定\<maximum_distance >。  
  
 \<match_order > 采用以下值之一：  
  
 **TRUE**  
 强制在词中使用指定的顺序。 例如，`NEAR(A,B)` 仅匹配 `A … B`。  
  
 **FALSE**  
 忽略指定的顺序。 例如，`NEAR(A,B)` 匹配 `A … B` 和 `B … A`。  
  
 这是默认设置。  
  
 例如，以下邻近词按指定顺序搜索“`Monday`”、“`Tuesday`”和“`Wednesday`”词，而不考虑它们之间的距离：  
  
```  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 有关使用自定义邻近词的详细信息，请参阅[邻近的词到另一个单词使用 NEAR 搜索](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<weighted_term >  
 指定（由查询返回的）匹配行与一组词和短语匹配，每个词和短语有一个可选的加权值。  
  
 ISABOUT  
 指定 *\<weighted_term >*关键字。  
  
 权重 (*weight_value*)  
 指定介于 0.0 和 1.0 之间的加权值。 在每个组件 *\<weighted_term >*可能包括*weight_value*。 *weight_value*是一种更改的查询的各个部分会影响分配到与查询匹配的每一行的排名值方法。 权重不会影响结果的 CONTAINS 查询，但中的权重影响级别[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)查询。  
  
> [!NOTE]  
>  不管操作系统的区域设置如何，小数点分隔符始终为句点。  
  
 { AND | & } | { AND NOT | &! } | { OR | | }  
 指定两个包含搜索条件之间的逻辑运算。  
  
 {和 | （& A)}  
 指示匹配项必须满足这两个包含搜索条件。 可以使用 And 符 (&) 代替关键字 AND 来表示 AND 运算符。  
  
 {而不 | & ！ }  
 指示匹配项中不能出现第二个搜索条件。 可以使用 And 符后跟感叹号 (&!) 代替关键字 AND NOT 来表示 AND NOT 运算符。  
  
 {或 | |}  
 指示匹配项必须满足这两个包含搜索条件之一。 可以使用竖线符号 (|) 代替关键字 OR 来表示 OR 运算符。  
  
 当 *\<contains_search_condition >*包含括号中的组，首先评估组的这些用圆括号括起来。 计算了带括号的组之后，将这些逻辑运算符用于包含搜索条件时，适用以下规则：  
  
-   NOT 用在 AND 之前。  
  
-   NOT 只能出现在 AND 之后，如在 AND NOT 中。 不允许使用 OR NOT 运算符。 不能在首个字词前指定 NOT。 例如，`CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )` 就是无效的。  
  
-   AND 用在 OR 之前。  
  
-   相同类型的 Boolean 运算符（AND、OR）可以结合使用，因此可以按任意顺序应用。  
  
 *n*  
 一个占位符，指示可在其中指定多个 CONTAINS 搜索条件和搜索词。  
  
## <a name="general-remarks"></a>一般备注  
 全文谓词和函数作用于 FROM 谓词所示的单个表。 若要对多个表进行搜索，请在 FROM 子句中使用联接表，以搜索由两个或更多个表的乘积构成的结果集。  
  
 中不允许使用全文谓词[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md)当数据库兼容级别设置为 100。  
  
## <a name="querying-remote-servers"></a>查询远程服务器  
 你可以在 CONTAINS 使用由四部分构成的名称或[FREETEXT](../../t-sql/queries/freetext-transact-sql.md)谓词来查询的全文索引列中的链接服务器上的目标表。 若要准备远程服务器以接收全文查询，请在远程服务器上的目标表和列上创建全文索引，然后将该远程服务器添加为链接服务器。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE 与全文搜索的比较  
 与全文搜索不同，[LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 谓词仅对字符模式有效。 另外，不能使用 LIKE 谓词来查询格式化的二进制数据。 此外，对大量非结构化的文本数据执行 LIKE 查询要比对相同数据执行同样的全文查询慢得多。 对数百万行文本数据进行的 LIKE 查询可能需要几分钟的时间才能返回结果；而对于同样的数据，全文查询只需要几秒甚至更少的时间，具体取决于返回的行数及其大小。 另一个考虑因素是 LIKE 仅对整个表执行简单模式扫描。 相反，全文查询可识别语言，它在索引和查询时应用特定的转换，例如，筛选非索引字并进行同义词库和变形扩展。 这些转换可帮助全文查询改进其撤回以及结果的最终排名。  
  
## <a name="querying-multiple-columns-full-text-search"></a>查询多个列（全文搜索）  
 可通过指定一组要搜索的列来查询多个列。 这些列必须来自同一个表。  
  
 例如，下面的 CONTAINS 查询搜索单词`Red`中`Name`和`Color`列`Production.Product`表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]示例数据库。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-contains-with-simpleterm"></a>A. 使用与 CONTAINS \<simple_term >  
 下面的示例查找包含 `$80.99` 一词且价格为 `Mountain`的所有产品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain');  
GO  
```  
  
### <a name="b-using-contains-and-phrase-with-simpleterm"></a>B. 使用 CONTAINS 和带有短语\<simple_term >  
 以下示例返回包含短语 `Mountain` 或 `Road` 的所有产品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefixterm"></a>C. 使用与 CONTAINS \<prefix_term >  
 下面的示例返回的所有产品名称中，其 `Name` 列中至少有一个词以前辍 chain 开头。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefixterm"></a>D. 使用 CONTAINS and \<prefix_term >  
 下面的示例将返回包含以 `chain` 或 `full` 为前缀的字符串的所有类别说明。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximityterm"></a>E. 使用与 CONTAINS \<proximity_term >  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 下面的示例搜索`Production.ProductReview`包含单词的所有注释的表`bike`10 个词以内的单词"`control`"和以指定顺序 (即，其中"`bike`"之前"`control`")。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generationterm"></a>F. 使用与 CONTAINS \<generation_term >  
 下面的示例将搜索包含单词 `ride` 的各种形式（如 riding 和 ridden 等）的所有产品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weightedterm"></a>G. 使用与 CONTAINS \<weighted_term >  
 以下示例搜索包含 `performance`、`comfortable` 或 `smooth` 词并为每个词指定不同加权的所有产品名称。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, 'ISABOUT (performance weight (.8),   
comfortable weight (.4), smooth weight (.2) )' );  
GO  
```  
  
### <a name="h-using-contains-with-variables"></a>H. 将 CONTAINS 与变量一起使用  
 以下示例使用变量替代具体的搜索词。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>I. 将 CONTAINS 与逻辑运算符 (AND) 一起使用  
 下面的示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的 ProductDescription 表。 查询使用 CONTAINS 谓词搜索的说明中的说明 ID 不等于 5 和描述包含这两个词`Aluminum`和 word `spindle`。 该搜索条件使用 AND 布尔运算符。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>J. 使用 CONTAINS 验证行插入操作  
 下面的示例在 SELECT 子查询中使用 CONTAINS。 该查询将使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库获取 ProductReview 表中针对某一特定循环的所有注释的注释值。 该搜索条件使用 AND 布尔运算符。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.ProductReview   
  (ProductID, ReviewerName, EmailAddress, Rating, Comments)   
VALUES  
  (780, 'John Smith', 'john@fourthcoffee.com', 5,   
'The Mountain-200 Silver from AdventureWorks2008 Cycles meets and exceeds expectations. I enjoyed the smooth ride down the roads of Redmond');  
  
-- Given the full-text catalog for these tables is Adv_ft_ctlg,   
-- with change_tracking on so that the full-text indexes are updated automatically.  
WAITFOR DELAY '00:00:30';     
-- Wait 30 seconds to make sure that the full-text index gets updated.  
  
SELECT r.Comments, p.Name  
FROM Production.ProductReview AS r  
JOIN Production.Product AS p   
    ON r.ProductID = p.ProductID  
    AND r.ProductID = (SELECT ProductID  
FROM Production.ProductReview  
WHERE CONTAINS (Comments,   
    ' AdventureWorks2008 AND   
    Redmond AND   
    "Mountain-200 Silver" '));  
GO  
```  
  
### <a name="k-querying-on-a-document-property"></a>K. 查询文档属性  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 以下查询在 `Title` 表的 `Document` 列中搜索索引属性 `Production.Document`。 该查询仅返回 `Title` 属性包含字符串 `Maintenance`   `Repair` 的文档。  
  
> [!NOTE]  
>  要使属性搜索返回行，在编制索引过程中分析列的一个或多个筛选器必须提取指定的属性。 另外，必须配置指定表的全文索引以包含该属性。 有关详细信息，请参阅 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Document 
FROM Production.Document  
WHERE CONTAINS(PROPERTY(Document,'Title'), 'Maintenance OR Repair');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索入门](../../relational-databases/search/get-started-with-full-text-search.md)   
 [创建和管理全文索引目录](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [创建 FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT (Transact-SQL)](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [使用全文搜索查询](../../relational-databases/search/query-with-full-text-search.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 [创建全文搜索查询 (Visual Database Tools)](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

