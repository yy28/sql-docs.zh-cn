---
title: ParallelPeriod (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cde031af19fff309520cd72e145b6c04dc19d9c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580819"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回上一期间中与指定成员具有相同的相对位置的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Index*  
 指定要滞后的并行期间数的有效数值表达式。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 尽管类似于[Cousin](../mdx/cousin-mdx.md)函数， **ParallelPeriod**函数更紧密地与时间序列。 **ParallelPeriod**函数指定的级别，获取指定的成员的祖先、 查找与指定的滞后的上级的同级和最后返回指定成员的同级元素的后代中的并行期间。  
  
 **ParallelPeriod**函数具有以下默认值：  
  
-   如果指定既不是级别表达式，也不是成员表达式，则默认成员值是上一种类型的第一个维度的第一个层次结构的当前成员*时间*度量值组中。  
  
-   如果指定一个级别表达式，但未指定一个成员表达式，该默认成员值将*Level_Expression*。**Hierarchy.CurrentMember**。  
  
-   默认索引值为 1。  
  
-   默认级别为指定成员的父级别。  
  
 **ParallelPeriod**函数等同于以下的 MDX 语句：  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
