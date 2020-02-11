---
title: 示例：指定 ELEMENT 指令和实体编码 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28e0e9f808820acc1959ccc11266174e5610600c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63287242"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>示例：指定 ELEMENT 指令和实体编码
  下面的这个示例说明了 **ELEMENT** 和 **XML** 指令之间的差异。 **ELEMENT** 指令会实体化数据，但 **XML** 指令则不会。 在查询中向 \<Summary> 元素分配了 XML `<Summary>This is summary description</Summary>`。  
  
 请看下面的查询：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription!ELEMENT]  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        NULL,  
       '<Summary>This is summary description</Summary>'  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 结果如下： 在结果中，对摘要说明进行了实体化。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription><Summary>This is summary description</Summary></SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 现在，如果在列名 **中指定** XML `Summary!2!SummaryDescription!XML`指令而不是 **ELEMENT** 指令，则您将收到未经实例化的摘要说明。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <Summary>This is summary description</Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 以下查询使用 **xml** 类型的 **query()** 方法（而不是分配一个静态 XML 值）从 **xml** 类型的 CatalogDescription 列中检索产品型号摘要说明。 因为已经知道结果为 **xml** 类型，所以未进行实体化。  
  
```  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
       (SELECT CatalogDescription.query('  
            declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
          /pd:ProductDescription/pd:Summary'))  
FROM     Production.ProductModel  
WHERE    CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],Tag  
FOR XML EXPLICIT  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)  
  
  
