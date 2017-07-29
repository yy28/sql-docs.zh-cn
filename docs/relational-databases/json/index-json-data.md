---
title: "对 JSON 数据编制索引 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="index-json-data"></a>对 JSON 数据编制索引
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

在 SQL Server 2016 中，JSON 不是内置数据类型，和 SQL Server 不具有自定义 JSON 索引。 你可以优化你的查询对 JSON 文档，但是，通过使用标准索引。 

数据库索引可提升筛选和排序操作的性能。 如果没有索引，每次查询数据时，SQL Server 不得不扫描整个表。  
  
## <a name="index-json-properties-by-using-computed-columns"></a>通过使用计算列对 JSON 属性编制索引  
当将 JSON 数据存储在 SQL Server 中时，通常要进行筛选或排序查询结果的一个或多*属性*的 JSON 文档。  

### <a name="example"></a>示例 
在此示例中，假定 AdventureWorks`SalesOrderHeader`表具有`Info`包含 JSON 格式中有关销售订单的各种信息的列。 例如，它包含有关客户、 销售人员、 装运和帐单地址等信息。 你想要使用的值`Info`列来筛选某个客户的销售订单。

### <a name="query-to-optimize"></a>若要优化的查询
下面是类型的查询的你想通过使用索引来优化的示例。  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>示例索引
如果你想要加快你的筛选器或`ORDER BY`子句在 JSON 文档中的属性，可以使用您已在其他列使用相同的索引。 但是，你不能*直接*引用 JSON 文档中的属性。
    
1.  首先，你必须创建一个"虚拟列"返回你想要用于筛选的值。
2.  然后，需要对该虚拟列创建索引。  
  
下面的示例创建的计算的列，可用于索引。 然后在新的计算列上创建了索引。 此示例将创建公开客户名称，它存储在列`$.Customer.Name`JSON 数据中的路径。 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>有关计算列的详细信息 
计算列是非持久化的。 仅在需要重新生成索引时对其进行计算。 它不会在表中占用额外空间。   
  
它是你创建计算的列使用同一表达式你打算使用您的查询-在此示例中，表达式是重要`JSON_VALUE(Info, '$.Customer.Name')`。  
  
无须重新编写查询。 如果你使用与表达式`JSON_VALUE`函数，如上面的示例查询中所示 SQL Server 会存在为使用同一表达式的等效计算的列，并且如果可能将应用索引。

### <a name="execution-plan-for-this-example"></a>此示例的执行计划
下面是此示例中的查询的执行计划。  
  
![执行计划](../../relational-databases/json/media/jsonindexblog1.png "执行计划")  
  
SQL Server 在非聚集索引中使用索引查找而非进行全表扫描，由此找到满足指定条件的行。 然后，它使用中的键查找`SalesOrderHeader`表以获取其他查询-在此示例中中, 引用的列`SalesOrderNumber`和`OrderDate`。  
 
### <a name="optimize-the-index-further-with-included-columns"></a>优化进一步带有包含列的索引
如果索引中添加所需的列，则可避免这一额外查找表中。 可以添加这些列作为标准包含列，如以下示例中，扩展了中所示`CREATE INDEX`上面所示的示例。  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
在这种情况下不具有 SQL Server 将从中读取其他数据`SalesOrderHeader`表，因为它需要的所有内容包括非聚集 JSON 索引中。 这是在查询中的 JSON 和列数据相结合以及为你的工作负载创建最佳索引的好方法。  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 索引是可识别排序规则的索引  
对 JSON 数据的索引的一个重要功能是可识别排序规则的索引。 结果`JSON_VALUE`在创建计算的列时使用的函数是一个文本值，从输入表达式继承其排序规则。 因此，在索引中的值进行排序使用源列中定义的排序规则。  
  
为了阐释这一点，下面的示例创建具有主键和 JSON 内容的一个简单集合表。  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
前一个命令指定 JSON 列的塞尔维亚西里尔文排序规则。 后面的示例填充表，并对名称属性创建索引。  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
前面的命令对计算列创建标准索引`vName`，它表示值从 JSON`$.name`属性。 在塞尔维亚西里尔文代码页中，字母的顺序是“А”、“Б”、“В”、“Г”、“Д”、“Ђ”、“Е”等。在索引中的项的顺序是符合塞尔维亚西里尔文规则因为的结果`JSON_VALUE`函数从源列继承其排序规则。 下面的示例查询此集合并按名称对结果进行排序。  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 如果查看实际的执行计划，会发现它使用非聚集索引中经过排序的值。  
  
 ![执行计划](../../relational-databases/json/media/jsonindexblog2.png "执行计划")  
  
 虽然查询具有`ORDER BY`子句，执行计划不使用 Sort 运算符。 此时已根据塞尔维亚西里尔文规则对 JSON 索引进行了排序。 因此 SQL Server 便可使用其中结果已经过排序的非聚集索引。  
  
 但是，如果我们更改排序规则`ORDER BY`表达式-例如，如果我们将放`COLLATE French_100_CI_AS_SC`后`JSON_VALUE`函数-我们获得不同的查询执行计划。  
  
 ![执行计划](../../relational-databases/json/media/jsonindexblog3.png "执行计划")  
  
 由于索引中的值的顺序不符合法语排序规则，所以 SQL Server 无法使用索引对结果进行排序。 因此，它会添加一个使用法语排序规则对结果进行排序的 Sort 运算符。  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。

