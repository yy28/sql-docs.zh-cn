---
title: "BottomPercent (MDX) |Microsoft 文档"
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
- BOTTOMPERCENT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomPercent function
ms.assetid: c04866e6-e6dd-4ed1-ae79-c718c194930c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 416c5c68b30b72352ffc95658d0f34cc77f8e9af
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  按升序对集进行排序，并返回一个最小值元组集，该元组集的累积合计等于或大于指定的百分比。  
  
## <a name="syntax"></a>语法  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *百分比*  
 有效的数值表达式，指定要返回的元组的百分比。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 **BottomPercent**函数计算的指定数值表达式对集以升序进行排序指定集求得的总和。 然后，该函数返回合计值累积百分比至少达到指定百分比的最小值元素。 该函数返回累积合计至少达到指定百分比的最小子集。 返回的元素按从大到小的顺序排序。  
  
> [!IMPORTANT]  
>  **BottomPercent**函数，如[TopPercent](../mdx/toppercent-mdx.md)函数中，始终中断层次结构。 有关详细信息，请参阅 Order 函数。  
  
## <a name="example"></a>示例  
 下面的示例返回 2003 会计年度 Geography 维度 Geography 层次结构中 City 级别的最小成员集（对于 Bike 类别），其 Reseller Sales Amount 度量值的累积合计至少是累积合计的 15%（从具有最小销售额的集的成员开始）。  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

