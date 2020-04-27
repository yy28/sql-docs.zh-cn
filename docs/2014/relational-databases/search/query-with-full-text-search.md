---
title: 使用全文搜索查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 280f4bc3c20fb65be24ace423f69982ad96bfbff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011104"
---
# <a name="query-with-full-text-search"></a>使用全文搜索查询
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文查询使用全文谓词（CONTAINS 和 FREETEXT）以及全文函数（CONTAINSTABLE 和 FREETEXTTABLE）来定义全文搜索。 它们支持复杂的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法，这种语法支持各种形式的查询词。 若要编写全文查询，必须了解何时以及如何使用这些谓词和函数。  
  
##  <a name="overview-of-the-full-text-predicates-contains-and-freetext"></a><a name="OV_ft_predicates"></a>全文谓词（CONTAINS 和 FREETEXT）概述  
 CONTAINS 和 FREETEXT 谓词返回 TRUE 或 FALSE 值。 它们只能用于指定选择条件，以确定给定的行是否与全文查询相匹配。 匹配的行在结果集中返回。 CONTAINS 和 FREETEXT 在 SELECT 语句的 WHERE 或 HAVING 子句中指定。 它们可以与任何其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 谓词（例如 LIKE 和 BETWEEN）结合使用。  
  
> [!NOTE]  
>  有关这些谓词的语法和参数的信息，请参阅[CONTAINS &#40;transact-sql&#41;](/sql/t-sql/queries/contains-transact-sql)和[FREETEXT &#40;transact-sql&#41;](/sql/t-sql/queries/freetext-transact-sql)。  
  
 当使用 CONTAINS 或 FREETEXT 时，可以指定搜索表中的单个列、一组列或所有列。 此外，还可以指定语言，以便给定的全文查询使用此语言的资源进行断字和词干分析、同义词库查找以及干扰词删除。  
  
 CONTAINS 和 FREETEXT 可用于搜索不同种类的匹配项，如下所示：  
  
-   使用 CONTAINS（或 CONTAINSTABLE）可搜索单个词和短语的精确或模糊（不太精确的）匹配项、在一定差别范围内的相近词或加权匹配项。 当使用 CONTAINS 时，必须指定至少一个搜索条件，该搜索条件须指定要搜索的文本以及确定匹配项的条件。  
  
     可以在搜索条件之间使用逻辑运算。 有关详细信息，请参阅本主题后面的[使用布尔运算符（AND、OR 和 NOT （在 CONTAINS 和 CONTAINSTABLE 中）](#Using_Boolean_Operators)。  
  
-   使用 FREETEXT（或 FREETEXTTABLE）可搜索与指定词、短语或句子（Freetext 字符串**）的含义相符但措辞不完全相同的匹配项。 只要在指定列的全文索引中找到任何搜索词或任何搜索词的任何形式，就会生成匹配项。  
  
 可以在 CONTAINS 或 FREETEXT 谓词中使用由四部分组成的名称对链接服务器上的目标表的全文索引列进行查询。 若要准备远程服务器以接收全文查询，请在远程服务器上的目标表和列上创建全文索引，然后将该远程服务器添加为链接服务器。  
  
> [!NOTE]  
>  当数据库兼容级别设置为100时， [OUTPUT 子句](/sql/t-sql/queries/output-clause-transact-sql)中不允许使用全文谓词。  
  
 
  
### <a name="examples"></a>示例  
  
#### <a name="a-using-contains-with-simple_term"></a>A. 将 CONTAINS 与 <简单词> 一起使用  
 下面的示例查找包含 `$80.99` 一词且价格为 `"Mountain"`的所有产品。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>B. 使用 FREETEXT 搜索包含指定字符值的单词  
 以下示例搜索包含与 vital、safety、components 相关的单词的所有文档。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="overview-of-the-full-text-functions-containstable-and-freetexttable"></a><a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a>全文函数（CONTAINSTABLE 和 FREETEXTTABLE）概述  
 像一般的表名一样，CONTAINSTABLE 和 FREETEXTTABLE 函数也可以在 SELECT 语句的 FROM 子句中进行引用。 它们返回与全文查询匹配的、包含零行、一行或多行的表。 返回的表只包含与该函数的全文搜索条件中指定的选择条件相匹配的基表的行。  
  
> [!NOTE]  
>  有关这些函数的语法和参数的信息，请参阅[CONTAINSTABLE &#40;transact-sql&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)和[FREETEXTTABLE &#40;transact-sql&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)。  
  
 使用这些函数之一的查询返回每一行的相关性排名值 (RANK) 和全文键 (KEY)，如下所示：  
  
-   KEY 列  
  
     KEY 列返回所返回行的唯一值。 可使用 KEY 列指定选择条件。  
  
-   RANK 列  
  
     RANK 列返回每一行的排名值 ** ，此值指示该行与选择条件相匹配的程度。 行中文本或文档的排名值越高，该行与给定的全文查询的相关性就越高。 请注意，不同行的排名可以相同。 可以通过指定可选的 top_n_by_rank** 参数限制返回的匹配项的数目。 有关详细信息，请参阅 [使用 RANK 限制搜索结果](limit-search-results-with-rank.md)。  
  
 当使用这些函数之一时，必须指定要进行全文搜索的基表。 与谓词一样，可以指定搜索表中的单个列、一组列或所有列；此外，还可以指定给定的全文查询将使用的资源的语言。  
  
 CONTAINSTABLE 用来搜索的匹配项的种类与 CONTAINS 相同，FREETEXTTABLE 用来搜索的匹配项的种类与 FREETEXT 相同。 有关详细信息，请参阅本主题前面的 [全文谓词（CONTAINS 和 FREETEXT）概述](#OV_ft_predicates)。 在运行使用 CONTAINSTABLE 和 FREETEXTTABLE 函数的查询时，必须显式联接与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基表中的行一起返回的行。  
  
 通常，需要将 CONTAINSTABLE 或 FREETEXTTABLE 的结果与基表联接。 在这样的情况下，需要知道唯一键列名称。 该列出现在每个启用全文的表中，用于强制表的唯一行（“唯一键列”**）。 有关详细信息，请参阅 [管理全文索引](../indexes/indexes.md)。  
  
 
  
### <a name="examples"></a>示例  
  
#### <a name="a-using-containstable"></a>A. 使用 CONTAINSTABLE  
 对于在词“light”或“lightweight”附近包含词“aluminum”的 **Description** 列，以下示例返回其所有产品的说明 ID 和说明。 仅返回排名值为 2 或更高的行。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>B. 使用 FREETEXTTABLE  
 以下示例扩展了 FREETEXTTABLE 查询，以便首先返回排名最高的行，然后将每一行的排名添加到选择列表中。 若要指定查询，必须知道**ProductDescriptionID**是`ProductDescription`表的唯一键列。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 下面是同一查询的扩展查询，此查询只返回排名值为 10 或更高的行：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 
  
##  <a name="using-boolean-operators---and-or-and-not---in-contains-and-containstable"></a><a name="Using_Boolean_Operators"></a>使用布尔运算符（AND、OR 和 NOT in CONTAINS 和 CONTAINSTABLE）  
 CONTAINS 谓词和 CONTAINSTABLE 函数使用相同的搜索条件。 两者都支持使用布尔运算符（AND、OR 和 NOT）来合并多个搜索词，以执行逻辑运算。 例如，可以使用 AND 查找既包含“latte”又包含“New York-style bagel”的行。 例如，可以使用 AND NOT 查找包含“bagel”但不包含“cream cheese”的行。  
  
> [!NOTE]  
>  相反，FREETEXT 和 FREETEXTTABLE 将布尔值项视为词来搜索。  
  
 有关将 CONTAINS 与其他使用逻辑运算符 AND、OR 和 NOT 的谓词结合使用的信息，请参阅 [搜索条件 (Transact-SQL)](/sql/t-sql/queries/search-condition-transact-sql)。  
  
### <a name="example"></a>示例  
 下面的示例使用 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 数据库的 ProductDescription 表。 该查询使用 CONTAINS 谓词搜索说明 ID 不等于 5 并且既包含词“Aluminum”又包含词“spindle”的说明。 该搜索条件使用 AND 布尔运算符。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="additional-considerations-for-full-text-queries"></a><a name="Additional_Considerations"></a>全文查询的其他注意事项  
 编写全文查询时还应考虑下列事项:  
  
-   LANGUAGE 选项  
  
     许多查询词在很大程度上依赖于断字符行为。 为了确保您使用的是正确的断字符（和词干分析器）以及同义词库文件，我们建议您指定 LANGUAGE 选项。 有关详细信息，请参阅 [创建全文索引时选择语言](choose-a-language-when-creating-a-full-text-index.md)。  
  
-   非索引字  
  
     当定义全文查询时，全文引擎会去除搜索条件中的非索引字（也称为干扰词）。 非索引字是可能经常出现但通常对搜索特定文本没有帮助的词，如“a”、“and”、“is”或“the”。 非索引字在非索引字表中列出。 每个全文索引都与一个特定的非索引字表相关联，该非索引字表决定在进行索引时省略查询或索引中的哪些非索引字。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](full-text-search.md)。  
  
-   同义词库  
  
     FREETEXT 和 FREETEXTTABLE 查询默认情况下使用同义词库。 CONTAINS 和 CONTAINSTABLE 支持可选的 THESAURUS 参数。  
  
-   事例敏感性  
  
     全文搜索查询不区分大小写。 但是，在日语中，有许多表示语音的拼字法，其中拼字规范化这一概念与不区分大小写类似，如 kana = 不区分。 这种拼字规范化不受支持。  
  

  
##  <a name="querying-varbinarymax-and-xml-columns"></a><a name="varbinary"></a>查询 varbinary （max）和 xml 列  
 如果 `varbinary(max)`、`varbinary` 或 `xml` 列是全文索引列，则与任何其他全文索引列一样，可以使用全文谓词（CONTAINS 和 FREETEXT）以及函数（CONTAINSTABLE 和 FREETEXTTABLE）来查询该列。  
  
> [!IMPORTANT]  
>  全文搜索还可以用于图像列。 然而，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将来的版本中将删除 `image` 数据类型。 请避免在新的开发工作中使用此数据类型，并计划修改当前使用此数据类型的应用程序。 请改用 `varbinary(max)` 数据类型。  
  
### <a name="varbinarymax-or-varbinary-data"></a>varbinary(max) 或 varbinary 数据  
 单个 `varbinary(max)` 或 `varbinary` 列可以存储多种类型的文档。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持安装了相应筛选器并且在操作系统中可用的任何文档类型。 每个文档的文档类型由该文档的文件扩展名标识。 例如，对于 .doc 文件扩展名，全文搜索将使用支持 Microsoft Word 文档的筛选器。 有关可用文档类型的列表，请查询 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) 目录视图。  
  
 请注意，全文引擎可以利用操作系统中安装的现有筛选器。 在您可以使用操作系统筛选器、断字符和词干分析器之前，您必须将它们加载到服务器实例中，如下所示：  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 若要对 `varbinary(max)` 列创建全文索引，全文引擎需要访问 `varbinary(max)` 列中文档的文件扩展名。 此信息必须存储在一个称为“类型列”的表列中，该列必须与全文索引中的 `varbinary(max)` 列相关联。 在为文档创建索引时，全文引擎将使用类型列中的文件扩展名来标识要使用的筛选器。  
  
 
  
### <a name="xml-data"></a>xml 数据  
 `xml` 数据类型列仅存储 XML 文档和片段，并且只有 XML 筛选器用于此类文档。 因此，无需类型列。 在 `xml` 列上，全文索引会为 XML 元素的内容创建索引，但会忽略 XML 标记。 不为数值的属性值都会进行全文索引。 元素标记用作标记边界。 支持包含多种语言的格式正确的 XML 或 HTML 文档和片段。  
  
 有关对`xml`列进行查询的详细信息，请参阅对[XML 列使用全文搜索](../xml/use-full-text-search-with-xml-columns.md)。  
  
 
  
##  <a name="supported-forms-of-query-terms"></a><a name="supported"></a>支持的查询词形式  
 此部分总结了为全文谓词和行集值函数为每种查询提供的支持。  
  
> [!NOTE]  
>  有关给定查询词的语法，请单击下表“支持”**** 列中的相应链接。  
  
|查询词形式|说明|支持的服务|  
|----------------------|-----------------|------------------|  
|一个或多个特定的词或短语（“简单词”**）|在全文搜索中，词（或“标记”**）是其边界由相应的断字符标识、遵循指定语言的语言规则的字符串。 有效的短语由多个词组成，词之间可以有标点符号也可以没有标点符号。<br /><br /> 例如，"新月形面包" 是一个词，"caf？" au lait "是一个短语。 这样的词和短语称为“简单词”。<br /><br /> 有关详细信息，请参阅本主题后面的 [搜索特定的词或短语（简单词）](#Simple_Term)。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 查找短语的完全匹配项。<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) 和 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 将短语拆分为几个词。|  
|以指定文本开头的词或短语（“前缀词”**）|前缀词指附加到一个词的前面以生成一个派生词或变形的字符串。<br /><br /> 对于单个前缀词，以指定词开头的任何词将是结果集的一部分。 例如，词“auto*”与“automatic”、“automobile”等匹配。<br /><br /> 如果是短语，则该短语内的每个词都被看作是一个前缀。 例如，词“auto tran\*”与“automatic transmission”和“automobile transducer”匹配，但与“automatic motor transmission”不匹配。<br /><br /> 有关详细信息，请参阅本主题后面的 [执行前缀搜索（前缀词）](#Prefix_Term)。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|特定词的变形形式（*生成词-变形*）|变形是动词的不同时态和语态形式，或是名词的单数和复数形式。 例如，搜索词“drive”的变形。 如果表中不同的行包含词“drive”、“drives”、“drove”、“driving”和“driven”，则这些词都会出现在结果集中，原因是它们每一个都可以从词 drive 变形而来。<br /><br /> 有关详细信息，请参阅本主题后面的 [搜索特定词的变形（派生词）](#Inflectional_Generation_Term)。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql)和[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)在默认情况下查找所有指定词的变形术语。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 支持可选的 INFLECTIONAL 参数。|  
|特定词的同义词形式（*生成词-同义词库*）|同义词库为词定义用户指定的同义词。 例如，如果将项“{car, automobile, truck, van}”添加到同义词库，则可以搜索单词“car”的同义词库形式。 由于这些单词中的每一个都属于包含单词“car”的同义词扩展集，因此在所查询的表中所有包括单词“automobile”、“truck”、“van”或“car”的行都会出现在结果集中。<br /><br /> 有关同义词库文件的结构的信息，请参阅 [配置和管理全文搜索同义词库文件](configure-and-manage-thesaurus-files-for-full-text-search.md)。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql)和[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)在默认情况下使用同义词库。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql)和[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)支持可选的同义词库参数。|  
|与另一个词或短语邻近的词或短语（“邻近词”**）|邻近词表示相邻的词或短语。还可以指定在第一个搜索词与最后一个搜索之间最多可以有几个非搜索词。 此外，可以以任意顺序或您指定的顺序搜索词或短语。<br /><br /> 例如，查找词“ice”与“hockey”邻近或短语“ice skating”与“ice hockey”邻近的行。<br /><br /> 有关详细信息，请参阅 [使用 NEAR 搜索与另一个词邻近的词](search-for-words-close-to-another-word-with-near.md)。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|使用加权值的词或短语（“加权词”**）|加权值指示一组词和短语中的每个词和短语的重要程度。 加权值的最低值是 0.0，最高值是 1.0。<br /><br /> 例如，在某个搜索多个词条的查询中，可以为每个搜索单词指定一个加权值，用于指示它相对于搜索条件中其他单词的重要性。 此查询类型的结果将按指定给搜索单词的相对权重首先返回最相关的行。 结果集由包含任何指定词（或它们之间的内容）的文档或行组成；但是，由于与不同搜索词关联的加权值的不同，某些结果将被视为比其他结果更相关。<br /><br /> 有关详细信息，请参阅本主题后面的 [使用加权值搜索词或短语（加权词）](#Weighted_Term)。|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="searching-for-specific-word-or-phrase-simple-term"></a><a name="Simple_Term"></a>搜索特定的词或短语（简单词）  
 可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)或 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 在表中搜索特定短语。 例如，如果要在 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 数据库的 `ProductReview` 表中进行搜索，以查找关于某种产品的包含“learning curve”短语的所有注释，可以使用 CONTAINS 谓词，如下所示：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 搜索条件（在本例中是“learning curve”）可以很复杂，可由一项或多项组成。  
  
 
  
###  <a name="performing-prefix-searches-prefix-term"></a><a name="Prefix_Term"></a>执行前缀搜索（前缀词）  
 可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 或 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 来搜索具有指定前缀的词或短语。 将返回列中所有包含以指定前缀开头的文本的项。 例如，要搜索包含前缀 `top`- 的所有行，如 `top``ple`、 `top``ping`和 `top`。 该查询如下所示：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 将会返回所有与星号 (*) 之前指定的文本相匹配的文本。 如果未在文本和星号前后加上双引号标记（如 `CONTAINS (DESCRIPTION, 'top*')`），则全文搜索将不把星号当作通配符。  
  
 当前缀词是短语时，组成该短语的每个标记均被看作是单独的前缀词。 将返回包含以这些前缀词开头的词的所有行。 例如，前缀词“light bread*”将查找带有“light breaded”、“lightly breaded”或“light bread”文本的行，但不会返回“lightly toasted bread”。  
  
 
  
###  <a name="searching-for-inflectional-forms-of-a-specific-word-generation-term"></a><a name="Inflectional_Generation_Term"></a>搜索特定词的变形形式（生成词）  
 可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)或 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 搜索动词的所有不同时态和语态形式或搜索名词的单数和复数形式（变形搜索）或者搜索特定词的同义词形式（同义词库搜索）。  
  
 以下示例在 `Comments` 数据库的 `ProductReview` 表的 `AdventureWorks` 列搜索“foot”的任意变形（“foot”、“feet”等）：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  全文搜索使用词干分析器，它允许您搜索某个动词的不同时态和语态形式，或搜索某个名词的单数和复数形式。 有关词干分析器的详细信息，请参阅 [配置和管理断字符和词干分析器以便搜索](configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  

  
###  <a name="searching-for-words-or-phrases-using-weighted-values-weighted-term"></a><a name="Weighted_Term"></a>使用加权值搜索词或短语（加权词）  
 您可以使用 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 来搜索词或短语并指定加权值。 加权值用介于 0.0 到 1.0 之间的一个数字来表示，用于指示一组词和短语中的每个词和短语的重要程度。 加权值的最低值是 0.0，最高值是 1.0。  
  
 下例所示的查询使用加权值搜索所有符合以下条件的客户地址：地址中任何以字符串“Bay”开头的文本包含“Street”或“View”。 在结果中，对那些包含较多指定词的行赋予较高的排名。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 加权词可以与任意简单词、前缀词、派生词或邻近词一起使用。  
  

  
##  <a name="viewing-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a><a name="tokens"></a>查看断字符、同义词库和非索引字表组合的词汇切分结果  
 对查询字符串输入应用给定的断字符、同义词库和非索引字表组合后，可以使用 **sys.dm_fts_parser** 动态管理视图查看词汇切分结果。 有关详细信息，请参阅[sys.dm_fts_parser (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)。  
  
 
  
## <a name="see-also"></a>另请参阅  
 [包含 &#40;Transact-sql&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE (Transact-SQL)](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT (Transact-SQL)](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE (Transact-SQL)](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [创建全文搜索查询 (Visual Database Tools)](../../ssms/visual-db-tools/visual-database-tools.md)   
 [改进全文查询的性能](improve-the-performance-of-full-text-queries.md)  
  
  
