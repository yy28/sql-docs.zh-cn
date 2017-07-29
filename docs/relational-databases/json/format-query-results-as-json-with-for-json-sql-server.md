---
title: "使用 FOR JSON 将查询结果格式化为 JSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2017
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
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 50ef4db2a3c9eebcdf63ec9329eb22f1e0f001c0
ms.openlocfilehash: e59b0e12e0ee47a5ac8a68e539144401d80fb649
ms.contentlocale: zh-cn
ms.lasthandoff: 07/20/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>使用 FOR JSON 将查询结果格式化为 JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

通过将 **FOR JSON** 子句添加到 **SELECT** 语句中，将查询结果格式化为 JSON，或者将 SQL Server 中的数据导出为 JSON。 使用 FOR JSON 子句，通过委托从应用到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 JSON 输出格式来简化客户端应用程序。
  
 使用 FOR JSON 子句时，可以显式指定 JSON 输出的结构，或让 SELECT 语句的结构来决定输出。  
  
-   使用 FOR JSON PATH 来维护对 JSON 输出格式的完全控制。 你可以创建包装对象并嵌套复杂属性。  
  
-   使用 FOR JSON AUTO 来根据 SELECT 语句的结构自动格式化 JSON 输出。  
  
下面是带有 **FOR JSON** 子句的 **SELECT** 语句及其输出的示例。
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="option-1---you-control-output-with-for-json-path"></a>选项 1 - 使用 FOR JSON PATH 控制输出
在 **PATH** 模式下，可以使用点语法来设置嵌套的输出格式，例如 `'Item.Price'` 。  

以下是一个使用带有 **FOR JSON** 子句的 **对于 JSON** 模式。 下面的示例使用 **ROOT** 选项指定一个已命名根元素。 
  
 ![FOR JSON 输出流的图示](../../relational-databases/json/media/forjson-example1.png "FOR JSON 输出流的图示")  

### <a name="more-info-about-for-json-path"></a>有关 FOR JSON PATH 的详细信息
有关详细信息和示例，请参阅[使用 PATH 模式 &#40; 格式化嵌套 JSON 输出SQL server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

有关语法和用法的详细信息，请参阅 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>选项 2 - SELECT 语句使用 FOR JSON AUTO 控制输出
在 **AUTO** 模式下，SELECT 语句的结构决定 JSON 输出的格式。

默认情况下，输出中不包括 **null** 值。 你可以使用 **INCLUDE_NULL_VALUES** 来更改此行为。  

以下是一个使用带有 **FOR JSON** 子句的 **AUTO** 模式的示例查询。
 
**查询：**  
  
```sql  
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
 
### <a name="more-info-about-for-json-auto"></a>有关 FOR JSON AUTO 的详细信息
有关详细信息和示例，请参阅[格式自动设置 JSON 输出使用 AUTO 模式 &#40;SQL server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

有关语法和用法的详细信息，请参阅 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="control-other-json-output-options"></a>控制其他 JSON 输出选项  
控制的输出**FOR JSON**子句通过使用以下附加选项。  
  
-   **根**。 若要将单个顶层元素添加到 JSON 输出中，请指定 **ROOT** 选项。 如果未指定此选项，JSON 输出不会包括根元素。 有关详细信息，请参阅 [使用 ROOT 选项将根节点添加到 JSON 输出中 (SQL Server)](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)。  
  
-   **INCLUDE_NULL_VALUES**。 若要在 JSON 输出中包含 null 值，请指定 **INCLUDE_NULL_VALUES** 选项。 如果未指定此选项，输出不包括在查询结果中的 NULL 值的 JSON 属性。 有关详细信息，请参阅[使用 INCLUDE_NULL_VALUES 选项 &#40; 的 JSON 输出中包括 Null 值SQL server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**。 若要删除默认括住 **FOR JSON** 子句的 JSON 输出的方括号，请指定 **WITHOUT_ARRAY_WRAPPER** 选项。 此选项用于作为从单行结果的输出中生成单个 JSON 对象。 如果未指定此选项，JSON 输出格式化为数组-即括在方括号中。 有关详细信息，请参阅 [使用 WITHOUT_ARRAY_WRAPPER 选项从 JSON 输出中删除方括号 (SQL Server)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 子句的输出  
FOR JSON 子句的输出具有以下特征：  
  
1.  结果集包含单个列。
    -   一个小结果集可包含单个列。
    -   一个大型结果集将长的 JSON 字符串拆分跨多行。
        -   默认情况下，SQL Server Management Studio (SSMS) 连接结果为单个行的输出设置时**结果显示为网格**。 SSMS 状态栏会显示的实际行计数。
        -   其他客户端应用程序可能需要代码通过串联多个行的内容来将较长的结果重新组合为单个有效的 JSON 字符串。 此代码在 C# 应用程序的示例，请参阅[在 C# 客户端应用中的使用 FOR JSON 输出](https://docs.microsoft.com/en-us/sql/relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server#use-for-json-output-in-a-c-client-app)。
  
     ![FOR JSON 输出示例](../../relational-databases/json/media/forjson-example2.png "FOR JSON 输出示例")  
  
2.  结果的格式设置为 JSON 对象的数组。  
  
    -   （在应用 FOR JSON 子句） 之前的 JSON 数组中的元素数等于 SELECT 语句的结果中的行数。 
  
    -   选择语句 （在应用 FOR JSON 子句） 之前的结果中的每一行将成为一个单独的 JSON 对象数组中。  
  
    -   （在之前应用子句，FOR JSON) 的 SELECT 语句的结果中每个列将成为 JSON 对象的属性。  
  
3.  列的名称及其值都会根据 JSON 语法进行转义。 有关详细信息，请参阅 [FOR JSON 如何转义特殊字符和控制字符 (SQL Server)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)。
  
### <a name="example"></a>示例
下面是一个示例，演示如何**FOR JSON**子句的 JSON 输出格式设置。  
  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server)](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

