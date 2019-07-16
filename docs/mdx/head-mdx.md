---
title: Head (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906011"
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
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **Head**函数从指定集的开头返回指定元组数目。 会保留元素的顺序。 Count 的默认值为 1。 如果指定元组数目小于 1， **Head**函数返回空集。 如果指定的元组数目超过了集中的元组数目，则此函数返回原始集。  
  
## <a name="example"></a>示例  
 以下示例根据 Reseller Gross Profit 返回产品的前五大销售子类别（与层次结构无关）。 **Head**函数用于仅返回前 5 个集的结果后将结果排序使用**顺序**函数。  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
