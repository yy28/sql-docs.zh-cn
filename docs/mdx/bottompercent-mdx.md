---
title: BottomPercent (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a627ea8e5dd7a8f8266fcf0ea374e6abcde4bdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208797"
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)


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
  
## <a name="remarks"></a>备注  
 **BottomPercent**函数计算指定数值表达式对指定集，对该集按升序计算的总和。 然后，该函数返回合计值累积百分比至少达到指定百分比的最小值元素。 该函数返回累积合计至少达到指定百分比的最小子集。 返回的元素按从大到小的顺序排序。  
  
> [!IMPORTANT]  
>  **BottomPercent**函数一样， [TopPercent](../mdx/toppercent-mdx.md)函数中，总是会在层次结构。 有关详细信息，请参阅 Order 函数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
