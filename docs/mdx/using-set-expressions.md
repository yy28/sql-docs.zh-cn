---
title: 使用集表达式 |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], set
- tuples
- set expressions [MDX]
ms.assetid: 88d65872-0cbe-4c95-b36f-e1aa4ac8ed07
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 26ebed881d32bb9d550ae9630ee7b60cb15cd153
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-set-expressions"></a>使用集表达式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  集由零个或多个元组的有序列表组成。 不包含任何元组的集称为“空集”。  
  
 一个集的完整表达式由零个或多个显式指定的元组构成，各元组放在大括号中：  
  
 {[{ *Tuple_expression* | *Member_expression* } [，{ *Tuple_expression* | *Member_expression* }]...]}  
  
 集表达式中指定的成员表达式将被转换为由一个成员构成的元组表达式。  
  
## <a name="example"></a>示例  
 以下示例说明在查询的列和行轴上使用的两个集表达式：  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 在列轴上，集  
  
 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 由 Measures 维度的两个成员组成。 在行轴上，集  
  
 {([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),  
  
 ([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),  
  
 ([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}  
  
 由三个元组组成，每个元组包含对 Product 维度的 Product Categories 层次结构和 Date 维度的 Calendar 层次结构上成员的两个显式引用。  
  
 返回集的函数的示例，请参阅[使用成员、 元组和集&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表达式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
