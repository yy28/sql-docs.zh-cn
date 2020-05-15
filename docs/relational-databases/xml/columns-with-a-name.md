---
title: 具有名称的列 | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 855f7c079d592c095ce3754cd5c6fc799139324e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68113055"
---
# <a name="columns-with-a-name"></a>具有名称的列

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

下面是一些特定条件，在这些条件下具有名称的行集列将映射（区分大小写）到生成的 XML：  
  
-   列名以 at 符号 (\@) 开头。  
  
-   列名不以 at 符号 (\@) 开头。  
  
-   列名不以 at 符号 (\@) 开头，但包含斜线标记 (/)。  
  
-   多个列共享同一前缀。  
  
-   一列具有不同的名称。  
  
## <a name="column-name-starts-with-an-at-sign-"></a>列名以 at 符号 (\@) 开头  
 如果列名以 at 符号 (\@) 开头且不包含斜线标记 (/)，就会创建包含相应列值的 `row` 元素的属性。 例如，下面的查询返回包含两列（\@PmId 和 Name）的行集。 在生成的 XML 中，会向相应的  **元素添加 PmId 属性并为其分配 ProductModelID 值**`row`。  
  
```sql
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
 结果如下：  
  
```xml
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 请注意，在同一级别中，属性必须出现在其他任何节点类型（例如元素节点和文本节点）之前。 以下查询将返回一个错误：  
  
```sql
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>列名不以 at 符号 (\@) 开头  
 如果列名不以 at 符号 (\@) 开头、不是 XPath 节点测试之一且不包含斜线标记 (/)，就会创建作为行元素（默认为 `row`）的子元素的 XML 元素。  
  
 以下查询指定了列名 result。 因此，会向 `result` 元素添加 `row` 子元素。  
  
```sql
SELECT 2+2 as result  
for xml PATH;
```  
  
 结果如下：  
  
```xml
<row>  
  <result>4</result>  
</row>  
```  
  
 以下查询为针对 **xml** 类型的 Instructions 列指定的 XQuery 所返回的 XML 指定了列名 ManuWorkCenterInformation。 因此，可添加 `ManuWorkCenterInformation` 元素来作为 `row` 元素的子元素。  
  
```sql
SELECT
  ProductModelID,  
  Name,  
  Instructions.query(
    'declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";
     /MI:root/MI:Location
    ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;
```  
  
 结果如下：  
  
```xml
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>列名不以 at 符号 (\@) 开头，但包含斜线标记 (/)  
 如果列名不以 at 符号 (\@) 开头，但包含斜线标记 (/)，列名就指明了 XML 层次结构。 例如，列名为“Name1/Name2/Name3.../Name***n*** ”，其中每个 Name***i*** 表示嵌套在当前行元素 (i=1) 中的元素名称或名为 Name***i-1***的元素下的元素名称。 如果 Namen 以“\@”开头，它就会映射到 Namen-1 元素的属性。  
  
 例如，以下查询将返回雇员 ID 和表示为复杂元素 EmpName（包含名字、中间名和姓氏）的雇员名称。  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  AND
       E.EmployeeID=1  
FOR XML PATH;
```  
  
 列名用作在 PATH 模式中构造 XML 时的路径。 包含雇员 ID 值的列名以“\@”开头。因此，向  **元素添加 EmpID 属性**`row`。 其他所有列的列名中均包含指明层次结构的斜杠标记 (/)。 在生成的 XML 中，`EmpName` 元素下包含 `row` 子元素，而 `EmpName` 子元素包含 `First`、`Middle` 和 `Last` 子元素。  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 雇员的中间名为 Null，默认情况下，Null 值映射为“缺少相应的元素或属性”。 如果希望针对 NULL 值生成元素，则可以指定带有 XSINIL 的 ELEMENTS 指令，如以下查询中所示。  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  AND
       E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 结果如下：  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 默认情况下，PATH 模式生成以元素为中心的 XML。 因此，在 PATH 模式中指定 ELEMENTS 指令将不起作用。 但是，如上一个示例所示，可以指定带有 XSINIL 的 ELEMENTS 指令来针对 Null 值生成元素。  
  
 除了 ID 和名称以外，以下查询还将检索雇员地址。 按照地址列的列名中包含的路径，可向 `Address` 元素添加 `row` 子元素，并添加地址详细信息来作为 `Address` 元素的子元素。  
  
```sql
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E,
       Person.Contact C,
       Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH;
```  
  
 结果如下：  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>若干列共享同一个路径前缀  
 如果若干后续列共享同一个路径前缀，则它们将被分组到同一名称下。 如果它们使用的是不同的命名空间前缀，则即使它们被绑定到同一命名空间，也被认为是不同的路径。 在上一个查询中，FirstName、MiddleName 和 LastName 列共享同一个 EmpName 前缀。因此，它们被添加为 `EmpName` 元素的子元素。 在上一个示例中创建 `Address` 元素时也是如此。  
  
## <a name="one-column-has-a-different-name"></a>有一列具有不同的名称  
 如果列之间出现具有不同名称的列，则该列将会打破分组，如以下修改后的查询所示。 该查询通过在 FirstName 和 MiddleName 列之间添加地址列，打破了 FirstName、MiddleName 和 LastName 的分组（如上一个查询中所指定）。  
  
```sql
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E,
       Person.Contact C,
       Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH;
```  
  
 结果，查询创建两个 `EmpName` 元素。 第一个 `EmpName` 元素包含 `FirstName` 子元素，第二个 `EmpName` 元素包含 `MiddleName` 和 `LastName` 子元素。  
  
 结果如下：  
  
```xml
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
