---
title: "使用 FOR JSON 将查询结果格式化为 JSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c439a76e3e925d00e88adaaefa616e59f8529a40
ms.lasthandoff: 04/11/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>使用 FOR JSON 将查询结果格式化为 JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

通过将 **FOR JSON** 子句添加到 **SELECT** 语句中，将查询结果格式化为 JSON，或者将 SQL Server 中的数据导出为 JSON。 使用 **FOR JSON** 子句将 JSON 输出的格式化从客户端应用程序委托给 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
  
 使用 **FOR JSON** 子句时，可以显式指定输出的结构，或让 SELECT 语句的结构来决定输出。  
  
-   将 **PATH** 模式与 **FOR JSON** 一起使用来维持对 JSON 输出格式的完全控制。 你可以创建包装对象并嵌套复杂属性。  
  
-   将 **AUTO** 模式与 **FOR JSON** 子句一起使用来根据 SELECT 语句的结构自动格式化 JSON 输出。  
  
下面是带有 **FOR JSON** 子句的 **SELECT** 语句及其输出的示例。
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="maintain-control-over-json-output-with-path-mode"></a>使用 PATH 模式维持对 JSON 输出的控制  
在 **PATH** 模式下，可以使用点语法来设置嵌套的输出格式，例如 `'Item.Price'` 。 下面的示例使用 **ROOT** 选项指定一个已命名根元素。  

以下是一个使用带有 **FOR JSON** 子句的 **对于 JSON** 模式。
  
 ![FOR JSON 输出流的图示](../../relational-databases/json/media/forjson-example1.png "FOR JSON 输出流的图示")  

### <a name="more-info"></a>详细信息
有关详细信息和示例，请参阅[在 PATH 模式下设置嵌套的 JSON 输出格式 (SQL Server)](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)。

有关语法和用法的详细信息，请参阅 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="let-the-select-statement-control-json-output-with-auto-mode"></a>使用 AUTO 模式让 SELECT 语句控制 JSON 输出  
在 **AUTO** 模式下，SELECT 语句的结构决定 JSON 输出的格式。 默认情况下，输出中不包括 **null** 值。 你可以使用 **INCLUDE_NULL_VALUES** 来更改此行为。  

以下是一个使用带有 **FOR JSON** 子句的 **AUTO** 模式的示例查询。
 
**查询：**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **结果**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
### <a name="more-info"></a>详细信息
有关详细信息和示例，请参阅[在 AUTO 模式下自动格式化 JSON 输出 (SQL Server)](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。

有关语法和用法的详细信息，请参阅 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="control-other-json-output-options"></a>控制其他 JSON 输出选项  
 使用以下选项控制 **FOR JSON** 子句的输出。  
  
-   若要将单个顶层元素添加到 JSON 输出中，请指定 **ROOT** 选项。 如果没有指定 **ROOT** 选项，则 JSON 输出不会包括根元素。 有关详细信息，请参阅 [使用 ROOT 选项将根节点添加到 JSON 输出中 (SQL Server)](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)。  
  
-   若要在 JSON 输出中包含 null 值，请指定 **INCLUDE_NULL_VALUES** 选项。 如果没有指定此选项，输出不会在查询结果中包括 NULL 值的 JSON 属性。 有关详细信息，请参阅[使用 INCLUDE_NULL_VALUES 选项将 JSON 输出包含在 NULL 值中 (SQL Server)](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)。   

-   若要删除默认括住 **FOR JSON** 子句的 JSON 输出的方括号，请指定 **WITHOUT_ARRAY_WRAPPER** 选项。 使用此选项可以生成单个 JSON 对象作为输出。 如果不指定此选项，JSON 输出将括在方括号中。 有关详细信息，请参阅 [使用 WITHOUT_ARRAY_WRAPPER 选项从 JSON 输出中删除方括号 (SQL Server)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 子句的输出  
 **FOR JSON** 子句的输出具有以下特征。  
  
1.  结果集包含单个列。 一个小结果集可包含单个列。 一个大结果集可包含多个列。  
  
     ![FOR JSON 输出示例](../../relational-databases/json/media/forjson-example2.png "FOR JSON 输出示例")  
  
2.  结果的格式设置为 JSON 对象的数组。  
  
    -   数组中元素的数目等于结果中的行数。  
  
    -   结果集中的每一行都是数组中的一个独立 JSON 对象。  
  
    -   结果集中的每一列成为 JSON 对象的一个属性。  
  
3.  列的名称及其值都会根据 JSON 语法进行转义。 有关详细信息，请参阅 [FOR JSON 如何转义特殊字符和控制字符 (SQL Server)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)。
  
 下面是一个示例，演示 JSON 输出的格式设置。  
  
 **查询结果**  
  
|||||  
|-|-|-|-|  
|**指向**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|是|  
|30|31|32|Z|  
  
 **JSON 输出**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  
 有关 **FOR JSON** 子句的输出内容的详细信息，请参阅以下主题。  
-   [FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server)](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
**FOR JSON** 子句使用本主题中所述的规则在 JSON 输出中将 SQL 数据类型转换为 JSON 类型。  

-   [FOR JSON 如何转义特殊字符和控制字符 (SQL Server)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 **FOR JSON** 子句按照本主题所述的方式在 JSON 输出中转义特殊字符和表示控制字符。  

## <a name="learn-more-about-for-json-and-built-in-json-support-in-sql-server"></a>了解 SQL Server 中 FOR JSON 和内置 JSON 支持的详细信息  
 [博客作者：Microsoft 项目经理 Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server)](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

