---
title: "示例：指定 HIDE 指令 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: facd99a2ba793140d70a00da10e4d3bda856db8e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="example-specifying-the-hide-directive"></a>示例：指定 HIDE 指令
  此示例说明如何使用 **HIDE** 指令。 当希望查询返回一个属性以对该查询所返回的通用表中的行进行排序，但是不希望该属性出现在最终所得到的 XML 文档中时，该指令很有用。  
  
 以下查询将构造此 XML：  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 此查询将生成所需的 XML。 此查询标识列名中 Tag 值为 1 和 2 的两个列组。  
  
 此查询使用 [xml](../../t-sql/xml/query-method-xml-data-type.md) 数据类型的 **query() 方法（xml 数据类型）** 来查询 **xml** 类型的 CatalogDescription 列，以便检索摘要说明。 此查询还使用 [xml](../../t-sql/xml/value-method-xml-data-type.md) 数据类型的 **value() 方法（xml 数据类型）** 从 CatalogDescription 列中检索 ProductModelID 值。 所得到的 XML 中不需要此值，但对生成的行集进行排序时需要此值。 因此，列名称 `[Summary!2!ProductModelID!HIDE]`包括 **HIDE** 指令。 如果 SELECT 语句中不包括此列，您将不得不按 `[ProductModel!1!ProdModelID]` 和 `[Summary!2!SummaryDescription]` xml **类型的** 对行集进行排序，并且不能在 ORDER BY 中使用 **xml** 类型列。 因此，将另外添加一个 `[Summary!2!ProductModelID!HIDE]` 列，然后在 ORDER BY 子句中指定该列。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 结果如下：  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
