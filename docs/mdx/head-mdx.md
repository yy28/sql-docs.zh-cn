---
title: Head (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 05cfcb3c23a0369f010b8440d4a27e94ffacdb21
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740476"
---
# <a name="head-mdx"></a>Head (MDX)


  返回集中指定数目的前几个元素，同时保留重复项。  
  
## <a name="syntax"></a>语法  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>Remarks  
 **头**函数从指定集的开头返回指定的数目的元组。 会保留元素的顺序。 Count 的默认值为 1。 如果指定的元组数是等于或大于 1，**头**函数返回一个空集。 如果指定的元组数目超过了集中的元组数目，则此函数返回原始集。  
  
## <a name="example"></a>示例  
 以下示例根据 Reseller Gross Profit 返回产品的前五大销售子类别（与层次结构无关）。 **头**函数用于在结果中返回仅的前 5 集后使用排序结果,**顺序**函数。  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [结尾&#40;MDX&#41;](../mdx/tail-mdx.md)   
 [项&#40;元组&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [项&#40;成员&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [级别&#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
