---
title: 没有名称的列 | Microsoft Docs
description: 了解生成 XML 时 SQL Server 如何处理不带名称的列。
ms.custom: ''
ms.date: 08/01/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: rothja
ms.author: jroth
ms.openlocfilehash: 878f1a89240f8df02eaafb34cef09540b884b614
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2020
ms.locfileid: "87523439"
---
# <a name="columns-without-a-name"></a>没有名称的列
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  任何没有名称的列都将成为内联列。 例如，未指定列别名的计算列或嵌套标量查询将生成没有名称的列。 如果该列属于 **xml** 类型，则将插入该数据类型实例的内容。 否则，列内容将作为文本节点插入。  
  
```sql
SELECT 2+2  
FOR XML PATH  
```  
  
 生成此 XML。 默认情况下，对于行集中的每一行，生成的 XML 中都会生成一个 `<row>` 元素。 这与 RAW 模式相同。  
  
 `<row>4</row>`  
  
 以下查询将返回一个包含三列的行集。 第三列没有名称，且包含 XML 数据。 PATH 模式将插入一个 xml 类型的实例。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query(
           'declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
            /MI:root/MI:Location   
           ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 下面是部分结果：  
  
```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location ...LocationID="10" ...></MI:Location>
  <MI:Location ...LocationID="20" ...></MI:Location>
  ...
</row>
```

## <a name="see-also"></a>另请参阅  
 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
