---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d95baeee7248aecda4c0bcbc374f378359bb722e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179544"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)
  SELECT 查询将结果作为行集返回。 （可选操作）您可以通过在 SQL 查询中指定 FOR XML 子句，从而将该查询的正式结果作为 XML 来检索。 FOR XML 子句可以用在顶级查询和子查询中。 顶级 FOR XML 子句只能用在 SELECT 语句中。 而在子查询中，FOR XML 可以用在 INSERT、UPDATE 和 DELETE 语句中。 它还可以用在赋值语句中。  
  
 在 FOR XML 子句中，指定以下模式之一：  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
-   PATH  
  
 RAW 模式将为 SELECT 语句所返回行集中的每行生成一个 \<row> 元素。 可以通过编写嵌套 FOR XML 查询来生成 XML 层次结构。  
  
 AUTO 模式将基于指定 SELECT 语句的方式来使用试探性方法在 XML 结果中生成嵌套。 您对生成的 XML 的形状具有最低限度的控制能力。 除了 AUTO 模式的试探性方法生成的 XML 形状之外，还可以编写 FOR XML 查询来生成 XML 层次结构。  
  
 EXPLICIT 模式允许对 XML 的形状进行更多控制。 您可以随意混合属性和元素来确定 XML 的形状。 由于执行查询而生成的结果行集需要具有特定的格式。 此行集格式随后将映射为 XML 形状。 使用 EXPLICIT 模式能够随意混合属性和元素、创建包装和嵌套的复杂属性、创建用空格分隔的值（例如 OrderID 属性可能具有一列排序顺序 ID 值）以及混合内容。  
  
 但是，编写 EXPLICIT 模式的查询会比较麻烦。 可以使用某些新的 FOR XML 功能（例如编写嵌套 FOR XML RAW/AUTO/PATH 模式查询和 TYPE 指令），而不使用 EXPLICIT 模式来生成层次结构。 嵌套 FOR XML 查询可以生成使用 EXPLICIT 模式可生成的任何 XML。 有关详细信息，请参阅 [使用嵌套的 FOR XML 查询](use-nested-for-xml-queries.md) 和 [FOR XML 查询中的 TYPE 指令](type-directive-in-for-xml-queries.md)。  
  
 PATH 模式与嵌套 FOR XML 查询功能一起以较简单的方式提供了 EXPLICIT 模式的灵活性。  
  
 仅当执行设置了这些模式的查询时，这些模式才有效。 它们不会影响以后执行的任何查询的结果。  
  
 对于任何与 FOR BROWSE 子句一起使用的选择语句，FOR XML 均无效。  
  
## <a name="example"></a>示例  
 下面的 `SELECT` 语句将从 `Sales.Customer` 数据库的 `Sales.SalesOrderHeader` 和 `AdventureWorks2012` 表中检索信息。 此查询在 `AUTO` 子句中指定了 `FOR XML` 模式：  
  
```  
USE AdventureWorks2012  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status  
FROM Sales.Customer Cust   
INNER JOIN Sales.SalesOrderHeader OrderHeader  
ON Cust.CustomerID = OrderHeader.CustomerID  
FOR XML AUTO  
```  
  
## <a name="the-for-xml-clause-and-server-names"></a>FOR XML 子句和服务器名称  
 如果带 FOR XML 子句的 SELECT 语句在查询中指定了一个由四部分组成的名称，则在本地计算机上执行查询时，所得 XML 文档中将不返回该服务器名称。 但在网络服务器上执行该查询时，此服务器名称将作为由四部分组成的名称返回。  
  
 例如，请考虑下面的查询：  
  
```  
SELECT TOP 1 LastName  
FROM ServerName.AdventureWorks2012.Person.Person  
FOR XML AUTO  
```  
  
 如果 `ServerName` 是本地服务器，则此查询将返回以下结果：  
  
```  
<AdventureWorks2012.Person.Person LastName="Achong" />  
```  
  
 如果 `ServerName` 是网络服务器，此查询将返回以下结果：  
  
```  
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />  
```  
  
 通过指定如下别名可以避免这种潜在的二义性：  
  
```  
SELECT TOP 1 LastName  
FROM ServerName.AdventureWorks2012.Person.Person x  
FOR XML AUTO   
```  
  
 此查询将返回如下结果：  
  
```  
<x LastName="Achong"/>  
```  
  
## <a name="see-also"></a>请参阅  
 [FOR XML 子句的基本语法](basic-syntax-of-the-for-xml-clause.md)   
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)   
 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)   
 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)   
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)   
 [OPENXML (SQL Server)](openxml-sql-server.md)   
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
