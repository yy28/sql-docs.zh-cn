---
title: 示例：使用 AUTO 模式 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a280477dbc8a41292ff3ee3519ec74df4d5c7ea
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943417"
---
# <a name="examples-using-auto-mode"></a>示例：使用 AUTO 模式
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  下列示例说明了 AUTO 模式的使用。 这些查询中有许多都针对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库的 ProductModel 表的 Instructions 列中存储的自行车生产说明 XML 文档指定的。  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>示例：检索客户、订单和订单详细信息  
 此查询检索特定客户的客户、订单和订单详细信息。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 由于查询标识了 `Cust`、 `OrderHeader`、 `Detail`和 `Product` 表别名，因此 `AUTO` 模式生成相应的元素。 同样，由 `SELECT` 子句中指定的列所标识的表的顺序确定这些元素的层次结构。  
  
 下面是部分结果：  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>示例：指定 GROUP BY 和聚合函数  
 以下查询将返回各个客户 ID 以及客户已请求的订单数。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>示例：在 AUTO 模式下指定计算列  
 此查询返回串联的各个客户名以及订单信息。 因为计算列被分配到在该点（在此例中是 <`SOH`>）出现的最内层级别， 因此，串联的客户名在结果中作为 <`SOH`> 元素的属性添加。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 下面是部分结果：  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 若要检索具有 `IndividualCustomer` 属性（包含销售订单表头信息，并将每条信息作为一个子元素）的 <`Name`> 元素，应使用嵌套的 SELECT 子句重写查询。 内部 SELECT 子句创建临时的 `IndividualCustomer` 表，此表具有计算列，其中包含各个客户的名称。 然后，此表与 `SalesOrderHeader` 表联接以获得结果。  
  
 请注意， `Sales.Customer` 表存储有单个客户信息，其中包括该客户的 `PersonID` 值。 然后，此 `PersonID` 用于从 `Person.Person` 表中查找联系人姓名。  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 下面是部分结果：  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>示例：返回二进制数据  
 此查询返回 `ProductPhoto` 表中的产品照片。 `ThumbNailPhoto` 是 **表中的** varbinary(max) `ProductPhoto` 列。 默认情况下， `AUTO` 模式向二进制数据返回一个引用，该引用为执行查询的数据库的虚拟根目录的相对 URL。 必须指定 `ProductPhotoID` 键属性，才能标识图像。 如此示例中所示，检索图像引用时，还必须在 `SELECT` 子句中指定表的主键，才能唯一标识行。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 结果如下：  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 用 `BINARY BASE64` 选项执行上述查询。 查询以 base64 编码格式返回二进制数据。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 结果如下：  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 默认情况下，使用 AUTO 模式检索二进制数据时，将返回执行查询的数据库的虚拟根目录的相对 URL 的引用，而不返回二进制数据。 如果未指定 BINARY BASE64 选项，也会出现这种情况。  
  
 当 AUTO 模式返回不区分大小写的数据库（查询中指定的表名或列名与数据库中的表名或列名不匹配）中的二进制数据的 URL 引用时，将执行查询。 但是，引用中返回结果的大小写将不一致。 例如：  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 结果如下：  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 这可能成为一个问题，尤其是对区分大小写的数据库执行 dbobject 查询时。 若要避免这个问题，查询中指定的表名或列名的大小写应该与数据库中表名或列名的大小写一致。  
  
## <a name="example-understanding-the-encoding"></a>示例：了解编码  
 下面的示例显示了结果中出现的各种编码。  
  
 创建下表：  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 将下列数据添加到表中：  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 下面的查询将返回该表中的数据。 指定了 FOR XML AUTO 模式。 二进制数据作为引用返回。  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 结果如下：  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 下面是对结果中的特殊字符进行编码的过程：  
  
-   通过使用相应的 Unicode 字符的十六进制值，对查询结果中返回的元素名及属性名中的特殊 XML 和 URL 字符进行编码。 在上面的结果中，元素名 <`Special Chars`> 作为 <`Special_x0020_Chars`> 返回。 属性名称 <`Col#&2`> 作为 <`Col_x0023__x0026_2`> 返回。 XML 和 URL 特殊字符都进行了编码。  
  
-   如果元素值或属性值包含 5 个标准 XML 字符实体（'、""、\<、> 和 &）中的任何一个，将始终使用 XML 字符编码对这些特殊 XML 字符进行编码。 在上面的结果中，属性 <`&`> 的值中的 `Col1` 值被编码为 `&`。 但是，# 字符仍保留为 #，因为它是有效的 XML 字符，而不是特殊的 XML 字符。  
  
-   如果元素值或属性值包含 URL 中有特殊意义的任何特殊 URL 字符，则只能在 DBOBJECT URL 值中对它们进行编码，而且只有当该特殊字符是表名或列名的一部分时，才会对它们进行编码。 在结果中，作为表名 `#` 的一部分的字符 `Col#&2` 被编码为 `_x0023_ in the DBOJBECT URL`。  
  
## <a name="see-also"></a>另请参阅  
 [将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
