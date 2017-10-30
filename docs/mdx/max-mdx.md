---
title: "最大值 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MAX
dev_langs:
- kbMDX
helpviewer_keywords:
- Max function [MDX]
ms.assetid: 745c2b3e-022b-471a-ac16-e39ecb3297ea
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd3151c2fec5a7fecee1a3ff0b1c2b988f9e08bc
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="max-mdx"></a>Max (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对集求值的数值表达式的最大值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Max( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 如果指定了数值表达式，则对集计算指定数值表达式的值，然后返回求得的最大值。 如果没有指定数值表达式，则在指定集成员的当前上下文中计算指定集，然后返回求得的最大值。  
  
> [!NOTE]  
>  计算一组数值的最大值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略空值。  
  
## <a name="example"></a>示例  
 下面的示例将返回 Adventure Works 多维数据集中每个季度、子类别和国家（地区）的最大每月销售额。  
  
```  
WITH MEMBER Measures.x AS Max   
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

