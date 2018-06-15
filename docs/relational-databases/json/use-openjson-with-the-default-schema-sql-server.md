---
title: 使用具有默认架构的 OPENJSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fcca984a6c35477267f9776cce89eef7b4faee8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32941782"
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>使用具有默认架构的 OPENJSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  使用具有默认架构的 OPENJSON 可返回一个表，其中每行显示对象的一个属性或数组中的一个元素。  
  
 下面的一些示例展示了如何使用具有默认架构的 **OPENJSON** 。 有关详细信息和更多示例，请参阅 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)。  
  
## <a name="example---return-each-property-of-an-object"></a>示例 - 返回对象的各个属性  
 **“数据集属性”**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **结果**  
  
|Key|ReplTest1|  
|---------|-----------|  
|NAME|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>示例 - 返回数组的各个元素  
 **“数据集属性”**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **结果**  
  
|Key|ReplTest1|  
|---------|-----------|  
|0|en-GB|  
|@shouldalert|en-UK|  
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
  
|Key|ReplTest1|类型|  
|---------|-----------|----------|  
|type|@shouldalert|0|  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>详细了解 SQL Server 和 Azure SQL 数据库中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 博客文章  
  
若要获取特定解决方案、用例和建议，请参阅有关 SQL Server 和 Azure SQL 数据库中内置 JSON 支持的[博客文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。  

### <a name="microsoft-videos"></a>Microsoft 视频

有关 SQL Server 和 Azure SQL 数据库中内置 JSON 支持的视频介绍，请观看以下视频：

-   [SQL Server 2016 和 JSON 支持](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [在 SQL Server 2016 和 Azure SQL 数据库中使用 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON 充当 NoSQL 和关系环境之间的桥梁](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另请参阅  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
