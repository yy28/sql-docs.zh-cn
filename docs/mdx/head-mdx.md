---
title: Head (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Head function
ms.assetid: 2a909bda-1366-4537-93b0-c089554fc11f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b0e25718c55dbe433bd34438b459aed31b2097f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="head-mdx"></a>Head (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>注释  
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
  
## <a name="see-also"></a>另请参阅  
 [结尾&#40;MDX&#41;](../mdx/tail-mdx.md)   
 [项&#40;元组&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [项&#40;成员&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [级别&#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
