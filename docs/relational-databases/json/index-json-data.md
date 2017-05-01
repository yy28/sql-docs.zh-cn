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
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>对 JSON 数据编制索引
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  数据库索引可提升筛选和排序操作的性能。 如果没有索引，每次查询数据时，SQL Server 不得不扫描整个表。  
  
 JSON 不是 SQL Server 2016 中的内置数据类型，SQL Server 2016 不具有自定义 JSON 索引。 但是，可以通过使用标准索引最大程度地优化对 JSON 文档的查询。  
  
## <a name="index-json-properties-by-using-computed-columns"></a>通过使用计算列对 JSON 属性编制索引  
 当将 JSON 数据存储到 SQL Server 中时，通常你会希望按 JSON 文档的属性对查询结果进行筛选或排序。  
  
 在此示例中，AdventureWorks SalesOrderHeader 表具有一个“信息”列，其中包含有关销售订单的各种信息 - 例如，有关客户、销售人员、装运/帐单地址等的信息。 你想要使用信息列的值来筛选某个客户的销售订单。 下面是你希望通过使用索引进行优化的查询。  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 如果想要加快针对 JSON 文档中某属性的筛选器或 ORDER BY 子句的运转速度，可以使用正用于其他列的索引。 但是，不能直接引用 JSON 文档中的属性。 必须首先创建一个“虚拟列”，它会返回你要用于筛选的值。 然后，需要对该虚拟列创建索引。  
  
 下面的示例创建可用于编制索引的计算列，然后对此计算列创建索引。 此示例创建一个公开客户名称的列，名称存储在 JSON 文档中的 $.Customer.Name 路径中。  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 计算列是非持久化的。 它不会在表中占用额外空间。 仅在需要重新生成索引时对其进行计算。  
  
 需使用你计划在查询中使用的表达式来创建计算列，这一点很重要。在此示例中为 `JSON_VALUE(Info, '$.Customer.Name')`。  
  
 无须重新编写查询。 如果你使用带有 JSON_VALUE 函数的表达式，SQL Server 会认为存在具有相同表达式的等效计算列，并会在可能的情况下应用索引。 下面是此示例中的查询的执行计划。  
  
 ![执行计划](../../relational-databases/json/media/jsonindexblog1.png "执行计划")  
  
 SQL Server 在非聚集索引中使用索引查找而非进行全表扫描，由此找到满足指定条件的行。 然后它在 SalesOrderHeader 表中使用键查找来提取查询中引用的其他列 - 在此示例中则为 SalesOrderNumber 和 OrderDate。  
  
 如果在 JSON 索引中添加所需的列，则可避免在表中进行这一额外查找。 可将这些列作为标准包含列进行添加，如下例中所示。  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 在这种情况下，SQL Server 不会从 SalesOrderHeader 表中读取其他数据，因为所需内容已全部包含在非聚集 JSON 索引中。 这是在查询中将 JSON 和列数据相结合以及为工作负载创建最佳索引的一个好方法。  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 索引是可识别排序规则的索引  
 JSON 索引的一个重要特性是它们识别排序规则。 JSON_VALUE 函数的结果是一个文本值，该值从输入表达式继承其排序规则。 因此，将使用源列中定义的排序规则对索引中的值进行排序。  
  
 为了阐释这一点，下面的示例创建具有主键和 JSON 内容的一个简单集合表。  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 前一个命令指定 JSON 列的塞尔维亚西里尔文排序规则。 后面的示例填充表，并对名称属性创建索引。  
  
```tsql  
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
  
 前面的命令对计算列 vName 创建标准索引，它表示 JSON $.name 属性的值。 在塞尔维亚西里尔文代码页中，字母的顺序是“А”、“Б”、“В”、“Г”、“Д”、“Ђ”、“Е”等。索引中的项的顺序符合塞尔维亚西里尔文规则，因为 JSON_VALUE 函数的结果从源列继承其排序规则。 下面的示例查询此集合并按名称对结果进行排序。  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 如果查看实际的执行计划，会发现它使用非聚集索引中经过排序的值。  
  
 ![执行计划](../../relational-databases/json/media/jsonindexblog2.png "执行计划")  
  
 虽然查询具有 ORDER BY 子句，但执行计划不使用 Sort 运算符。 此时已根据塞尔维亚西里尔文规则对 JSON 索引进行了排序。 因此 SQL Server 便可使用其中结果已经过排序的非聚集索引。  
  
 但是，如果我们通过表达式来更改排序规则 - 例如，如果将 `COLLATE French_100_CI_AS_SC` 放在 JSON_VALUE 函数之后 - 我们会得到不同的查询执行计划。  
  
 ![执行计划](../../relational-databases/json/media/jsonindexblog3.png "执行计划")  
  
 由于索引中的值的顺序不符合法语排序规则，所以 SQL Server 无法使用索引对结果进行排序。 因此，它会添加一个使用法语排序规则对结果进行排序的 Sort 运算符。  
  
  

