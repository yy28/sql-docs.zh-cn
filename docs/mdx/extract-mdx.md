---
title: 提取 (MDX) |Microsoft 文档
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
f1_keywords:
- EXTRACT
dev_langs:
- kbMDX
helpviewer_keywords:
- Extract function
ms.assetid: c0d27d31-e36e-4b7f-bb86-1e4707351392
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 103bec97eab0c80b9306acd2452a21805c169e92
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="extract-mdx"></a>Extract (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回由提取的层次结构元素中的元组构成的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression1*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression2*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **提取**函数返回的元组从提取层次结构元素组成的集。 对于指定集中的每个元组，将指定层次结构的成员提取到结果集中的新元组。 此函数始终删除重复元组。  
  
 **提取**函数执行相反操作[叉积](../mdx/crossjoin-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的查询演示如何使用**提取**函数对元组返回一组**NonEmpty**函数：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
