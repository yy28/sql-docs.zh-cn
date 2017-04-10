---
title: "示例：检索雇员信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "EXPLICIT 模式"
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# 示例：检索雇员信息
  此示例检索每个雇员的雇员 ID 和雇员姓名。 在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中，可从 Employee 表的 BusinessEntityID 列获得 employeeID。 可从 Person 表中获得雇员姓名。 可使用 BusinessEntityID 列来联接表。  
  
 假定要让 FOR XML EXPLICIT 转换生成 XML，如下所示：  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 因为层次结构中有两个级别，所以应编写两个 `SELECT` 查询并应用 UNION ALL。 下面是检索 <`Employee`> 元素及其属性的值的第一个查询。 该查询将值 `1` 赋给 <`Employee`> 元素的 `Tag`，将 NULL 赋给 `Parent`，因为它是一个顶级元素。  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 下面是第二个查询。 它检索 <`Name`> 元素的值。 它将值 `2` 赋给 <`Name`> 元素的 `Tag`，将值 `1` 赋给 `Parent` 标记，从而将 <`Employee`> 标识为父元素。  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 可以使用 `UNION AL`L 组合这些查询，应用 `FOR XML EXPLICIT`，并指定所需的 `ORDER BY` 子句。 您必须先按 `BusinessEntityID` 、再按姓名对行集进行排序，以便先显示姓名中的 NULL 值。 通过执行下面这个不带 FOR XML 子句的查询，可以看到生成的通用表。  
  
 下面是最终查询：  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 下面是部分结果：  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 第一个 `SELECT` 指定所得到的行集中的列名。 这些名称形成两个列组。 列名中 `Tag` 值为 `1` 的组将 `Employee` 标识为元素，将 `EmpID` 标识为属性。 另一个列组的列中的 `Tag` 值为 `2`，它将 <`Name`> 标识为元素，将 `FName` 和 `LName` 标识为属性。  
  
 下表显示了查询生成的部分行集：  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 下面说明了如何处理通用表中的行以生成所得到的 XML 树：  
  
 第一个行标识 `Tag` 值 `1`。 因此，标识了 `Tag` 值为 `1` 的列组 `Employee!1!EmpID`。 此列将 `Employee` 标识为元素名称。 然后，将创建一个带有 `EmpID` 属性的 <`Employee`> 元素。 将为这些属性分配相应的列值。  
  
 第二个行具有 `Tag` 值 `2`。 因此，标识了列名（ `Tag` 和 `2` ）中具有 `Name!2!FName`值 `Name!2!LName`的列组。 这些列名将 `Name` 标识为元素名称。 将创建一个带有 `FName` 和 `LName` 属性的 <`Name`> 元素。 然后，将为这些属性分配相应的列值。 此行将 `1` 作为 `Parent` 标识。 此子元素将添加到上一个 <`Employee`> 元素。  
  
 对于行集中的其余行，重复此过程。 请注意，对通用表中的行进行排序很重要，因为这使得 FOR XML EXPLICIT 可以按顺序处理行集并生成所需的 XML。  
  
## 另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  