---
title: "中值 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEDIAN
dev_langs: kbMDX
helpviewer_keywords: Median function
ms.assetid: 7a326a3f-0123-45c4-9b18-31f83b90d986
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 44e92801c99d7ca2990d656fda13b395a9b0229b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="median-mdx"></a>Median (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对集求值的数值表达式的中值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果指定了数值表达式，则对集计算指定数值表达式的值，然后返回求得的中值。 如果没有指定数值表达式，则在指定集成员的当前上下文中计算指定集，然后返回求得的中值。  
  
 中值是一组有序数值的中间值。 （中值不同于平均值，平均值是一组数值的总和除以这组数值的个数所得的值）。 中值是通过选择最小值以使这组数值中至少有一半值不大于所选的值来确定的。 如果这组数值的个数为奇数，则中值对应于单个值。 如果这组数值的个数为偶数，则中值对应于两个中间值的和除以 2 所得的值。  
  
> [!NOTE]  
>  计算一组有序数值的中值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略空值。  
  
## <a name="example"></a>示例  
 下例将返回 Adventure Works 多维数据集中每个季度、每个子类别和每个国家（地区）的每月销售额中值。  
  
```  
WITH MEMBER Measures.x AS Median   
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
  
  
