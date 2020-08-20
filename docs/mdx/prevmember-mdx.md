---
description: PrevMember (MDX)
title: PrevMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f02dfca925fce4399bb9f0c4a8c7ff1e005e598
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471659"
---
# <a name="prevmember-mdx"></a>PrevMember (MDX)


  返回指定成员所在级别的上一个成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.PrevMember   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **PrevMember**函数返回与指定成员位于同一级别的上一个成员。  
  
## <a name="example"></a>示例  
 下面的示例显示一个简单查询，该查询使用 **PrevMember** 函数来显示紧靠在行轴上的当前成员之前的成员的名称：  
  
 `WITH MEMBER MEASURES.PREVMEMBERDEMO AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.PREVMEMBER.NAME`  
  
 `SELECT MEASURES.PREVMEMBERDEMO ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 下面的示例根据用 Aggregate 函数计算、用户选择的 State-Province 成员值，返回上一个时期销售额下滑的分销商的计数。 **Hierarchize**和**DrillDownLevel**函数用于为 "产品" 维度中的产品类别的销售额返回值。 **PrevMember**函数用于将当前时间段与上一个时间段进行比较。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
