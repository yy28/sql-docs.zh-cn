---
title: "解决 SQL Server 中 JSON 的常见问题 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 94435e9fb466887a00c8d22076f229481a83f280
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="solve-common-issues-with-json-in-sql-server"></a>解决 SQL Server 中 JSON 的常见问题
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 此处可找到关于 SQL Server 中内置 JSON 支持的常见问题解答。  
 
## <a name="for-json-and-json-output"></a>FOR JSON 和 JSON 输出

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH 或 FOR JSON AUTO？  
 **问题。** 我想要从简单的 SQL 查询单个表上创建 JSON 文本结果。 FOR JSON PATH 和 FOR JSON AUTO 生成相同的输出。 我应该使用这两个选项之中的哪一个？  
  
 **答案。** 请使用 FOR JSON PATH。 尽管没有任何区别在 JSON 输出中的，AUTO 模式将适用一些其他的逻辑，可检查是否应嵌套列。 请将 PATH 作为默认选项。  

### <a name="create-a-nested-json-structure"></a>创建一个嵌套的 JSON 结构  
 **问题。** 我想要生成在同一级别上的多个数组具有复杂 JSON。 FOR JSON PATH 可以使用路径创建嵌套对象，FOR JSON AUTO 为每个表创建其他的嵌套级别。 既不这两个选项之一能够让我生成我想要的输出。 我如何才能自定义现有选项不直接支持的 JSON 格式？  
  
 **答案。** 可以通过将 FOR JSON 查询添加为返回 JSON 文本的列表达式来创建任何数据结构。 你还可以通过使用 JSON_QUERY 函数手动创建 JSON。 下面的示例演示这些技术。  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
列表达式中 FOR JSON 查询或 JSON_QUERY 函数的每个结果的格式都为单独嵌套的 JSON 子对象，并且都包含在主要结果中。  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>防止 FOR JSON 输出中的 JSON 被双转义  
 **问题。** 我的 JSON 文本存储在一个表列中。 我想将它包含到 FOR JSON 的输出中。 但 FOR JSON 会转义 JSON 中的所有字符，因此我将获取 JSON 字符串而不是嵌套对象，如下面的示例中所示。  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 此查询将生成以下输出。  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 我如何才能防止此行为？ 我想让 `{"day":23}` 作为 JSON 对象而不是转义文本返回。  
  
 **答案。** 存储在文本列中的 JSON 或文字被当做文本处理。 也就是说，它具有用双引号括起来并经过转义。 如果你想要返回的非转义的 JSON 对象，JSON 列作为参数传递到 JSON_QUERY 函数，如下面的示例中所示。  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 没有可选次要参数的 JSON_QUERY 仅将第一个参数作为结果返回。 由于 JSON_QUERY 始终返回有效的 JSON，因此 FOR JSON 知道此结果不需要对其进行转义。

### <a name="json-generated-with-the-withoutarraywrapper-clause-is-escaped-in-for-json-output"></a>使用 WITHOUT_ARRAY_WRAPPER 子句生成的 JSON 在 FOR JSON 输出中被转义  
 **问题。** 我正尝试通过使用 FOR JSON 和 WITHOUT_ARRAY_WRAPPER 选项设置列表达式的格式。  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 但 FOR JSON 查询返回的文本似乎被转义成了纯文本。 这种情况仅在指定了 WITHOUT_ARRAY_WRAPPER 的情况下才会发生。 为什么它不被视为 JSON 对象并以未转义的形式包含在结果中？  
  
 **答案。** 如果指定`WITHOUT_ARRAY_WRAPPER`中内部选项`FOR JSON`，生成的 JSON 文本并不一定是有效的 JSON。 因此外部`FOR JSON`假定其为纯文本，并对字符串进行转移。 如果确定 JSON 输出是有效，则将其与包装`JSON_QUERY`函数要提升它到正确格式化 JSON，如下面的示例中所示。  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>OPENJSON 和 JSON 输出

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>使用 OPENJSON 从 JSON 文本中返回嵌套的 JSON 子对象  
 **问题。** 我无法打开包含这两个标量值、 对象和数组使用 OPENJSON 和显式架构的复杂 JSON 对象数组。 当我在 WITH 子句中引用键时，仅返回了标量值。 对象和数组则返回为 NULL 值。 作为 JSON 对象，如何可以提取对象或数组？  
  
 **答案。** 如果你想要返回的对象或数组作为列，在列定义中，使用 AS JSON 选项在下面的示例所示。  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-jsonvalue"></a>返回用 OPENJSON 而不是 JSON_VALUE 长文本值
 **问题。** 我在包含长文本的 JSON 文本中拥有描述键。 `JSON_VALUE(@json, '$.description')` 返回 NULL，而不是一个值。  
  
 **答案。** JSON_VALUE 旨在返回小的标量值。 通常此函数返回 NULL，而不是溢出错误。 如果你想返回更长的值，请使用支持 NVARCHAR(MAX) 值的 OPENJSON，如下例所示。  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-jsonvalue"></a>用 OPENJSON 而不是 JSON_VALUE 句柄重复键
 **问题。** 我的 JSON 文本中有重复的键。 JSON_VALUE 仅返回在该路径上找到的第一个键。 我如何返回名称相同的所有键？  
  
 **答案。** 内置的 JSON 标量函数返回仅引用的对象的第一个匹配项。 如果需要多个键，请使用 OPENJSON 表值函数，如下例所示。  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON 要求兼容性级别 130  
 **问题。** 我正尝试在 SQL Server 2016 中运行 OPENJSON，但收到以下错误。  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **答案。** OPENJSON 函数仅在兼容性级别 130 下可用。 如果你的 DB 兼容性级别低于 130，则会隐藏 OPENJSON。 其他 JSON 函数在所有兼容性级别均可用。  
 
## <a name="other-questions"></a>其他问题

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>引用 JSON 文本中中包含非字母数字字符的键  
 **问题。** 我的 JSON 文本中有包含非字母数字字符的键。 我如何引用这些属性？  
  
 **答案。** 必须在 JSON 路径中用引号将它们括起来。 例如， `JSON_VALUE(@json, '$."$info"."First Name".value')`。
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。

