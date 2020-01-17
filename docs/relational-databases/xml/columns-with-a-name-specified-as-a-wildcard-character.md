---
title: 指定包含通配符的列 (SQLXML) | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: b75c343c675e74f7ce26bb1b1787bfbef99b7623
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258378"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>名称指定为通配符的列

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

如果指定的列名是一个通配符 (\*)，则插入此列的内容时就像没有指定列名那样插入。 如果此列不是**xml** 类型的列，则此列的内容将作为文本节点插入，如下例所示：  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
  INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 结果如下：  

```xml
<row EmpID="1">KenJSánchez</row>
```

 如果此列的类型为 **xml** ，则将插入相应的 XML 树。 例如，下面的查询将“*”指定为一个列的列名，该列包含由针对 Instructions 列的 XQuery 所返回的 XML。  
  
```sql
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
```  
  
 结果如下： 插入 XQuery 所返回的 XML 时不带包装元素。  

```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location LocationID="10">...</MI:Location>
  <MI:Location LocationID="20">...</MI:Location>
  ...
</row>
```

## <a name="see-also"></a>另请参阅  
 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
