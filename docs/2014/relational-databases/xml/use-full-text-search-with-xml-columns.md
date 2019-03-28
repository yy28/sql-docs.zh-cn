---
title: 对 XML 列使用全文搜索 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 897002d437dcee8a6c64750f964c957c18a077f3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530899"
---
# <a name="use-full-text-search-with-xml-columns"></a>对 XML 列使用全文搜索
  您可以对 XML 列创建全文索引，这种索引对 XML 值的内容进行索引，但忽略 XML 标记。 元素标记用作标记边界。 将对以下项进行索引：  
  
-   XML 元素的内容。  
  
-   仅限顶级元素的 XML 属性的内容，除非这些值是数值。  
  
 如有可能，可以按如下方式将全文搜索与 XML 索引结合起来：  
  
1.  首先，使用 SQL 全文搜索筛选感兴趣的 XML 值。  
  
2.  然后，查询那些使用 XML 列的 XML 索引的 XML 值。  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>例如：结合使用全文搜索服务和 XML 查询  
 对 XML 列创建了全文索引后，下面的查询将检查 XML 值是否在书的标题中包含“custom”一词：  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 **contains()** 方法使用全文索引来将文档中任何位置包含“custom”一词的 XML 值组合为一个子集。 **exist()** 子句确保“custom”一词出现在书的标题中。  
  
 使用 **contains()** 的全文搜索与 XQuery **contains()** 具有不同语义。 后者是子字符串匹配，前者是使用词干匹配的标记匹配。 因此，如果搜索标题中包含“run”的字符串，则匹配结果将包括“run”、“runs”和“running”，因为同时满足全文 **contains()** 和 Xquery **contains()** 。 但是，查询不匹配标题中的“customizable”一词，因为全文 **contains()** 失败，但满足 Xquery **contains()** 。 通常，对于纯子字符串匹配，应删除全文 **contains()** 子句。  
  
 此外，全文搜索使用词干匹配，而 XQuery **contains()** 是文字匹配。 这一区别在下一个示例中进行说明。  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>例如：全文搜索使用词干匹配的 XML 值  
 通常不能消除上一个示例中执行的 XQuery **contains()** 检查。 请看下面的查询：  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 因为使用了词干匹配，所以文档中的“ran”一词匹配搜索条件。 此外，不通过使用 XQuery 来检查搜索上下文。  
  
 当通过使用全文索引的 AXSD 将 XML 分解为关系列时，对 XML 视图执行的 XPath 查询不对基础表执行全文搜索。  
  
## <a name="see-also"></a>请参阅  
 [XML 索引 (SQL Server)](xml-indexes-sql-server.md)  
  
  
