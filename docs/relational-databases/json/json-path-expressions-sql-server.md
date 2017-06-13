---
title: "JSON 路径表达式 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 44bfd54aa494dd52174eeed8479e14a99d810af3
ms.contentlocale: zh-cn
ms.lasthandoff: 06/09/2017

---
# <a name="json-path-expressions-sql-server"></a>JSON 路径表达式 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 使用 JSON 路径表达式来引用 JSON 对象的属性。  
  
 在调用以下函数时，必须提供路径表达式。  
  
-   调用 **OPENJSON** 以创建 JSON 数据的关系视图时。 有关详细信息，请参阅 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)。  
  
-   调用 **JSON_VALUE** 以从 JSON 文本中提取值。 有关详细信息，请参阅 [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)。  
  
-   调用 **JSON_QUERY** 以提取 JSON 对象或数组时。 有关详细信息，请参阅 [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)。  
  
-   调用 **JSON_MODIFY** 以更新 JSON 字符串的属性值时。 有关详细信息，请参阅 [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)。  

## <a name="parts-of-a-path-expression"></a>路径表达式的各部分
 路径表达式由两部分组成。  
  
1.  可选[path 模式](#PATHMODE)，值为**宽松**或**严格**。  
  
2.  [路径](#PATH) 本身。  

##  <a name="PATHMODE"></a> Path mode  
 在路径表达式的开头，可以选择指定关键字 **lax** 或 **strict**来声明路径模式。 默认值为 **lax**。  
  
-   在**宽松**模式下，如果路径表达式包含错误，该函数返回空值。 例如，如果请求值**$.name**，但 JSON 文本不包含**名称**密钥，该函数将返回 null，但不会引发错误。  
  
-   在**严格**模式下，如果路径表达式包含错误的函数引发错误。  

以下查询将显式指定`lax`路径表达式中的模式。

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 在声明可选的路径模式后，请指定路径本身。  
  
-   美元符号 (`$`) 表示上下文项。  
  
-   属性路径是一组路径步幅。 路径步幅可以包含下列元素和运算符。  
  
    -   键名。 例如， `$.name` 和 `$."first name"`。 如果键名以美元符号开头或者包含空格等特殊字符，请为其加上引号。   
  
    -   数组元素。 例如， `$.product[3]`。 数组从零开始。  
  
    -   点运算符 (`.`) 指示对象的成员。 例如，在`$.people[1].surname`，`surname`是的子级`people`。
  
## <a name="examples"></a>示例  
 本部分中的示例引用以下 JSON 文本。  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 下表显示了一些路径表达式示例。  
  
|路径表达式|值|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>内置函数如何处理重复的路径  
 如果 JSON 文本包含重复的属性-例如，两个密钥具有相同名称在同一级别的上**JSON_VALUE**和**JSON_QUERY**函数只返回第一个值相匹配的路径。 若要分析包含重复键的 JSON 对象并返回所有值，请使用**OPENJSON**，下面的示例中所示。  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
  
  

