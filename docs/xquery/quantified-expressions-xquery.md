---
title: 全称量词化表达式 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9fa6c22aafdd0279c9205f36902bac1ef18c77df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="quantified-expressions-xquery"></a>限定表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  存在量词和全称量词为应用于两个序列的布尔运算符指定不同的语义。 如下表所示。  
  
 *Existential 限定符*  
 假设有两个序列，第一个序列中的某一项在第二个序列中存在匹配项，则根据所用的比较运算符，返回的值为 True。  
  
 *通用的限定符*  
 假设有两个序列，第一个序列中的每一项在第二个序列中都存在匹配项，则返回的值为 True。  
  
 XQuery 支持下列格式的限定表达式：  
  
```  
( some | every ) <variable> in <Expression> (,…) satisfies <Expression>  
```  
  
 可以在查询中使用这些表达式，来对作用于一个或多个序列上的表达式显式应用存在限定或全称限定。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，`satisfies` 子句中表达式的结果可以为：节点序列、空序列或布尔值。 限定中将使用该表达式结果的有效布尔值。 使用现有量化**某些**如果至少一个受限定符的值在满足表达式中具有 True 结果将返回 True。 使用通用量化**每个**必须具有 true，则通过限定符绑定的所有值。  
  
 例如，以下查询将检查每个\<位置 > 元素以查看它是否具有 LocationID 属性。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 因为 LocationID 是必需的特性\<位置 > 元素，也会得到预期的结果：  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 而不是使用[query （） 方法](../t-sql/xml/query-method-xml-data-type.md)，你可以使用[value （） 方法](../t-sql/xml/value-method-xml-data-type.md)到关系世界中，返回的结果，如下面的查询中所示。 如果所有生产车间都具有 LocationID 属性，则查询返回 True。 否则，查询返回 False。  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 下面的查询检查是否其中一个产品图片为小图片。 在产品目录 XML 中，存储了各种大小不同、角度各异的产品图片。 您可能希望确保每个产品目录 XML 至少包括一个小尺寸图片。 下面的查询将实现此目的：  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 下面是部分结果：  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   绑定限定表达式中的变量时不支持类型断定。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 表达式](../xquery/xquery-expressions.md)  
  
  
