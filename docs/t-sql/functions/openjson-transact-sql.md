---
title: "OPENJSON (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 27eeb54d6493bb200e56caada1238d6fafb5b339
ms.contentlocale: zh-cn
ms.lasthandoff: 10/11/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON**是用于分析 JSON 文本，并返回对象和属性 JSON 输入中的行和列作为表值函数。 换而言之， **OPENJSON**对 JSON 文档中提供的行集视图。 行集和用于填充列的 JSON 属性路径中，可以显式指定的列。 由于**OPENJSON**返回一组行，您可以使用**OPENJSON**中`FROM`子句[!INCLUDE[tsql](../../includes/tsql-md.md)]就像你可以使用任何其他表、 视图或表值函数的语句。  
  
使用**OPENJSON**导入到的 JSON 数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或将 JSON 数据转换为关系格式使应用程序或服务，不能直接使用 JSON。  
  
> [!NOTE]  
>  **OPENJSON**函数是仅在兼容性级别 130 下可用或更高版本。 如果数据库兼容级别低于 130，SQL Server 将无法找到并运行 OPENJSON 函数。 其他 JSON 函数在所有兼容性级别均可用。
> 
> 可以在 `sys.databases` 视图或数据库属性中查看兼容级别。 你可以更改具有以下命令的数据库的兼容级别：  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> 兼容性级别 120 可能甚至中新的 Azure SQL 数据库的默认值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标")[TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

**OPENJSON**表值函数分析*jsonExpression*提供作为第一个参数并返回包含从表达式中的 JSON 对象的数据的一个或多个行。 *jsonExpression*可以包含嵌套的子对象。 如果你想要分析中的子对象*jsonExpression*，你可以指定**路径**参数 JSON 子对象。

### <a name="openjson"></a>openjson

![OPENJSON TVF 语法](../../relational-databases/json/media/openjson-syntax.png "OPENJSON 语法")  

默认情况下， **OPENJSON**表值函数将返回三个列，其中包含键名称，值，并且中找到的每个 {密钥： 值} 对类型*jsonExpression*。 作为替代方法，你可以显式指定结果的架构集的**OPENJSON**返回通过提供*with_clause*。
  
### <a name="withclause"></a>with_clause
  
![使用 OPENJSON TVF 中子句语法](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON 与语法")

*with_clause*包含具有其类型的列的列表**OPENJSON**返回。 默认情况下， **OPENJSON**匹配中的键*jsonExpression*与中的列名称*with_clause* （在这种情况下，匹配键意味着它是区分大小写）。 如果列名称与密钥名称不匹配，你可以提供一个可选*column_path*，即[JSON 路径表达式](../../relational-databases/json/json-path-expressions-sql-server.md)引用内的键*jsonExpression*。 

## <a name="arguments"></a>参数  
### <a name="jsonexpression"></a>*jsonExpression*  
包含 JSON 文本的 Unicode 字符表达式。  
  
OPENJSON 循环访问数组的元素或 JSON 表达式中的对象的属性，并为每个元素或属性返回一行。 下面的示例返回为提供的对象的每个属性*jsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**结果**  
  
|Key|值|类型|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|45|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue|["a"、"r"、"r"、""、"y"]|4|  
|ObjectValue|{"obj":"ect"}|5|  

### <a name="path"></a>*路径*  
引用某个对象或数组中的可选的 JSON 路径表达式*jsonExpression*。 **OPENJSON**定位到指定位置的 JSON 文本，并将其引用的片段。 有关详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).

