---
title: 例如：以 XML 形式检索产品型号信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving XML information example
ms.assetid: 3828b4ca-3ab2-444f-9c58-8be6e7f064a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b48b333a5619aaad7f7f6af1c6e8cf908ba35bb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62704710"
---
# <a name="example-retrieving-product-model-information-as-xml"></a>例如：以 XML 形式检索产品型号信息
  下面的查询将返回产品型号信息。 `RAW` 子句中指定了 `FOR XML` 模式。  
  
## <a name="example"></a>示例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW;  
GO  
```  
  
 下面是部分结果：  
  
 `<row ProductModelID="122" Name="All-Purpose Bike Stand" />`  
  
 `<row ProductModelID="119" Name="Bike Wash" />`  
  
 您可以通过指定 `ELEMENTS` 指令检索以元素为中心的 XML。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 下面是结果：  
  
```  
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>  
  <Name>Bike Wash</Name>  
</row>  
```  
  
 您可以选择性地指定 `TYPE` 指令将结果作为 `xml` 类型进行检索。 `TYPE` 指令不会更改结果的内容。 只影响结果的数据类型。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, TYPE ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)  
  
  
