---
title: "STRING_AGG (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf74698e9e61f456726b1e6a62126a8d78a09777
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

连接字符串表达式的值，并将它们之间的分隔符值。 不在字符串的末尾添加分隔符。
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>参数 

*分隔符*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的`NVARCHAR`或`VARCHAR`类型用作分隔符的串联字符串。 它可以是文本或变量。 

*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何类型。 表达式都转换为`NVARCHAR`或`VARCHAR`期间串联的类型。 非字符串类型转换为`NVARCHAR`类型。


< order_clause >   
（可选） 指定使用的串联结果的顺序`WITHIN GROUP`子句：
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
< order_by_expression_list >   
 
  将出现的非常量[表达式](../../t-sql/language-elements/expressions-transact-sql.md)了可以用于对结果进行排序。 只有一个`order_by_expression`允许每个查询。 默认的排序顺序为升序。   
  

## <a name="return-types"></a>返回类型 

返回类型是依赖于第一个自变量 （表达式）。 如果输入自变量是字符串类型 (`NVARCHAR`， `VARCHAR`)，结果类型将是与输入类型相同。 下表列出了自动转换：  

|输入的表达式类型 |结果 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR (1...4000) |NVARCHAR （4000) |
|VARCHAR (1...8000) |VARCHAR （8000) |
|int、 bigint、 smallint、 tinyint、 numeric、 float、 real、 位、 小数、 smallmoney、 money、 datetime、 datetime2， |NVARCHAR （4000) |


## <a name="remarks"></a>注释  
 
`STRING_AGG`聚合采用行中的所有表达式，并将它们连接到单个字符串。 表达式值已隐式转换为字符串类型，然后串联。 隐式转换为字符串的过程遵循现有的数据类型转换规则。 有关数据类型转换的详细信息，请参阅[CAST 和 CONVERT (TRANSACT-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。 

如果输入的表达式为类型`VARCHAR`，分隔符不能是类型`NVARCHAR`。 

将忽略 null 值，而且不会添加相应的分隔符。 若要返回 null 值的占位符，使用`ISNULL`函数示例 B.中所示

`STRING_AGG`只在任何兼容级别可用。


## <a name="examples"></a>示例 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. 生成名称的列表中新行分隔 
下面的示例生成的名称在一个结果单元格，以回车分隔的列表。
```tsql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`在中找到值`name`单元格不会返回结果中。   
> [!NOTE]  
>  如果使用 Management Studio 查询编辑器中，**结果显示为网格**选项不能实现回车。 切换到**结果显示为文本**才能看到结果正确设置。   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. 生成的名称与不包含 NULL 值的以逗号分隔的列表   
下面的示例使用 n/A 替换 null 值，并返回名称以单个结果单元格中的逗号分隔。  
```tsql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|Csv | 
|--- |
|John、 n/A、 Mike、 Peter、 n/A、 n/A、 Alice，Bob |  


### <a name="c-generate-comma-separated-values"></a>C. 生成逗号分隔值 

```tsql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|名称 | 
|--- |
|Ken Sánchez (年 2 月 8日 2003 12:00 AM) <br />Terri Duffy (2002 年 2 月 24日 12:00 AM) <br />Roberto Tamburello （5 2001 年 12 月 12:00 AM） <br />Rob Walters （29 2001 年 12 月 12:00 AM） <br />... |

> [!NOTE]  
>  如果使用 Management Studio 查询编辑器中，**结果显示为网格**选项不能实现回车。 切换到**结果显示为文本**才能看到结果正确设置。   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. 返回包含相关标记的新闻文章 

文章和标记分为不同的表。 开发人员想要返回每个与所有关联的标记每个项目的一行。 使用以下查询： 
```tsql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |标记 |
|--- |--- |--- |
|172 |轮询指示关闭选举结果 |政治、 轮询、 市/县 council | 
|176 |新高速公路希望减少拥塞 |NULL |
|177 |Dogs 继续要比 cats 更受欢迎 |轮询动物| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. 生成每个城镇电子的邮件列表

下面的查询查找员工的电子邮件地址，并按市分别有对其进行分组： 
```tsql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|镇 |电子邮件 |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

在列可以直接使用，以向组在某些特定城镇工作的人员发送电子邮件的电子邮件中返回电子邮件。 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 生成的每个市分别有电子邮件已排序的列表   
   
与前面的示例类似，下面的查询查找员工的电子邮件地址、 按镇，对其进行分组并按字母顺序排序电子邮件：   
```tsql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|镇 |电子邮件 |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>另请参阅  

[字符串函数 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  


