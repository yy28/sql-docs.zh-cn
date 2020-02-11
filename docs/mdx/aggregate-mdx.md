---
title: 聚合（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c75ab71456dc8b7ffc3efdf6bd157693de14881
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017167"
---
# <a name="aggregate-mdx"></a>Aggregate (MDX)


  返回一个数字，该数字是通过对集表达式返回的单元进行聚合而算出的。 如果未提供数值表达式，此函数将使用为每个度量值指定的默认聚合运算符来聚合当前查询上下文中的每个度量值。 如果指定了数值表达式，此函数将先计算指定集中的每个单元的数值表达式，然后再求和。  
  
## <a name="syntax"></a>语法  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了一组空元组或一个空集，则此函数返回一个空值。  
  
 下表描述了**聚合**函数在不同聚合函数中的行为。  
  
|聚合运算符|结果|  
|--------------------------|------------|  
|SUM|返回对集求得的值之和。|  
|Count|返回对集求得的值数。|  
|Max|返回对集求得的最大值。|  
|Min|返回对集求得的最小值。|  
|半累加性聚合函数|返回将形状投影到时间轴后，对集进行的半累加性计算。|  
|Distinct Count|当切片器轴包括某个集时，构成子多维数据集的事实数据的聚合。<br /><br /> 为集的每个成员返回非重复计数。 结果取决于正在聚合的单元的安全性而不是需要计算的单元的安全性。 集的单元安全性生成错误；低于指定集的粒度的单元安全性将被忽略。 对集进行计算会生成错误。 集粒度以下的计算将被忽略。 当集包含一个成员及其一个或多个子级时，对该集进行的非重复计数将返回跨越子成员事实数据范围的非重复计数。|  
|不能聚合的属性|返回值之和。|  
|混合式聚合函数|不支持这种聚合函数，将生成错误。|  
|一元运算符|不遵从；通过求和聚合值。|  
|计算度量值|设置求解次序以确保应用计算度量值。|  
|计算成员|应用一般规则，即最后一个求解次序优先。|  
|分配|分配根据度量值聚合函数聚合。 如果度量值聚合函数是非重复计数，则对分配求和。|  
  
## <a name="examples"></a>示例  
 下面的示例返回从**艾德工作**多维`Measures.[Order Quantity]`数据集中包含在`Date`维度中的前八个月的日历年2003的成员的总和。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下面的示例对 2003 日历年第二个半期的前两个月聚合。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下面的示例根据用 Aggregate 函数计算、用户选择的 State-Province 成员值，返回上一个时期销售额下滑的分销商的计数。 **Hierarchize**和**DrillDownLevel**函数用于为 "产品" 维度中的产品类别的销售额返回值。  
  
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
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [子 &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;集计数](../mdx/count-set-mdx.md)   
 [筛选 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX&#41;&#40;属性](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
