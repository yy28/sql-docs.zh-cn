---
title: 示例：指定 ID 和 IDREFS 指令 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5483235964a1b10decad823313e3657809a7d34a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>示例：指定 ID 和 IDREFS 指令
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  可以将元素属性指定为 **ID** 类型属性，然后就可以使用 **IDREFS** 属性来引用它。 这将启用文档内链接，与关系数据库中主键和外键关系类似。  
  
 此示例说明如何使用 **ID** 和 **IDREFS** 指令来创建 **ID** 和 **IDREFS** 类型的属性。 因为 ID 不能是整数值，所以对此示例中的 ID 值进行了转换。 也就是说，它们进行了类型转换。 ID 值中使用了前缀。  
  
 假定要如下所示构造 XML：  
  
```  
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >  
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
 < `SalesOrderIDList` > 元素的 `Customer` 属性是一个多值属性，它引用 < `SalesOrderID` > 元素的 `SalesOrder` 属性。 若要建立此链接，必须将 `SalesOrderID` 属性声明为 `ID` 类型，并且必须将 < `Customer`> 元素的 `SalesOrderIDList` 属性声明为 `IDREFS` 类型。 因为一个客户可请求多个订单，所以使用 `IDREFS` 类型。  
  
 **IDREFS** 类型的元素也有多个值。 因此，必须使用单独的 SELECT 子句来重复使用相同的标记、父级和键列信息。 然后， `ORDER BY` 必须确保组成 **IDREFS** 值的行的序列成组显示在它们的父元素下。  
  
 下面是生成所需的 XML 的查询。 该查询使用 `ID` 和 `IDREFS` 指令来覆盖列名称（`SalesOrder!2!SalesOrderID!ID`、 `Customer!1!SalesOrderIDList!IDREFS`）中的类型。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID       [Customer!1!CustomerID],  
        NULL               [Customer!1!SalesOrderIDList!IDREFS],  
        NULL               [SalesOrder!2!SalesOrderID!ID],  
        NULL               [SalesOrder!2!OrderDate]  
FROM   Sales.Customer C   
UNION ALL   
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID,  
        'O-'+CAST(SalesOrderID as varchar(10)),   
        NULL,  
        NULL  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
        C.CustomerID,  
        NULL,  
        'O-'+CAST(SalesOrderID as varchar(10)),  
        OrderDate  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerIDORDER BY [Customer!1!CustomerID] ,  
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
