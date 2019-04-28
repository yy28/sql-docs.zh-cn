---
title: 并集 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e51749416c0668ccc4760132bb860121ebae6e3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653457"
---
# <a name="union--mdx"></a>并集 (MDX)


  返回两个集的并集，并且可以选择保留重复成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>参数  
 *集表达式 1*  
 返回集的有效多维表达式 (MDX)。  
  
 *集表达式 2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数返回的并集的两个或多个指定集 *。* 使用标准语法和替代语法 1，默认情况下消除重复项。 使用标准语法中，使用**所有**标志可以集中保留重复项。 从该集的尾部删除重复项。 使用替代语法 2 时始终会保留重复项。  
  
## <a name="examples"></a>示例  
 下面的示例演示的行为**Union**函数使用每种语法。  
  
### <a name="standard-syntax-duplicates-eliminated"></a>标准语法，消除重复项  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>标准语法，保留重复项  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>替代语法 1，消除重复项  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>替代语法 2，保留重复项  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [+ &#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
