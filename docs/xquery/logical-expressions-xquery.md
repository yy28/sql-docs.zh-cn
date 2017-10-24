---
title: "逻辑表达式 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6a7c65f0c5758bdc8f50582d6d2288f9918677b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="logical-expressions-xquery"></a>逻辑表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支持逻辑**和**和**或**运算符。  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 测试表达式中，`expression1,``expression2`中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可能会导致空序列、 一个或多个节点的序列或一个单个的布尔值。 根据结果，按照下列方式确定它们的有效布尔值：  
  
-   如果测试表达式的结果是空序列，则表达式的结果为 False。  
  
-   如果测试表达式的结果是单个布尔值，则此值便为表达式的结果。  
  
-   如果测试表达式的结果是包含一个或多个节点的序列，则表达式的结果为 True。  
  
-   否则，将引发静态错误。  
  
 逻辑**和**和**或**运算符随后会应用于使用标准的逻辑语义表达式的生成布尔值。  
  
 下面的查询从产品目录中检索某个特定产品型号的正面小图片 <`Picture`> 元素。 请注意，对于每一个产品说明文档，目录都可以存储具有不同属性（如大小和角度）的一个或多个产品图片。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 结果如下：  
  
```  
<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 表达式](../xquery/xquery-expressions.md)  
  
  

