---
title: 联合（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 170e3764795e1bb6db3fc9589ecf1fe486078633
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097303"
---
# <a name="union--mdx"></a>联合（MDX）


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
 *集表达式1*  
 返回集的有效多维表达式 (MDX)。  
  
 *集表达式2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数返回两个或更多个指定集的并集。 对于标准语法和替代语法1，默认情况下将消除重复项。 使用标准语法，使用**ALL**标志可在联接集内保留重复项。 从该集的尾部删除重复项。 使用替代语法 2 时始终会保留重复项。  
  
## <a name="examples"></a>示例  
 下面的示例演示了使用每个语法的**联合**函数的行为。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [+ &#40;联合&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
