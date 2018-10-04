---
title: 名称指定为通配符的列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ff6bcd9379e6e20351dacee75cb92e56b79d374
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056147"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>名称指定为通配符的列
  如果指定的列名是一个通配符 (\*)，则插入此列的内容时就像没有指定列名那样插入。 如果此列为非`xml`类型列，则列内容将插入作为文本节点，如下面的示例中所示：  
  
```  
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
  
 `<row EmpID="1">KenJSánchez</row>`  
  
 如果此列的类型为 `xml`，则将插入相应的 XML 树。 例如，下面的查询将“*”指定为一个列的列名，该列包含由针对 Instructions 列的 XQuery 所返回的 XML。  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 结果如下： 插入 XQuery 所返回的 XML 时不带包装元素。  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>请参阅  
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)  
  
  
