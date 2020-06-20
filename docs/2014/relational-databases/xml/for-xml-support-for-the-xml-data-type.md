---
title: xml 数据类型的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
author: rothja
ms.author: jroth
ms.openlocfilehash: ad905027458e7594a46e3ab416aaa1f4f43cbc59
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061241"
---
# <a name="for-xml-support-for-the-xml-data-type"></a>xml 数据类型的 FOR XML 支持
  如果 FOR XML 查询在 SELECT 子句中指定了 `xml` 类型的列，列值将映射为返回的 XML 中的元素，不管是否指定了 ELEMENTS 指令。 `xml` 类型的列中的任何 XML 声明都不是序列化的。  
  
 例如，下面的查询从类型为的列中检索客户联系人信息 `BusinessEntityID` ，如、 `FirstName` 和 `LastName` 列，以及电话号码 `AdditionalContactInfo` `xml` 。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 因为查询没有指定 ELEMENTS 指令，所以除了从 `xml` 类型列中检索到的其他联系人信息值外，将把列值作为属性返回。 其他信息值作为元素返回。  
  
 下面是部分结果：  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 如果为 XQuery 生成的 XML 列指定列别名，则该别名用于在 XQuery 生成的 XML 周围添加包装元素。 例如，下列查询将 `MorePhoneNumbers` 指定为列别名：  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 XQuery 返回的 XML 包在 <`MorePhoneNumbers`> 元素中，如下面的部分结果所示：  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 如果在查询中指定 ELEMENTS 指令，则 BusinessEntityID、LastName 和 FirstName 将作为生成的 XML 中的元素返回。  
  
 下面的示例说明了 FOR XML 处理逻辑不会从 `xml` 类型列中序列化 XML 数据中的任何 XML 声明：  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 结果如下： 在结果中，XML 声明 <`?xml version="1.0" encoding="UTF-8" ?`> 未被序列化。  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>从用户定义的函数中返回 XML  
 可以使用 FOR XML 查询从用户定义函数返回 XML，该函数将返回下列任意一种结果：  
  
-   含有单个 `xml` 类型列的表  
  
-   `xml` 类型的实例  
  
 例如，下面的用户定义函数返回含有单个 `xm`l 类型列的表：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="http://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 您可以执行用户定义函数并查询由它返回的表。 在本示例中，通过查询表返回的 XML 被分配给一个 `xml` 类型的变量。  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 这是用户定义函数的另一个示例。 此用户定义函数将返回一个 `xml` 类型的实例。 在本示例中，用户定义函数将返回一个类型化的 XML 实例，因为指定了架构命名空间。  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 由用户定义函数返回的 XML 可以被分配给一个 `xml` 类型的变量，如下所示：  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](for-xml-support-for-various-sql-server-data-types.md)  
  
  
