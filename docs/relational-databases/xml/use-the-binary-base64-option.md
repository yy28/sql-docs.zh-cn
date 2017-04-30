---
title: "使用 BINARY BASE64 选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0cfc14849df2f82429b00e8d912ceba6c74200e
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-binary-base64-option"></a>使用 BINARY BASE64 选项
  如果查询中指定了 BINARY BASE64 选项，则以 base64 编码格式返回二进制数据。 默认情况下，如果未指定 BINARY BASE64 选项，则 AUTO 模式支持二进制数据的 URL 编码。 也就是说，不返回二进制数据，而返回执行查询的数据库的虚拟根目录的相对 URL 的引用。 通过使用 SQLXML ISAPI dbobject 查询，可在后续操作中利用此引用访问实际二进制数据。 查询必须提供足够的信息（如主键列），才能标识图像。  
  
 在指定查询的过程中，如果对视图的二进制列使用了别名，将在二进制数据的 URL 编码中返回别名。 在后续操作中，别名没有意义，也不能用 URL 编码检索图像。 因此，在使用 FOR XML AUTO 模式查询视图时不要使用别名。  
  
 例如，在 SELECT 查询中，将任意列转换为二进制大型对象 (BLOB) 后，由于该列丢失了其关联的表名和列名，它将成为临时实体。 这将导致 AUTO 模式查询产生错误，因为它不知道将该值放在 XML 层次结构中的什么位置。 例如：  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 由于会转换为二进制大型对象 (BLOB)，因此以下查询将产生错误：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 解决方案是将 BINARY BASE64 选项添加到 FOR XML 子句中。 如果删除转换，此查询将生成预期的结果：  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 结果如下：  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
