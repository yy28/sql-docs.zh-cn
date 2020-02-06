---
title: 生成内联 XSD 架构 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0902765a96f68acf811bd3583a41a8e8198d5ca
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943150"
---
# <a name="generate-an-inline-xsd-schema"></a>生成内联 XSD 架构
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  在 FOR XML 子句中，可以请求在查询返回查询结果的同时返回一个内联架构。 如果需要 XDR 架构，可以在 FOR XML 子句中使用 XMLDATA 关键字。 如果需要 XSD 架构，可以使用 XMLSCHEMA 关键字。  
  
 本主题将介绍 XMLSCHEMA 关键字并解释所产生的内联 XSD 架构的结构。 下面是您请求返回内联架构时的一些限制：  
  
-   只能在 RAW 和 AUTO 模式中，而不能在 EXPLICIT 模式中指定 XMLSCHEMA。  
  
-   如果嵌套的 FOR XML 查询指定了 TYPE 指令，查询结果则属于 **xml** 类型，并且此结果将被视为非类型化的 XML 数据的实例。 有关详细信息，请参阅 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)。  
  
 在 FOR XML 查询中指定 XMLSCHEMA 后，查询结果中便同时包含架构和 XML 数据。 数据的每个顶级元素都通过使用默认命名空间声明来引用前一个架构，而默认命名空间又引用内联架构的目标命名空间。  
  
 例如：  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 结果包含 XML 架构和 XML 结果。 结果中的 <`ProductModel`> 顶级元素通过使用默认命名空间声明 xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" 来引用该架构。  
  
 结果的架构部分可能包含说明多个命名空间的多个架构文档。 至少将返回下列两个架构文档：  
  
-   一个是说明 **Sqltypes** 命名空间的架构文档，并为其返回基本 SQL 类型。  
  
-   另一个是说明 FOR XML 查询结果形状的架构文档。  
  
 而且，如果查询结果中包含了任何类型化的 **xml** 数据类型，则与这些类型化的 **xml** 数据类型相关联的架构也包含在查询结果中。  
  
 说明 FOR XML 结果形状的架构文档的目标命名空间包含一个固定部分和一个自动递增的数值部分。 此命名空间的格式如下所示，其中 *n* 是一个正整数。 例如，在前一个查询中，urn:schemas-microsoft-com:sql:SqlRowSet1 是目标命名空间。  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 您可能希望两次执行的结果中的目标命名空间相同。 例如，如果对产生的 XML 进行查询，则假如目标命名空间发生更改，将需要更新查询。 通过在 FOR XML 子句中添加 XMLSCHEMA 选项，可以指定目标命名空间。 产生的 XML 将包含您提供的命名空间，而且无论运行该查询多少次，该命名空间都将保持不变。  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>实体元素  
 为了讨论为查询结果生成的 XSD 架构结构的详细信息，必须首先介绍实体元素。  
  
 由 FOR XML 查询返回的 XML 数据中的实体元素是从表而不是从列生成的。 例如，下列 FOR XML 查询将返回 `Person` 数据库的 `AdventureWorks2012` 表中的联系人信息。  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 结果如下：  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 在此结果中，<`Person`> 是实体元素。 在 XML 结果中可以有多个实体元素，并且每个实体元素在内联 XSD 架构中都具有全局声明。 例如，下面的查询将检索某个特定订单的销售订单标题和详细信息。  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 由于该查询指定了 ELEMENTS 指令，所以产生的 XML 是以元素为中心的。 该查询还指定了 XMLSCHEMA 指令。 因此，将返回一个内联 XSD 架构。 结果如下：  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 请注意上述查询的以下方面：  
  
-   在结果中，<`SalesOrderHeader`> 和 <`SalesOrderDetail`> 是实体元素。 因此，它们在架构中是以全局的方式声明的。 也就是说，声明显示在 <`Schema`> 元素内的顶级。  
  
-   <`SalesOrderID`>、<`ProductID`> 和 <`OrderQty`> 不是实体元素，因为它们映射到一些列。 由于指定了 ELEMENTS 指令，列数据将作为 XML 中的元素返回。 它们被映射到实体元素的复杂类型的本地元素。 请注意，如果没有指定 ELEMENTS 指令，则 `SalesOrderID`、 `ProductID` 和 `OrderQty` 值将被映射到相应实体元素的复杂类型的本地属性。  
  
