---
title: "后代 (MDX) |Microsoft 文档"
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
- DESCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Descendants function
ms.assetid: d103b0f5-e794-4828-aa57-43f6918a0749
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 82ae4fdab005443b03802f443097ddb435342c1a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="descendants-mdx"></a>Descendants (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回成员在指定级别或距离上的后代集，可以选择包括或不包括其他级别的后代。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *距离*  
 指定与指定成员距离的有效数值表达式。  
  
 *Desc_Flag*  
 指定用于区分可能后代集的说明标志的有效字符串表达式。  
  
## <a name="remarks"></a>注释  
 如果指定一个级别，则**后代**函数返回一个包含指定的成员或指定的集，由中指定的标志 （可选） 修改属于指定级别的成员的后代集*Desc_Flag*。  
  
 如果*距离*指定，则**后代**函数返回一个包含指定的成员或对指定集的指定以外，在指定的成员，（可选） 修改中指定的标志的层次结构的级别数的成员的后代集*Desc_Flag*。 通常情况下，此函数与 Distance 参数一同用于处理不规则的层次结构。 如果指定距离为零 (0)，该函数将返回仅由指定的成员或指定的集组成的集。  
  
 如果指定一个集表达式，则**后代**函数解析单独的每个成员组，并再次创建了该组。 换而言之，用于语法**后代**函数在功能上等效于 MDX[生成](../mdx/generate-mdx.md)函数。  
  
 如果不指定任何级别或距离，则将由函数所用的级别的默认值调用[级别](../mdx/level-mdx.md)函数 (<\<成员 >>。级别） 的指定成员 （如果未指定成员） 或通过调用**级别**（如果指定一组） 的一组指定每个成员函数。 如果未指定级别表达式、距离或标志，此函数将在假定使用了以下语法的情况下执行操作：  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 如果指定了级别但未指定说明标志，此函数将在假定使用了以下语法的情况下执行操作：  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 通过更改说明标志的值，可以包括或排除位于指定级别或指定距离处的后代、位于指定级别或距离之前或之后（直到叶节点为止）的子成员以及位于任何级别或距离的叶子成员。 下表描述了中允许的标志*Desc_Flag*自变量。  
  
|标志|Description|  
|----------|-----------------|  
|SELF|仅返回指定级别或指定距离处的后代成员。 如果指定级别为指定成员所在的级别，该函数将包括指定成员。|  
|AFTER|返回指定级别或指定距离处的所有从属级别的后代成员。|  
|BEFORE|返回指定成员和指定级别之间或指定距离内所有级别的后代成员。 它包括指定的成员，但不包含从指定的级别或距离的成员。|  
|BEFORE_AND_AFTER|返回指定成员所在级别的所有从属级别的后代成员。 它包括指定成员，但不包括指定级别或指定距离处的成员。|  
|SELF_AND_AFTER|返回指定级别或指定距离内的后代成员，以及指定级别或指定距离内的所有从属级别的后代成员。|  
|SELF_AND_BEFORE|返回指定级别或指定距离内的后代成员，以及指定成员和指定级别之间或指定距离内所有级别的后代成员（包括指定成员）。|  
|SELF_BEFORE_AFTER|返回指定成员所在级别的所有从属级别的后代成员（包括指定成员）。|  
|LEAVES|返回指定成员和指定级别之间或指定距离内的叶后代成员。|  
  
## <a name="examples"></a>示例  
 下面的示例返回指定成员 (United States) 以及指定成员 (United States) 和指定级别 (City) 前一个级别的成员之间的成员。该示例返回指定成员 (United States) 本身以及 State-Province 级别（City 级别的前一个级别）的成员. 此示例包括注释参数，使您可以轻松地测试此函数的其他参数。  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 下面的示例返回的每日平均值`Measures.[Gross Profit Margin]`度量值，从计算在 2003年会计年度中，在每月的天数**Adventure Works**多维数据集。 **后代**函数将返回一组日期的当前成员从确定`[Date].[Fiscal]`层次结构。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 下面的示例使用一个级别表达式并返回 Internet Sales Amount 澳大利亚，每个州-省按每个州-省返回有关澳大利亚总 Internet Sales Amount 的百分比。 此示例使用 Item 函数以从返回的集合中提取的第一个 （并且只有一个） 的元组**上级**函数。  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

