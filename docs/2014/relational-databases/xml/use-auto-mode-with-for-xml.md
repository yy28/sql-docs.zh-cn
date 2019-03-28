---
title: 将 AUTO 模式与 FOR XML 一起使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e6464fee5779e35559b6eca23981aa09312aeb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534789"
---
# <a name="use-auto-mode-with-for-xml"></a>将 AUTO 模式与 FOR XML 一起使用
  如 [FOR XML (SQL Server)](for-xml-sql-server.md)中所述，AUTO 模式将查询结果以嵌套 XML 元素的方式返回。 这不能较好地控制从查询结果生成的 XML 的形式。 如果要生成简单的层次结构，AUTO 模式查询很有用。 但是， [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md) 和 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md) 在确定从查询结果生成的 XML 的形式方面可提供更好的控制和更大的灵活性。  
  
 在 FROM 子句内，每个在 SELECT 子句中至少有一列被列出的表都表示为一个 XML 元素。 如果在 FOR XML 子句中指定了可选的 ELEMENTS 选项，SELECT 子句中列出的列将映射到属性或子元素。  
  
 生成的 XML 中的 XML 层次结构（即元素嵌套）基于由 SELECT 子句中指定的列所标识的表的顺序。 因此，在 SELECT 子句中指定的列名的顺序非常重要。 最左侧第一个被标识的表形成所生成的 XML 文档中的顶级元素。 由 SELECT 语句中的列所标识的最左侧第二个表形成顶级元素内的子元素，依此类推。  
  
 如果 SELECT 子句中列出的列名来自由 SELECT 子句中以前指定的列所标识的表，该列将作为已创建的元素的属性添加，而不是在层次结构中打开一个新级别。 如果已指定 ELEMENTS 选项，该列将作为属性添加。  
  
 例如，执行以下查询：  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 下面是部分结果：  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 对于 SELECT 子句，注意下列内容：  
  
-   CustomerID 引用 Cust 表。 因此，创建一个 <`Cust`> 元素，CustomerID 作为其属性添加。  
  
-   接下来的三列 OrderHeader.CustomerID、OrderHeader.SaleOrderID 和 OrderHeader.Status 引用 OrderHeader 表。 因此，为 <`Cust`> 元素添加 <`OrderHeader`> 子元素，这三列作为 <`OrderHeader`> 的属性添加。  
  
-   接着，Cust.CustomerType 列再次引用 Cust 表，该表已由 Cust.CustomerID 列标识。 因此，不创建新元素， 而是为以前创建的 <`Cust`> 元素添加 CustomerType 属性。  
  
-   查询为表名指定别名。 这些别名显示为相应的元素名。  
  
-   需要使用 ORDER BY 对一个父级下的所有子级分组。  
  
 下面的查询与上一个查询类似，不同的是 SELECT 子句先指定 OrderHeader 表中的列，再指定 Cust 表中的列。 因此，首先创建 <`OrderHeader`> 元素，然后为该元素添加 <`Cust`> 子元素。  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 下面是部分结果：  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 如果在 FOR XML 子句中添加了 ELEMENTS 选项，将返回以元素为中心的 XML。  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 下面是部分结果：  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 在此查询中，因为 CustomerID 是表的主键，所以在创建 \<Cust> 元素的过程中会逐行比较 CustomerID 值。 如果未将 CustomerID 标识为表的主键，将逐行比较所有列值（此查询中的 CustomerID 和 CustomerType）。 如果值不同，将向 XML 添加新的 \<Cust> 元素。  
  
 在比较这些列值时，如果要比较的任何列是 **text**、 **ntext**、 **image**或 **xml**类型，即使它们的值可能相同，FOR XML 也将认为它们是不同的，并且不对其进行比较。 这是因为不支持大型对象的比较。 这些元素将被添加到每个选定行的结果中。 请注意，会比较 **(n)varchar(max)** 和 **varbinary(max)** 类型的列。  
  
 如果 SELECT 子句中的某列无法与 FROM 子句中标识的任何表相关联（例如，该列是聚合列或计算列的情况下），则该列在列表中出现时，将添加到 XML 文档的最深嵌套级别中。 如果该列作为 SELECT 子句的第一列出现，将被添加到顶级元素。  
  
 如果 SELECT 子句中指定了星号 (*) 通配符，则以前面所述的方式根据查询引擎所返回的行的顺序确定嵌套。  
  
## <a name="in-this-section"></a>本节内容  
 下面的主题提供有关 AUTO 模式的更多信息：  
  
-   [使用 BINARY BASE64 选项](use-the-binary-base64-option.md)  
  
-   [返回的 XML 成形过程中的 AUTO 模式试探方法](auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [示例：使用 AUTO 模式](examples-using-auto-mode.md)  
  
## <a name="see-also"></a>请参阅  
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML (SQL Server)](for-xml-sql-server.md)  
  
  
