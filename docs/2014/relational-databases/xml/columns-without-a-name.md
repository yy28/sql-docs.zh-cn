---
title: 没有名称的列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 016d84eb5fee22e2bd8152d0a5eeb283304c456a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717179"
---
# <a name="columns-without-a-name"></a>没有名称的列
  任何没有名称的列都将成为内联列。 例如，未指定列别名的计算列或嵌套标量查询将生成没有名称的列。 如果该列属于 `xml` 类型，则将插入该数据类型实例的内容。 否则，列内容将作为文本节点插入。  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 生成此 XML。 默认情况下，针对行集中的每一行，生成的 XML 中将生成一个相应的 <`row`> 元素。 这与 RAW 模式相同。  
  
 `<row>4</row>`  
  
 以下查询将返回一个包含三列的行集。 第三列没有名称，且包含 XML 数据。 PATH 模式将插入一个 xml 类型的实例。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 下面是部分结果：  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location ...LocationID="10" ...></MI:Location>`  
  
 `<MI:Location ...LocationID="20" ...></MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>另请参阅  
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)  
  
  
