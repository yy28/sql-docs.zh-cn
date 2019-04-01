---
title: 例如：使用 ELEMENTS 指令指定 XSINIL | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b708e9ff71bd7f7599339ae2eebc0377b0c5fb1f
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512914"
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>例如：指定带有 ELEMENTS 指令的 XSINIL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  以下查询将指定 `ELEMENTS` 指令以根据查询结果生成以元素为中心的 XML。  
  
## <a name="example"></a>示例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 下面是部分结果：  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 由于 `Color` 列针对某些产品包含 Null 值，因此生成的 XML 将不会生成对应的 <`Color`> 元素。 通过添加 `XSINIL` 和 `ELEMENTS` 指令，甚至可以针对结果集中的 NULL 颜色值生成 <`Color`> 元素。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 下面是部分结果：  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
