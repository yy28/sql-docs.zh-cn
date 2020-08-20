---
description: 一元运算符
title: 一元运算符 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32f5084190642bd4237d225404c92f0c4754da7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466469"
---
# <a name="unary-operators"></a>一元运算符


  在多维表达式 (MDX) 中，一元运算符对单个操作数执行操作，如返回数值表达式的负值或正值。  
  
 MDX 支持下表中列出的一维运算符。  
  
|操作员|描述|  
|--------------|-----------------|  
|[-（负）](../mdx/negative-mdx.md)|返回数值表达式的负值。|  
|[+（正）](../mdx/positive-mdx.md)|返回数值表达式的正值。|  
  
 下面的示例显示了如何使用一维运算符返回度量值的负值：  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 此外，MDX 使用特殊一元运算符来确定由 [RollupChildren](../mdx/rollupchildren-mdx.md) 函数执行的聚合操作。 有关这些特殊一元运算符的详细信息，请参阅 [向维度中添加自定义聚合](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)。  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;MDX 语法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
