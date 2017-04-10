---
title: "用 OPENJSON (SQL Server) 将 JSON 数据转换为行和列 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, 导入"
  - "导入 JSON"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# 用 OPENJSON (SQL Server) 将 JSON 数据转换为行和列
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **OPENJSON** 行集函数可将 JSON 文本转换为一组行和列。 你可以使用 **OPENJSON** 在 JSON 集合上运行 SQL 查询，或将 JSON 文本导入 SQL Server 表中。  
  
> [!NOTE] **OPENJSON** 函数仅在**兼容级别 130** 下可用。 如果数据库兼容性级别低于 130，SQL Server 将无法找到并运行 **OPENJSON** 函数。 其他 JSON 函数在所有兼容性级别均可用。 你可以在 sys.databases 视图或数据库属性中查看兼容级别。
> 
>   你可以使用以下命令更改数据库的兼容级别：   
>   ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
  
 **OPENJSON** 函数将获得单个 JSON 对象或 JSON 对象的集合，并将其转换为一行或多行。 默认情况下，**OPENJSON** 函数将返回所有键：JSON 对象的第一级别中可找到的值对或具有其索引的 JSON 数组中的所有元素。  
  
 你可以使用 WITH 子句指定 **OPENJSON** 函数将返回的行的架构。 此显式架构定义输出的结构。  
  
## 使用不具有结果架构的 OPENJSON。

下面是使用具有默认架构的 **OPENJSON**  的快捷示例，该示例为显示 JSON 对象的每个属性返回一行。  
 
如果你使用不具有指定的返回结果架构的 **OPENJSON** 函数（即 OPENJSON 后面没有 WITH 子句），则函数返回的表将具有三列 - 输入对象中的属性的名称（或输入数组中的元素的索引）、属性值或数组元素，以及类型（如字符串、数字、布尔值、数组或对象）。 JSON 对象的属性（或数组元素）返回在不同的行中。  

-   有关详细信息和更多示例，请参阅[使用具有默认架构的 OPENJSON (SQL Server)](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)。
-   有关语法和用法的信息，请参阅 [OPENJSON (Transact SQL)](../../t-sql/functions/openjson-transact-sql.md)。 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
SELECT *  
FROM OPENJSON(@json);  
```  
  
**结果**  
  
|Key|值|type|  
|---------|-----------|----------|  
|name|John|1|  
|姓氏|Doe|1|  
|年龄|45|2|  
|技能|["SQL","C#","MVC"]|4|
    
## 使用具有显式架构的 OPENJSON

以下是使用具有显式指定架构的 **OPENJSON** 的简单示例。  
  
如果在 **OPENJSON** 函数的 WITH 子句中指定了返回结果的架构，则该函数返回的表中将包含 WITH 子句中定义的列。 在 WITH 子句中，你可以指定一组输出列、列类型和每个输出值的 JSON 源属性的路径。 **OPENJSON** 将循环访问 JSON 对象的数组，读取每一列的指定路径上的值，并将值转换为指定类型。  

-   有关详细信息和更多示例，请参阅[使用具有显示架构的 OPENJSON (SQL Server)](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)。
-   有关语法和用法的信息，请参阅 [OPENJSON (Transact SQL)](../../t-sql/functions/openjson-transact-sql.md)。
  
```tsql  
SET @json =   
 N'[  
      {  
        "Order": {  
          "Number":"SO43659",  
          "Date":"2011-05-31T00:00:00"  
        },  
        "AccountNumber":"AW29825",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":1  
        }  
      },  
      {  
        "Order": {  
          "Number":"SO43661",  
          "Date":"2011-06-01T00:00:00"  
        },  
        "AccountNumber":"AW73565",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":3  
        }  
     }  
]'  
  
SELECT * FROM  
OPENJSON ( @json )  
WITH (   
             Number   varchar(200) '$.Order.Number' ,  
             Date     datetime     '$.Order.Date',  
             Customer varchar(200) '$.AccountNumber',  
             Quantity int          '$.Item.Quantity'  
)  
```  
  
**结果**  
  
|Number|日期|Customer|数量|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 此函数返回 JSON 数组的元素并将其格式化。  
  
-   对于 JSON 数组中的每个元素，**OPENJSON** 会在输出表中生成新的一行。 JSON 数组中的两个元素将在返回的表中转换为两行。  
  
-   对于通过使用 `colName type json_path` 语法指定的每一列，**OPENJSON** 函数将转换在指定路径上的数组元素中找到的值，将其转换为指定类型，并且填充输出表中的单元格。 在此示例中，日期列的值获取自路径 `$.Order.Date` 上的每个对象，并被转换为日期时间值。  
  
将 JSON 集合转换为行集后，可以在返回的数据上运行任意 SQL 查询或将其插入到表中。  
  
## 了解 SQL Server 中有关 OPENJSON 和内置 JSON 支持的详细信息  
 [博客作者：Microsoft 项目经理 Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## 另请参阅  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
  
  