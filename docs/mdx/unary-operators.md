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
ms.openlocfilehash: 391b39dd92011ce43b146d740b232d0c4fca6669
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193477"
---
# <a name="unary-operators"></a>一元运算符


  在多维表达式 (MDX) 中，一元运算符对单个操作数执行操作，如返回数值表达式的负值或正值。  
  
 MDX 支持下表中列出的一维运算符。  
  
|运算符|说明|  
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
  
 此外，MDX 使用特殊一元运算符来确定由 [RollupChildren](../mdx/rollupchildren-mdx.md) 函数执行的聚合操作。 有关这些特殊一元运算符的详细信息，请参阅 [向维度中添加自定义聚合](/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)。  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;MDX 语法&#41;](../mdx/operators-mdx-syntax.md)  
  