在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]并在[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，可以提供变量的值作为*路径*。
  
下面的示例通过指定返回嵌套的对象*路径*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **结果**  
  
|Key|值|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
当**OPENJSON**分析的 JSON 数组，该函数返回的元素的索引的 JSON 文本中作为键。

用于匹配的属性的 JSON 表达式的路径步幅比较不区分大小写和排序规则不识别 （即，BIN2 比较）。 

### <a name="withclause"></a>*with_clause*
显式定义的输出架构**OPENJSON**函数以返回。 可选*with_clause*可以包含以下元素：

*colName*是输出列的名称。  
  
默认情况下， **OPENJSON**使用列的名称匹配的 JSON 文本中的属性。 例如，如果指定的列*名称*在架构中，OPENJSON 尝试填充此属性的 JSON 文本中的"名称"列。 你可以使用重写此默认映射*column_path*自变量。  
  
*type*  
是输出列的数据类型。  

> [!NOTE]
> 如果你还使用**AS JSON**选项，列*类型*必须`NVARCHAR(MAX)`。
  
*column_path*  
是指定要返回指定列中的属性的 JSON 路径。 有关详细信息，请参阅说明*路径*以前在本主题中的参数。  
  
使用*column_path*时能重写默认的映射规则的输出列名称与属性的名称不匹配。  
  
用于匹配的属性的 JSON 表达式的路径步幅比较不区分大小写和排序规则不识别 （即，BIN2 比较）。  
  
有关路径的详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*为 JSON*  
使用**AS JSON**列定义中的选项以指定的引用的属性包含一个内部的 JSON 对象或数组。 如果指定**AS JSON**选项，列的类型必须为 nvarchar (MAX)。

-   如果没有指定**AS JSON**对于列，函数将返回标量值 （例如，int、 字符串、 true、 false） 从指定的 JSON 属性在指定路径上。 如果路径表示一个对象或数组，并且在指定的路径找不到属性，该函数返回 null 在宽松模式中，或在严格模式下将返回错误。 此行为是的行为类似**JSON_VALUE**函数。  
  
-   如果指定**AS JSON**对于列，该函数返回 JSON 片段从指定的 JSON 属性在指定路径上。 如果路径表示标量值，并且在指定的路径找不到属性，该函数返回 null 在宽松模式中，或在严格模式下将返回错误。 此行为是的行为类似**JSON_QUERY**函数。  
  
> [!NOTE]  
> 如果你想要从 JSON 属性返回嵌套的 JSON 片段，你必须提供**AS JSON**标志。 如果不使用此选项，如果找不到属性，OPENJSON 返回了 NULL 值而不是引用的 JSON 对象或数组，或它将返回在严格模式下运行时错误。  
  
例如，以下查询返回，数组的元素进行格式设置：  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
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
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**结果**  
  
|Number|日期|Customer|数量|订单|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number":"SO43659"，"日期":"2011年-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number":"SO43661"，"日期":"2011年-06-01T00:00:00"}|  
  

## <a name="return-value"></a>返回值  
OPENJSON 函数返回的列取决于 WITH 选项。  
  
1. 当您调用具有默认架构的 OPENJSON，即当不在 WITH 子句中的指定显式架构函数将返回具有以下各列的表：  
    1.  **密钥**。 一个包含指定属性的名称或指定数组中元素的索引的 nvarchar （4000） 值。 键列具有 BIN2 排序规则。  
    2.  **值**。 一个包含属性的值的 nvarchar (max) 值。 值列继承其排序规则从*jsonExpression*。
    3.  **类型**。 Int 值包含值的类型。 **类型**仅当你使用具有默认架构的 OPENJSON 返回列。 类型列具有以下值之一：  
  
        |类型列的值|JSON 数据类型|  
        |------------------------------|--------------------|  
        |0|null|  
        |1|string|  
        |2|int|  
        |3|true/false|  
        |4|array|  
        |5|对象 (object)|  
  
     仅返回第一个级别的属性。 如果 JSON 文本的格式不正确，则语句将失败。  

2. 当调用 OPENJSON 和你在 WITH 子句中指定显式架构时，函数将返回具有你在 WITH 子句中定义的架构的表。  

## <a name="remarks"></a>注释  

*json_path*的第二个参数中使用**OPENJSON**或*with_clause*可以使用启动**宽松**或**严格**关键字。

-   在**宽松**模式下， **OPENJSON**不会引发错误，如果无法找到指定路径上的值的对象。 如果找不到路径， **OPENJSON**返回空结果集或 NULL 值。
-   在**严格**，模式**OPENJSON**返回错误，如果找不到路径。

某些此页上的示例显式指定的路径模式，lax 或 strict。 Path 模式是可选的。 如果你未显式指定 path 模式，宽松的模式是默认值。 Path 模式和路径表达式的详细信息，请参阅[JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).    

中的列名称*with_clause*与 JSON 文本中的密钥匹配。 如果指定的列名称`[Address.Country]`，与键匹配`Address.Country`。 如果你想要引用嵌套的键`Country`对象内`Address`，你必须指定路径`$.Address.Country`列路径中。

*json_path*可能包含字母数字字符的密钥。 转义中的密钥名称*json_path*用双引号引起来，如果你在键中有特殊字符。 例如，`$."my key $1".regularKey."key with . dot"`匹配值为 1 的以下 JSON 文本中：

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>示例  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>示例 1-将 JSON 数组转换为临时表  
下面的示例以 JSON 数组的数字的形式提供标识符的列表。 查询将 JSON 数组转换为标识符的表和筛选器具有指定 id 的所有产品。  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
此查询相当于下面的示例。 但是，在下面的示例中，你需要在而不是将它们作为参数传递的查询中嵌入数字。  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>示例 2-合并来自两个 JSON 对象的属性  
下面的示例选择的两个 JSON 对象的所有属性的并集。 两个对象具有重复*名称*属性。 示例使用密钥值来从结果中排除重复行。  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>示例 3-包含 JSON 数据存储在表单元格中使用 CROSS APPLY 的联接行  
在下面的示例中，`SalesOrderHeader`表具有`SalesReason`文本列，其中包含的数组`SalesOrderReasons`采用 JSON 格式。 `SalesOrderReasons`对象包含属性，例如*质量*和*制造商*。 该示例创建一个报表，将每个销售订单行联接到相关的销售原因。 OPENJSON 运算符将扩展销售原因的 JSON 数组，原因是存储在单独的子表中。 然后 CROSS APPLY 运算符将每个销售订单行联接到 OPENJSON 表值函数返回的行。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> 你必须展开 JSON 数组存储在单个域中，并将它们加入其父行，则通常使用[!INCLUDE[tsql](../../includes/tsql-md.md)]CROSS APPLY 运算符。 CROSS APPLY 的详细信息，请参阅[FROM &#40;Transact SQL &#41;](../../t-sql/queries/from-transact-sql.md).  
  
可以通过重写相同的查询`OPENJSON`具有要返回的行显式定义的架构：  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
在此示例中，`$`路径可以引用数组中的每个元素。 如果你想要显式强制转换返回的值，你可以使用此类型的查询。  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>示例 4-合并关系行，并使用 CROSS APPLY 的 JSON 元素  
以下查询将关系的行和 JSON 元素合并到下表中显示的结果。  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**结果**  
  
|title|街道|postcode|lon|lat|  
|-----------|------------|--------------|---------|---------|  
|整个食品市场|17991 Redmond 方法|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>示例 5-导入到 SQL Server 的 JSON 数据  
下面的示例展示了将整个 JSON 对象加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 路径表达式 &#40;SQL server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [将 JSON 数据转换为行和列使用 OPENJSON &#40;SQL server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [使用具有默认架构 &#40; 的 OPENJSONSQL server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [使用具有显式架构 &#40; 的 OPENJSONSQL server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

