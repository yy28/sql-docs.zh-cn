---
title: 使用嵌套的 FOR XML 查询形成 XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22522a2bfabc3406e8e3e1331a0518a38b930c8a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68000672"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>使用嵌套的 FOR XML 查询形成 XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  下面的示例查询 `Production.Product` 表以检索特定产品的 `ListPrice` 值和 `StandardCost` 值。 为使查询具有趣味性，这两个价格都在 <`Price`> 元素中返回，每个 <`Price`> 元素都有 `PriceType` 属性。  
  
## <a name="example"></a>示例  
 以下是期望的 XML 形状：  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 以下是嵌套的 FOR XML 查询：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 请注意上述查询的以下方面：  
  
-   外部 SELECT 语句构造具有 **ProductID** 属性和两个 <`Price`> 子元素的 <`Product`> 元素。  
  
-   两个内部 SELECT 语句构造两个 <`Price`> 元素，每一个都具有一个 **PriceType** 属性和可以返回产品价格的 XML。  
  
-   外部 SELECT 语句中的 XMLSCHEMA 指令生成用于描述结果 XML 外形的内联 XSD 架构。  
  
 为使查询能够更加有趣，可以编写 FOR XML 查询，然后针对结果编写 XQuery 以重新定形 XML，如以下查询所示：  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 先前的示例使用 **xml** 数据类型的 **query()** 方法查询由内部 FOR XML 查询返回的 XML，并构造预期的结果。  
  
 结果如下：  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用嵌套 FOR XML 查询](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