## <a name="attribute-name-clashes"></a>属性名称冲突  
 下面的论述基于 `CustOrder` 和 `CustOrderDetail` 表。 若要测试下列示例，请创建这些表并添加自己的示例数据：  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 在 FOR XML 中，同一个名称有时用来表示不同的属性、特性。 例如，下面的以属性为中心的 RAW 模式查询将生成具有相同名称 (OrderID) 的两个属性。 这将生成一个错误。  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 但是，由于两个元素具有相同的名称是可以接受的，因此可以通过添加 ELEMENTS 指令来消除该问题。  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 结果如下： 请注意，在内联 XSD 架构中，OrderID 元素被定义了两次。 一个声明将 minOccurs 设置为 0（对应于 CustOrderDetail 表的 OrderID）；另一个声明映射到 `CustOrder` 表的 OrderID 主键列，在这种情况下，minOccurs 默认设置为 1。  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>元素名称冲突  
 在 FOR XML 中，同一个名称可以用来表示两个子元素。 例如，下面的查询将检索产品的 ListPrice 和 DealerPrice 值，但为这两列指定了同一别名 (Price)。 因此，产生的行集将具有名称相同的两列。  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>情况 1：两个子元素是相同类型的非键列而且可以为 NULL  
 在下面的查询中，两个子元素是相同类型的非键列而且可以为 NULL。  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 下面是生成的相应 XML。 仅显示了一部分内联 XSD：  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 请注意该内联 XSD 架构的以下方面：  
  
-   ListPrice 和 DealerPrice 属于同一类型 ( `money`)，在表中都可以为 NULL。 因此，由于产生的 XML 中可能不返回它们，所以在 minOccurs=0 且 maxOccurs=2 的 <`Price`> 元素的复杂类型声明中仅有一个 <`row`> 子元素。  
  
-   在结果中，由于表中的 `DealerPrice` 值为 NULL，所以只有 `ListPrice` 被作为一个 <`Price`> 元素返回。 如果将 `XSINIL` 参数添加到 ELEMENTS 指令，则假如将对应于 DealerPrice 的 <`xsi:nil`> 元素的 `Price` 值设置为 TRUE，返回的结果中将包括这两个元素。 如果将两个元素的 `Price` 属性设置为 TRUE，还将收到内联 XSD 架构的 <`row`> 复杂类型定义中的两个 <`nillable`> 子元素。 下面是部分结果：  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>情况 2：相同类型的一个键列和一个非键列  
 下面的查询说明了相同类型的一个键列和一个非键列。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 下面对表 **T** 的查询为 Col1 和 Col2 指定了相同的别名，其中 Col1 是主键，不能为空，而 Col2 可以为空。 这将生成两个同级元素，它们都是 <`row`> 元素的子元素。  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 结果如下： 仅显示了一部分内联 XSD 架构。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 请注意，在内联 XSD 架构中，对应于 Col2 的 <`Col`> 元素的 minOccurs 被设置为 0。  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>情况 3：两个不同类型的元素而且对应的列可以为 NULL  
 对情况 2 中显示的示例表进行下面的查询：  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 在下面的查询中，Col2 和 Col3 被给予相同的别名。 这将生成两个具有相同名称的同级元素，而且它们都是结果中 <`raw`> 元素的子元素。 这两列类型不同，而且都可以为 NULL。 结果如下： 仅显示了部分内联 XSD 架构。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 请注意该内联 XSD 架构的以下方面：  
  
-   由于 Col2 和 Col3 都可以为 NULL，所以 <`Col`> 元素声明将 minOccurs 指定为 0，将 maxOccurs 指定为 2。  
  
-   由于两个 <`Col`> 元素是同级元素，所以在架构中只有一个元素声明。 而且，还由于两个元素类型不同，所以尽管都是简单类型，架构中元素的类型仍为 `xsd:anySimpleType`。 在结果中，每个实例类型都由 `xsi:type` 属性标识。  
  
-   在结果中，<`Col`> 元素的每个实例都通过使用 `xsi:type` 属性来引用其实例类型。  
  
  
