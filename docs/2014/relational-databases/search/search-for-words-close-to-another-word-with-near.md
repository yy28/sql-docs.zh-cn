---
title: 使用 NEAR 搜索与另一个词邻近的词 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8c2d187ea3ed951ac6f17eb4babc5f4f77451d4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003995"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>使用 NEAR 搜索与另一个词邻近的词
  可以在 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 谓词或 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 函数中使用邻近词 (NEAR) 来搜索相互邻近的字词或短语。 还可以指定在第一个搜索词与最后一个搜索之间最多可以有几个非搜索词。 此外，可以按任意顺序或您指定的顺序搜索词或短语。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]同时支持以前的[通用邻近词](#Generic_NEAR)（现已不推荐使用）和[自定义邻近词](#Custom_NEAR)，这是中的新术语 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 。  
  
##  <a name="the-custom-proximity-term"></a><a name="Custom_NEAR"></a>自定义邻近词  
 自定义邻近词引入了下列新功能：  
  
-   可以指定第一个搜索词与最后一个搜索词之间存在的非搜索词的最大数目或最大距离**，以作为构成匹配项的条件。  
  
-   如果指定词的最大数目，还可以指定搜索词必须以指定顺序出现在匹配项中。  
  
 若要成为一个符合条件的匹配项，文本字符串必须满足以下条件：  
  
-   以其中一个指定搜索词开头，以其中另一个指定搜索词结尾。  
  
-   包含所有指定的搜索词。  
  
-   如果指定了最大距离，在第一个搜索词和最后一个搜索词之间出现的非搜索词（包括非索引字）的数目必须少于或等于最大距离。  
  
 基本语法为：  
  
 NEAR (  
  
 {  
  
 *search_term* [,.。。*n* ]  
  
 |  
  
 （*search_term* [,.。。*n* ]） [，<maximum_distance> [，<match_order>]]  
  
 }  
  
 )  
  
> [!NOTE]  
>  有关 <custom_proximity_term> 语法的详细信息，请参阅 [CONTAINS (Transact-SQL)](/sql/t-sql/queries/contains-transact-sql)。  
  
 例如，可以搜索距离“Smith”两个词以内的“John”，如下所示：  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 匹配的字符串的一些示例包括“`John Jacob Smith`”和“`Smith, John`”。 字符串“`John Jones knows Fred Smith`”中间隔有三个非搜索词，因此它不是一个匹配项。  
  
 若要求查找指定顺序的词，可以将上面的邻近词示例更改为 `NEAR((John, Smith),2, TRUE).` 。这样将搜索距离“`John`”两个词以内的“`Smith`”并且“`John`”必须在“`Smith`”之前。 在从左向右阅读的语言（如英语）中，匹配的字符串的示例有“`John Jacob Smith`”。  
  
 请注意，对于从右向左阅读的语言（例如阿拉伯语或希伯来语），全文引擎会以相反的顺序应用指定词。 此外， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的对象资源管理器会自动颠倒从右到左语言中指定的文字显示顺序。  
  
> [!NOTE]  
>   有关详细信息，请参阅本主题后面的“[有关邻近搜索的更多考虑因素](#Additional_Considerations)”。  
  
### <a name="how-maximum-distance-is-measured"></a>最大距离的测量方式  
 特定的最大距离（例如 10 或 25）决定在给定字符串的第一个搜索词与最后一个搜索词之间可以出现多少个非搜索词（包括非索引字）。 例如， `NEAR((dogs, cats, "hunting mice"), 3)` 将返回以下行，其中非搜索词的总数为 3（“`enjoy`”、“`but`”和“`avoid`”)：  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 相同的邻近词将不返回以下行，因为最大距离超过了四个非搜索词（“`enjoy`”、“`but`”、“`usually`”和“`avoid`”）：  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### <a name="combining-a-custom-proximity-term-with-other-terms"></a>将自定义邻近词与其他词组合使用  
 可以将自定义邻近词与一些其他词组合使用。 可以使用 AND (&), OR (|) 或 AND NOT (&!) 将一个自定义邻近词与另一个自定义邻近词、简单词或前缀词组合使用。 例如：  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 例如，  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 不能将自定义邻近词与通用邻近词（*term1* NEAR *term2*）、生成字词（ISABOUT ...）或加权术语（FORMSOF ...）组合在一起。  
  
### <a name="example-using-the-custom-proximity-term"></a>示例：使用自定义邻近词  
 以下示例在 `Production.Document` 示例数据库的 `AdventureWorks2012` 表中搜索包含与字词“bracket”在同一文档中的字词“reflector”的所有文档摘要。  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  

  
##  <a name="additional-considerations-for-proximity-searches"></a><a name="Additional_Considerations"></a>邻近搜索的其他注意事项  
 本节讨论了对通用邻近搜索和自定义邻近搜索都有影响的考虑因素：  
  
-   搜索词的重叠匹配项  
  
     所有邻近搜索始终都仅查找非重叠匹配项。 搜索词的重叠匹配项永远不会符合匹配项的条件。 例如，请考虑以下邻近词，它按照此顺序搜索“`A`”和“`AA`”，并且最大距离为两个词：  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     可能的匹配项是“`AAA`”、“`A.AA`”和“`A..AA`”。 仅包含“`AA`”的行将不匹配。  
  
    > [!NOTE]  
    >  可以指定重叠的词，例如 `NEAR("mountain bike", "bike trails")` 或 `(NEAR(comfort*, comfortable), 5)`。 指定重叠词会增加查询的复杂性，这是因为增加了可能的匹配项排列。 如果指定了大量这样的重叠词，查询可能会耗尽资源并失败。 如果发生这种情况，请简化查询，然后重试。  
  
-   通用 NEAR 和自定义 NEAR（无论是否指定最大距离）都指示词之间的逻辑距离，而不是词之间的绝对距离间。 例如，某一段落内其他短语或句子中的字词被视为距离远于同一短语或句子中的字词，而与其实际临近情况无关，因为假定它们是不相关的。 同样，不同段落中的字词被视为距离更远。 如果一个匹配项包含一个句子、一个段落或一个章节，用于文档排名的差距将分别提高 8、128 或 1024。  
  
-   邻近词通过 CONTAINSTABLE 函数对排名的影响  
  
     当 NEAR 在 CONTAINSTABLE 函数中使用时，文档中相对于文档长度的匹配项数以及每个匹配项中第一个与最后一个搜索词之间的距离会影响每个文档的排名。 对于通用邻近词，如果匹配的搜索词之间相隔的距离 > 50 个逻辑词，则对文档返回的排名为 0。 对于没有指定一个整数作为最大距离的自定义邻近词，只有其包含的匹配项的相隔距离 > 100 个逻辑词时，文档才会得到 0 排名。 有关自定义邻近搜索排名的详细信息，请参阅 [Limit Search Results with RANK](limit-search-results-with-rank.md)。  
  
-   **transform noise words** 服务器选项  
  
     如果在邻近搜索中指定了非索引字，则 **transform noise words** 的值会影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理非索引字的方式。 有关详细信息，请参阅 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。  
  

  
##  <a name="the-deprecated-generic-proximity-term"></a><a name="Generic_NEAR"></a>不推荐使用的通用邻近词  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我们建议您使用 [自定义邻近词](#Custom_NEAR)。  
  
 通用邻近词表明指定的搜索词必须全部出现在一个文档中匹配项才能返回，而与搜索词之间非搜索词的数目（距离**）无关。 基本语法为：  
  
 { *search_term* {NEAR | ~} *search_term* }[ ,...*n* ]  
  
 例如，在下面的示例中，单词“fox”和“chicken”必须都出现才能产生一个匹配项，不管它们的出现顺序如何：  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  有关 <generic_proximity_term> 语法的信息，请参阅 [CONTAINS (Transact-SQL)](/sql/t-sql/queries/contains-transact-sql)。  
  
  有关详细信息，请参阅本主题后面的“[有关邻近搜索的更多考虑因素](#Additional_Considerations)”。  
  
### <a name="combining-a-generic-proximity-term-with-other-terms"></a>将通用邻近词与其他词组合使用  
 可以使用 AND (&), OR (|) 或 AND NOT (&!) 将一个通用邻近词与另一个通用邻近词、简单词或前缀词组合使用。 例如：  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 不能将通用邻近词与自定义邻近词（如 `NEAR((term1,term2),5)` 加权术语（ISABOUT）或代词（FORMSOF ...））组合。  
  
### <a name="example-using-the-generic-proximity-term"></a>示例： 使用通用邻近词  
 下面的示例使用通用邻近词在一个有字词“bracket”的文档中搜索字词“reflector”。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 注意，也可以在 CONTAINSTABLE 中反转词条，所得到的结果相同：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 可以用字符 ~ 来代替前面查询中的 NEAR 关键字，其结果是一样的：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 可以在搜索条件中指定两个以上的词或短语。 例如，可以编写：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 这意味着“reflector”必须与“bracket”在同一文档中，“bracket”必须与“installation”在同一文档中。  
  

  
## <a name="see-also"></a>另请参阅  
 [CONTAINSTABLE (Transact-SQL)](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [使用全文搜索查询](query-with-full-text-search.md)   
 [CONTAINS (Transact-SQL)](/sql/t-sql/queries/contains-transact-sql)  
  
  
