---
title: "示例：重命名 &lt;row&gt; 元素 | Microsoft Docs"
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
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c907cb5e9ac3f4cd7535bea384068b08298e8b9
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="example-renaming-the-ltrowgt-element"></a>示例：重命名 &lt;row&gt; 元素
  对于结果集中的每一行，RAW 模式都生成一个元素 `<row>`。 您可以通过向 RAW 模式指定一个可选参数为该元素指定另一个名称，如该查询中所示。 该查询为行集中的每一行返回一个 <`ProductModel`> 元素。  
  
## <a name="example"></a>示例  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 结果如下： 由于查询中添加了 `ELEMENTS` 指令，因此，结果以元素为中心。  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>另请参阅  
 [将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
