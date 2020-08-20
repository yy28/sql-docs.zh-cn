---
description: 串联运算符
title: 串联运算符 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 54e935e3491156c04e1a4b9e704b655a7151fdb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466489"
---
# <a name="concatenation-operators"></a>串联运算符


  串联运算符为加号 (+)。 可以将两个或更多个字符串合并或串联成一个字符串， 还可以串联二进制字符串。  
  
 下列代码是串联运算符的一个示例，在此示例中，用串联运算符将产品名称与产品的唯一名称连接起来：  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>语言注意事项  
 当串联中使用的字符串具有相同的排序规则时，生成的串联字符串具有与输入字符串相同的排序规则。 当串联中使用的字符串具有不同的排序规则时，生成的串联字符串的排序规则由排序规则的优先顺序规则确定。 有关详细信息，请参阅[语言和排序规则 (Analysis Services)](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services)。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [运算符 &#40;MDX 语法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
