---
title: FOR XML 查询中的 TYPE 指令 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
caps.latest.revision: 40
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3e5a3ffe184513bce9f331f5d905a0587897e64a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129637"
---
# <a name="type-directive-in-for-xml-queries"></a>FOR XML 查询中的 TYPE 指令
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持[xml &#40;TRANSACT-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql)使您能够根据需要，FOR XML 查询的结果作为返回请求`xml`通过指定 TYPE 指令的数据类型。 这样您便可以在服务器上处理 FOR XML 查询的结果。 例如，你可以对其指定 XQuery，将结果分配给`xml`类型变量，或编写[嵌套 FOR XML 查询](use-nested-for-xml-queries.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回 XML 数据类型到不同服务器构造由于客户端的实例数据，例如使用 TYPE 指令的 FOR XML 查询或在其中`xml`数据类型用于从 SQL 表列和输出返回 XML 实例数据值参数。 在客户端应用程序代码中，ADO.NET 提供程序请求从服务器以二进制编码发送此 XML 数据类型信息。 但是，如果使用的是不带 TYPE 指令的 FOR XML，则 XML 数据将以字符串类型返回。 在任何情况下，客户端访问接口都始终能够处理其中任一种形式的 XML 内容。 请注意，不带 TYPE 指令的顶级 FOR XML 不能与游标一起使用。  
  
## <a name="examples"></a>示例  
 以下示例说明了带 FOR XML 查询的 TYPE 指令的用法。  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>作为 xml 类型检索 FOR XML 查询结果  
 下面的查询检索 `Contacts` 表中的客户联系信息。 由于在 `TYPE` 中指定了 `FOR XML` 指令，因此返回的结果的类型为 `xml`。  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 下面是部分结果：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>将 FOR XML 查询结果赋给 xml 类型变量  
 在下面的示例中，FOR XML 结果分配给`xml`类型变量`@x`。 该查询将检索联系信息，如`BusinessEntityID`， `FirstName`， `LastName`，和其他从电话号码，`AdditionalContactInfo`列`xml``TYPE`。 由于 `FOR XML` 子句指定了 `TYPE` 指令，因此 XML 返回为 `xml` 类型并赋给某个变量。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>查询 FOR XML 查询的结果  
 FOR XML 查询返回 XML。 因此，你可以应用`xml`类型方法，如`query()`和`value()`，到 FOR XML 查询返回的 XML 结果。  
  
 在下面的查询，`query()`方法`xml`数据类型用于查询的结果`FOR XML`查询。 有关详细信息，请参阅 [query() 方法（xml 数据类型）](/sql/t-sql/xml/query-method-xml-data-type)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 内部`SELECT … FOR XML`查询将返回`xml`类型结果外部`SELECT`适用`query()`方法`xml`类型。 请注意指定的 `TYPE` 指令。  
  
 结果如下：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 在下面的查询中，`xml` 数据类型的 `value()` 方法用于检索 `SELECT…FOR XML` 查询返回的 XML 结果中的值。 有关详细信息，请参阅 [value() 方法（xml 数据类型）](/sql/t-sql/xml/value-method-xml-data-type)。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 `value()` 方法中的 XQuery 路径表达式检索 `BusinessEntityID` 为 `1`的客户联系人的第一个电话号码。  
  
> [!NOTE]  
>  如果未指定 TYPE 指令，FOR XML 查询结果则返回类型为`nvarchar(max)`。  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>在 INSERT、UPDATE 和 DELETE 中使用 FOR XML 查询结果 (Transact-SQL DML)  
 下面的示例说明了如何在数据操作语言 (DML) 语句中使用 FOR XML 查询。 在示例中，`FOR XML`返回的实例`xml`类型。 `INSERT` 语句将此 XML 插入表中。  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [FOR XML (SQL Server)](../xml/for-xml-sql-server.md)  
  
  
