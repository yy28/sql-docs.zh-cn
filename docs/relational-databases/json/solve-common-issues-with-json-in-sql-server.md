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
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: abae3fc5a3d8edab6e4b465ce4cae038e45222d0
ms.lasthandoff: 04/11/2017

---
# <a name="solve-common-issues-with-json-in-sql-server"></a>解决 SQL Server 中 JSON 的常见问题
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 此处可找到关于 SQL Server 中内置 JSON 支持的常见问题解答。  
 
## <a name="for-json-and-json-output"></a>FOR JSON 和 JSON 输出

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH 或 FOR JSON AUTO？  
 **问题。** 我需要在一个表上从简单的 SQL 查询创建 JSON 文本结果。 FOR JSON PATH 和 FOR JSON AUTO 生成相同的输出。 我应该使用这两个选项之中的哪一个？  
  
 **答案。** 请使用 FOR JSON PATH。 尽管 JSON 输出没有任何区别，但 AUTO 模式拥有一些其他的逻辑，可检查是否应嵌套列。 请将 PATH 作为默认选项。  

### <a name="create-a-nested-json-structure"></a>创建一个嵌套的 JSON 结构  
 **问题。** 我需要在同一级别上生成具有多个数组的复杂 JSON。 FOR JSON PATH 可以使用路径创建嵌套对象，FOR JSON AUTO 为每个表创建其他的嵌套级别。 这两个选项都不能够让我生成所需的输出。 我如何才能自定义现有选项不直接支持的 JSON 格式？  
  
 **答案。** 你可以通过将 FOR JSON 查询添加为返回 JSON 文本的列表达式来创建任何数据结构，或者通过使用 JSON_QUERY 函数手动创建 JSON，如下例所示。  
  
```tsql  
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
 **问题。** 我的 JSON 文本存储在一个表列中。 我想将它包含到 FOR JSON 的输出中。 FOR JSON 会转义 JSON 中的所有字符，因此我将会得到 JSON 字符串，而不是嵌套对象，如下例所示。  
  
```tsql  
SELECT 'Text' as myText, '{"day":23}' as myJson  
FOR JSON PATH  
```  
  
 此查询将生成以下输出。  
  
```json  
[{"myText":"Text","myJson":"{\"day\":23}"}]  
```  
  
 我如何才能防止此行为？ 我想让 `{"day":23}` 作为 JSON 对象而不是转义文本返回。  
  
 **答案。** 存储在文本列中的 JSON 或文字被当做文本处理。 它用双引号括起来并经过转义。 如果你想返回未转义的 JSON 对象，则必须将此列作为参数传递到 JSON_QUERY 函数，如下例所示。  
  
```tsql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 没有可选次要参数的 JSON_QUERY 仅将第一个参数作为结果返回。 由于 JSON_QUERY 返回了有效的 JSON，因此 FOR JSON 知道不需要对此结果进行转义。

### <a name="json-generated-with-the-withoutarraywrapper-clause-is-escaped-in-for-json-output"></a>使用 WITHOUT_ARRAY_WRAPPER 子句生成的 JSON 在 FOR JSON 输出中被转义  
 **问题。** 我正尝试通过使用 FOR JSON 和 WITHOUT_ARRAY_WRAPPER 选项设置列表达式的格式。  
  
```tsql  
SELECT 'Text' as myText,  
       (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 但 FOR JSON 查询返回的文本似乎被转义成了纯文本。 这种情况仅在指定了 WITHOUT_ARRAY_WRAPPER 的情况下才会发生。 为什么它不被视为 JSON 对象并以未转义的形式包含在结果中？  
  
 **答案。** 如果你指定了 WITHOUT_ARRAY_WRAPPER 选项，那么生成的 JSON 文本并不一定是有效的。 因此，外部 FOR JSON 会假定其为纯文本，并对字符串进行转移。 如果你确定该 JSON 输出是有效的，请用 JSON_QUERY 函数包装它，以将其提升为格式正确的 JSON，如下例所示。  
  
```tsql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>OPENJSON 和 JSON 输出

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>使用 OPENJSON 从 JSON 文本中返回嵌套的 JSON 子对象  
 **问题。** 我无法使用 OPENJSON 和显式架构打开包含标量值、对象和数组的复杂 JSON 对象数组。 当我在 WITH 子句中引用键时，仅返回了标量值。 对象和数组则返回为 NULL 值。 我如何提取 JSON 对象中的对象或数组？  
  
 **答案。** 如果你想将对象或数组作为列返回，请在列定义中使用 AS JSON 选项，如下例所示。  
  
```tsql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
             WITH ( scalar1 int,  
                          scalar2 datetime2,  
                          obj1 NVARCHAR(MAX) AS JSON,  
                          obj2 NVARCHAR(MAX) AS JSON,  
                          arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="use-openjson-instead-of-jsonvalue-to-return-long-text-values"></a>使用 OPENJSON 而不是 JSON_VALUE 返回长文本值  
 **问题。** 我在包含长文本的 JSON 文本中拥有描述键。 `JSON_VALUE(@json, '$.description')` 返回 NULL，而不是一个值。  
  
 **答案。** JSON_VALUE 旨在返回小的标量值。 通常此函数返回 NULL，而不是溢出错误。 如果你想返回更长的值，请使用支持 NVARCHAR(MAX) 值的 OPENJSON，如下例所示。  
  
```tsql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="use-openjson-instead-of-jsonvalue-to-handle-duplicate-keys"></a>使用 OPENJSON 而不是 JSON_VALUE 处理重复键  
 **问题。** 我的 JSON 文本中有重复的键。 JSON_VALUE 仅返回在该路径上找到的第一个键。 我如何返回名称相同的所有键？  
  
 **答案。** JSON 内置标量函数仅返回所引用对象的第一个匹配项。 如果需要多个键，请使用 OPENJSON 表值函数，如下例所示。  
  
```tsql  
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
 

