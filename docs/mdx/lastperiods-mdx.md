---
title: LastPeriods （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905786"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  返回指定成员之前（包含该成员）的成员集。  
  
## <a name="syntax"></a>语法  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *编入*  
 指定期间数的有效数值表达式。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定的期间数为正，则**LastPeriods**函数返回一组成员，该成员从指定的成员表达式中以滞后于*索引*-1 的成员开头，并以指定的成员结束。 函数返回的成员数等于*Index*。  
  
 如果指定的期间数为负数，则**LastPeriods**函数返回一组成员，这些成员以指定成员开头，并以从指定成员领导（- *Index* -1）的成员结尾。 函数返回的成员数等于*Index*的绝对值。  
  
 如果指定的期间数为零，则**LastPeriods**函数返回空集。 这与**Lag**函数不同，后者会在指定0时返回指定的成员。  
  
 如果未指定成员，则**LastPeriods**函数将使用**CurrentMember**。 如果没有任何一个维度标记为 Time 维度，该函数将在不发生错误的情况下分析并执行，但将导致客户端应用程序出现单元错误。  
  
## <a name="examples"></a>示例  
 下面的示例返回 2002 会计年度第二、第三和第四会计季度的默认度量值。  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  此示例还可以用 :（冒号）运算符编写：  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 下面的示例返回 2002 会计年度第一会计季度的默认度量值。 虽然指定的期间数为三个，但是只能返回一个，因为该会计年度中没有更早的期间。  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
