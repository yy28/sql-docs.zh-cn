---
description: 使用集表达式
title: 使用集表达式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d47372f2e90f96aca99eb05bd6a2565c08567611
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491381"
---
# <a name="using-set-expressions"></a>使用集表达式


  集由零个或多个元组的有序列表组成。 不包含任何元组的集称为“空集”。  
  
 一个集的完整表达式由零个或多个显式指定的元组构成，各元组放在大括号中：  
  
 {[{ *Tuple_expression*  |  *Member_expression* } [，{ *Tuple_expression*  |  *Member_expression* }] ...]}  
  
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
  
 { ( [Product]。[产品类别]。[类别]. & [4]，[Date]。[Calendar]。[Calendar Year]。 & [2004] ) ，  
  
  ( [Product]。[产品类别]。[类别]. & [1]，[Date]。[Calendar]。[Calendar Year]。 & [2003] ) ，  
  
  ( [Product]。[产品类别]。[类别]. & [3]，[Date]。[Calendar]。[Calendar Year]。 & [2004] ) }  
  
 由三个元组组成，每个元组包含对 Product 维度的 Product Categories 层次结构和 Date 维度的 Calendar 层次结构上成员的两个显式引用。  
  
 有关返回集的函数的示例，请参阅 [使用成员、元组和集 &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)。  
  
## <a name="see-also"></a>另请参阅  
 [MDX&#41;&#40;表达式 ](../mdx/expressions-mdx.md)  
  
  
