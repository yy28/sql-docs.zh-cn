---
title: "使用具有默认架构的 OPENJSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 2aa30c8c5e0257a819d58688c90b24782d3fd153
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>使用具有默认架构的 OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用具有默认架构的 **OPENJSON** 可返回一个表，其中每行显示对象的一个属性或数组中的一个元素。  
  
 下面的一些示例展示了如何使用具有默认架构的 **OPENJSON** 。 有关详细信息和更多示例，请参阅 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)。  
  
## <a name="example---return-each-property-of-an-object"></a>示例 - 返回对象的各个属性  
 **Query**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **结果**  
  
|Key|值|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>示例 - 返回数组的各个元素  
 **Query**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **结果**  
  
|Key|值|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>示例 - 将 JSON 转换成临时表  
 以下查询返回 **info** 对象的所有属性。  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **结果**  
  
|Key|值|类型|  
|---------|-----------|----------|  
|类型|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|标记|[ "Sport", "Water polo" ]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>示例 - 合并关系数据和 JSON 数据  
 在下面的示例中，SalesOrderHeader 表中有 SalesReason 文本列，其中包含 JSON 格式的 SalesOrderReasons 数组。 SalesOrderReasons 对象包含“Manufacturer”和“Quality”等属性。 此示例创建了一个报表，通过扩展销售原因的 JSON 数组，将每个销售订单行与相关的销售原因联接，就如同将销售原因存储在单独的子表中一样。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 在此示例中，OPENJSON 返回了销售原因表，将原因显示为值列。 CROSS APPLY 运算符将每个销售订单行与 OPENJSON 表值函数返回的行联接。  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
  
  

