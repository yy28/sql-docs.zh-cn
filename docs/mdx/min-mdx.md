---
title: "最小值 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MIN
dev_langs: kbMDX
helpviewer_keywords: Min function [MDX]
ms.assetid: 9f3799c0-2502-4056-a259-053898f69b7c
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9d98884911f1da05e801214b31f3d81676380f9f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="min-mdx"></a>Min (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对集求值的数值表达式的最小值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果指定了数值表达式，则指定的数值表达式对集求值，然后返回该求值的最小值。 如果未指定数值表达式，则在指定集的成员的当前上下文中对该集求值，然后该求值的最小值。  
  
> [!NOTE]  
>  计算一组数值的最小值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略空值。  
  
## <a name="example"></a>示例  
 下面的示例返回 Adventure Works 多维数据集中每个子类别和国家/地区的最小季度销售额。  
  
```  
WITH MEMBER Measures.x AS Min   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
