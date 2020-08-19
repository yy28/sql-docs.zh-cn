---
description: Head (MDX)
title: Head (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51a832bf38d3834c44f9b31f5bbfd27833d6d691
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429919"
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
 **Head**函数从指定集的开头返回指定数量的元组。 会保留元素的顺序。 Count 的默认值为 1。 如果指定的元组数目小于1，则 **Head** 函数返回空集。 如果指定的元组数目超过了集中的元组数目，则此函数返回原始集。  
  
## <a name="example"></a>示例  
 以下示例根据 Reseller Gross Profit 返回产品的前五大销售子类别（与层次结构无关）。 **Head**函数用于在使用**Order**函数对结果进行排序后，仅返回结果中的前5个集。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [项 &#40;元组&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [项 &#40;成员&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [&#40;MDX 的排名&#41;](../mdx/rank-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
