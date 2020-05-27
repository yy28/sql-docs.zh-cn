---
title: 示例：指定 ID 和 IDREF 指令 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- IDREF directive
- ID directive
ms.assetid: 7ff1ea73-71ca-4786-bd42-564f1b5de2d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76e471b3e6e35e3c6f0568c446b9650466ffa542
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68006694"
---
# <a name="example-specifying-the-id-and-idref-directives"></a>示例：指定 ID 和 IDREF 指令

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此示例与 [指定 ELEMENTXSINIL 指令](../../relational-databases/xml/example-specifying-the-elementxsinil-directive.md) 示例几乎相同。 唯一的差别在于查询指定的是 **ID** 和 **IDREF** 指令。 这些指令覆盖 <`OrderHeader`> 和 <`OrderDetail`> 元素中 **SalesPersonID** 属性的类型。 这会形成文档内链接。 您需要使用架构才能查看被覆盖的类型。 因此，该查询在 FOR XML 子句中指定 **XMLDATA** 选项来检索架构。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        SalesOrderID  as [OrderHeader!1!SalesOrderID!id],  
        OrderDate     as [OrderHeader!1!OrderDate],  
        CustomerID    as [OrderHeader!1!CustomerID],  
        NULL          as [SalesPerson!2!SalesPersonID],  
        NULL          as [OrderDetail!3!SalesOrderID!idref],
        NULL          as [OrderDetail!3!LineTotal],  
        NULL          as [OrderDetail!3!ProductID],  
        NULL          as [OrderDetail!3!OrderQty]  
FROM   Sales.SalesOrderHeader  
WHERE  SalesOrderID=43659 or SalesOrderID=43661  

UNION ALL   
SELECT 2 as Tag,  
       1 as Parent,  
        SalesOrderID,   
        NULL,  
        NULL,  
        SalesPersonID,    
        NULL,           
        NULL,           
        NULL,  
        NULL           
FROM   Sales.SalesOrderHeader  
WHERE  SalesOrderID=43659 or SalesOrderID=43661  

UNION ALL  
SELECT 3 as Tag,  
       1 as Parent,  
        SOD.SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,  
        SOH.SalesOrderID,  
        LineTotal,  
        ProductID,  
        OrderQty     
FROM    Sales.SalesOrderHeader SOH,
        Sales.SalesOrderDetail SOD  
WHERE   SOH.SalesOrderID = SOD.SalesOrderID  
AND     (SOH.SalesOrderID=43659 or SOH.SalesOrderID=43661)
ORDER BY [OrderHeader!1!SalesOrderID!id],
         [SalesPerson!2!SalesPersonID],  
         [OrderDetail!3!SalesOrderID!idref],
         [OrderDetail!3!LineTotal]

FOR XML EXPLICIT, XMLDATA;
```  
  
 下面是部分结果： 请注意，在架构中，**ID** 和 **IDREF** 指令已经覆盖了 <`OrderHeader`> 和 <`OrderDetail`> 元素中 **SalesOrderID** 属性的数据类型。 如果删除这些指令，架构将返回这些属性的原始类型。  
  
```xml
<Schema
       name="Schema1"
       xmlns="urn:schemas-microsoft-com:xml-data"
       xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="OrderHeader" content="mixed" model="open">  
    <AttributeType name="SalesOrderID" dt:type="id" />  
    <AttributeType name="OrderDate" dt:type="dateTime" />  
    <AttributeType name="CustomerID" dt:type="i4" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <attribute type="CustomerID" />  
  </ElementType>  
  <ElementType name="SalesPerson" content="mixed" model="open">  
    <AttributeType name="SalesPersonID" dt:type="i4" />  
    <attribute type="SalesPersonID" />  
  </ElementType>  
  <ElementType name="OrderDetail" content="mixed" model="open">  
    <AttributeType name="SalesOrderID" dt:type="idref" />  
    <AttributeType name="LineTotal" dt:type="number" />  
    <AttributeType name="ProductID" dt:type="i4" />  
    <AttributeType name="OrderQty" dt:type="i2" />  
    <attribute type="SalesOrderID" />  
    <attribute type="LineTotal" />  
    <attribute type="ProductID" />  
    <attribute type="OrderQty" />  
  </ElementType>  
</Schema>  
<OrderHeader
       xmlns="x-schema:#Schema1"
       SalesOrderID="43659"
       OrderDate="2001-07-01T00:00:00"
       CustomerID="676">  
  <SalesPerson SalesPersonID="279" />  
  <OrderDetail
         SalesOrderID="43659"
         LineTotal="10.373000"
         ProductID="712"
         OrderQty="2" />  
  ...  
</OrderHeader>  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
