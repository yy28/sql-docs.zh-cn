---
title: 带有指定为 data() 的路径的列名 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e48e7addad583ef6a9b9efb8163f592f5c33bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059535"
---
# <a name="column-names-with-the-path-specified-as-data"></a>带有指定为 data() 的路径的列名
  如果被指定为列名的路径为 data()，则在生成的 XML 中，该值将被作为一个原子值来处理。 如果序列化中的下一项也是一个原子值，则将向 XML 中添加一个空格字符。 这在创建列表类型化元素值和属性值时很有用。 以下查询将检索产品型号 ID、名称和该产品型号中的产品列表。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 嵌套 SELECT 语句将检索产品 ID 列表。 它指定 data() 作为产品 ID 列名。 由于 PATH 模式为行元素名指定了空字符串，因此不会生成行元素。 相反，将返回值以分配给父级 SELECT 的 <`ProductModelData`> 行元素的 ProductIDs 属性。 结果如下：  
  
 `<ProductModelData ProductModelID="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 888 889 890 891 892 893" />`  
  
## <a name="see-also"></a>另请参阅  
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)  
  
  
