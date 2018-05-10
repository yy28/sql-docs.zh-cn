---
title: 使用嵌套 AUTO 模式查询生成同级 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae7999f048b29672f1e324a789d0daccd5aa82e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>使用嵌套 AUTO 模式查询生成同级
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  以下示例显示了如何使用嵌套 AUTO 模式查询来生成同级。 生成此类 XML 的其他方式只有这一种，即使用 EXPLICIT 模式。 但是，这样做可能会很麻烦。  
  
## <a name="example"></a>示例  
 此查询将构造用于提供销售订单信息的 XML。 其中包括：  
  
-   销售订单表头信息、 `SalesOrderID`、 `SalesPersonID`和 `OrderDate`。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 将此信息存储在 `SalesOrderHeader` 表中。  
  
-   销售订单详细信息。 这包括所订购的一个或多个产品、单价和订购数量。 此信息存储在 `SalesOrderDetail` 表中。  
  
-   销售人员信息。 这是获得订单的销售人员。 `SalesPerson` 表提供 `SalesPersonID`。 对于此查询，必须将此表联接到 `Employee` 表以查找销售人员的姓名。  
  
 后面两个不同的 `SELECT` 查询生成外形略有不同的 XML。  
  
 第一个查询生成的 XML 中的 <`SalesPerson`> 和 <`SalesOrderHeader`> 显示为 <`SalesOrder`> 的同级子成员。  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 在先前的查询中，最外面的 `SELECT` 语句执行下列操作：  
  
-   查询在 `SalesOrder` 子句中指定的行集 `FROM`。 结果是包含一个或多个 <`SalesOrder`> 元素的 XML。  
  
-   指定 `AUTO` 模式和 `TYPE` 指令。 `AUTO` 模式将查询结果转换为 XML，且 `TYPE` 指令返回 **xml** 类型的结果。  
  
-   包括两个以逗号分隔的嵌套 `SELECT` 语句。 第一个嵌套 `SELECT` 语句检索销售订单信息、表头和详细信息，第二个嵌套 `SELECT` 语句检索销售人员信息。  
  
    -   检索 `SELECT` 、 `SalesOrderID`和 `SalesPersonID`的 `CustomerID` 语句本身包括另一个返回销售订单详细信息的嵌套 `SELECT ... FOR XML` 语句（使用 `AUTO` 模式和 `TYPE` 指令）。  
  
 检索销售人员信息的 `SELECT` 语句查询在 `SalesPerson`子句中创建的行集 `FROM` 。 若要使用 `FOR XML` 查询，必须提供在 `FROM` 子句中生成的匿名行集的名称。 在本例中，提供的名称为 `SalesPerson`。  
  
 下面是部分结果：  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 以下查询生成的销售订单信息基本相同，只是在结果 XML 中，<`SalesPerson`> 显示为 <`SalesOrderDetail`> 的同级：  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 以下是查询语句：  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 结果如下：  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 由于 `TYPE` 指令将查询结果作为 **xml** 类型返回，因此，可以使用各种 **xml** 数据类型方法查询生成的 XML。 有关详细信息，请参阅 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)。 在以下查询中，注意：  
  
-   将先前的查询添加到 `FROM` 子句。 查询结果返回为表。 注意添加的 `XmlCol` 别名。  
  
-   `SELECT` 子句对 `XmlCol` 子句中返回的 `FROM` 指定 XQuery。 **xml** 数据类型的 **query() 方法**用于指定 XQuery。 有关详细信息，请参阅 [query() 方法（xml 数据类型）](../../t-sql/xml/query-method-xml-data-type.md)。  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [使用嵌套 FOR XML 查询](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
