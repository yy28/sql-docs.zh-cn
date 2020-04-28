---
title: ParallelPeriod （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020699"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  返回上一期间中与指定成员具有相同的相对位置的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *索引*  
 指定要滞后的并行期间数的有效数值表达式。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 与[同级](../mdx/cousin-mdx.md)函数类似， **ParallelPeriod**函数比时序更密切地相关。 **ParallelPeriod**函数采用指定级别的指定成员的祖先，查找具有指定 lag 的祖先的同级，最后返回同级的后代中指定成员的并行期间。  
  
 **ParallelPeriod**函数具有以下默认值：  
  
-   如果级别表达式和成员表达式均未指定，则默认成员值为第一个维度上第一个层次结构的当前成员，该维度的度量值组中的时间类型为*Time* 。  
  
-   如果指定了级别表达式，但未指定成员表达式，则默认成员值为*Level_Expression*。**CurrentMember**。  
  
-   默认索引值为 1。  
  
-   默认级别为指定成员的父级别。  
  
 **ParallelPeriod**函数等效于下面的 MDX 语句：  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>示例  
 下面的示例以季度级别为基准并以三个期间为间隔，返回了 October 2003（2003 年 10 月）的并行期间，即 2003 年 1 月。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下面的示例以半期级别为基准并以三个期间为间隔，返回了 October 2003（2002 年 10 月）的并行期间，即 2002 年 4 月。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
