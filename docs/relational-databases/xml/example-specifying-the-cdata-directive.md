---
title: 示例：指定 CDATA 指令 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- CDATA directive
ms.assetid: 949071e6-787f-480d-bb86-3ac16a027af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6c6c2f5e19e22cdff4b7f9ca282fc3406efd3fc
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664783"
---
# <a name="example-specifying-the-cdata-directive"></a>示例：指定 CDATA 指令
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  如果指令设置为 **CDATA**，则不对包含的数据进行实体编码，而是将其放入 CDATA 部分。 **CDATA** 属性必须没有名称。  
  
 以下查询将产品型号摘要说明包装在 CDATA 部分中。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        '<Summary>This is summary description</Summary>'     
            as [ProductModel!1!!CDATA] -- no attribute name so ELEMENT assumed  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 结果如下：  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
   <![CDATA[<Summary>This is summary description</Summary>]]>  
</ProductModel>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
