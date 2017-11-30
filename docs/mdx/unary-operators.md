---
title: "一元运算符 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: unary operators
ms.assetid: bf1b5518-6040-4484-9ce8-79c0eb4373a9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a2dd50160dbe0185056988cfd866f119d7e330c4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="unary-operators"></a>一元运算符
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多维表达式 (MDX) 中，一元运算符对单个操作数执行操作，如返回数值表达式的负值或正值。  
  
 MDX 支持下表中列出的一维运算符。  
  
|运算符|Description|  
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
  
 MDX 此外，使用特殊的一元运算符以确定执行的聚合操作[RollupChildren](../mdx/rollupchildren-mdx.md)函数。 有关这些特殊的一元运算符的详细信息，请参阅[向维度中添加自定义聚合](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md)。  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;MDX 语法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
