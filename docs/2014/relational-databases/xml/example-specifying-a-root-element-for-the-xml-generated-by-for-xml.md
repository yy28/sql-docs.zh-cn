---
title: 示例：为 FOR XML 生成的 XML 指定根元素 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 95efd8d52ec89c3184a882d32add5e17449d343d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125811"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>示例：为 FOR XML 生成的 XML 指定根元素
  通过在 `ROOT` 查询中指定 `FOR XML` 选项，您可以为生成的 XML 请求一个顶级元素，如该查询中所示。 为 `ROOT` 指令指定的参数提供了根元素名称。  
  
## <a name="example"></a>示例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 结果如下：  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>请参阅  
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)  
  
  