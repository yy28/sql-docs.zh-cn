---
description: DrilldownLevel (MDX)
title: DrilldownLevel (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bc939e8aa055a2a36216a6c94fd032e561cbabf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484000"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  将某个集的成员深化到该集中所表示的最低级别的下一个级别。  
  
 指定向下钻取的级别是可选的，但如果设置了级别，则可以使用 **级别表达式** 或 **索引级别**。 这两种参数互相排斥。 最后，如果计算成员出现在查询中，你可指定一个聚合以将这些成员包含在行集中。  
  
## <a name="syntax"></a>语法  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 （可选）。 显式标识要深化的级别的 MDX 表达式。 如果指定了级别表达式，请跳过下面的索引参数。  
  
 *索引*  
 （可选）。 有效的数值表达式，它指定在集中要深化的层次结构编号。 你可使用索引级别而不是 Level_Expression 显式标识要深化的级别。  
  
 *Include_Calc_Members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>备注  
 **DrilldownLevel**函数基于指定集内包含的成员按层次结构顺序返回一组子成员。 指定集中原始成员的顺序将保持不变，只不过该函数的结果集中包含的所有子成员都位于其父成员下方并紧随其父成员。  
  
 根据多级别分层数据结构，你可显式选择要深化的级别。 有两种独占方式可指定级别。 第一种方法是使用返回级别的 MDX 表达式来设置 **level_expression** 参数，另一种方法是指定 **索引** 参数，使用数值表达式指定级别的按数字。  
  
 如果指定了级别表达式，函数将只检索指定级别的成员的子成员，然后用这些子成员按层次结构顺序构造一个集。 如果指定了级别表达式且该级别没有成员，则忽略该级别表达式。  
  
 如果指定了索引值，此函数将基于从零开始的索引只检索指定集中引用的层次结构的下一最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 如果级别表达式和索引值均未指定，此函数将只检索指定集中引用的第一个维度的最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅 [&#40;xmla&#41;支持的 Xmla 属性 ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
## <a name="examples"></a>示例  
 你可使用 Adventure Works 多维数据集在 SSMS 中的 MDX 查询窗口中尝试下面的示例。  
  
 **示例 1-演示最少语法**  
  
 第一个示例显示了 **DrilldownLevel**的最小语法。 所需的唯一参数是集表达式。 请注意，运行此查询时，您将获得下一级别的父 [所有类别] 和成员： [附件]、[自行车] 等。 尽管此示例很简单，但它演示了 **DrilldownLevel** 函数的基本用途，该函数可深化到下一级别。  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 示例 2-使用显式索引级别的替代语法  
  
 此示例演示了替代语法，该语法通过数字表达式指定索引级别。 在本例中，索引级别是 0。 对于从零开始的索引，这是最低级别。  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 请注意，结果集与之前的查询完全相同。 通常，不必设置索引级别，除非你想要从特定级别开始深化。 将索引值设置为 1，然后设置为 2，重新运行之前的查询。 索引值设置为 1 时，你会看到深化从层次结构中的第二个级别开始。 索引值设置为 2 时，深化从第三个级别（本示例中的最高级别）开始。 数字表达式越高，索引级别越高。  
  
 **示例 3-演示级别表达式**  
  
 下面的示例显示如何使用级别表达式。 基于代表层次结构的集，使用级别表达式可让你在层次结构中选择开始深化的级别。  
  
 在此示例中，向下钻取级别以 [City] 开头，作为 **DrilldownLevel** 函数的第二个参数。 运行此查询时，深化从华盛顿和俄勒冈州的 [City] 级别开始。 根据 **DrilldownLevel** 函数，结果集还包括下一个级别的成员，即 [邮政编码]。  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **示例 4-包括计算成员**  
  
 最后一个示例显示一个计算成员，当您添加 **include_calculated_members** 标志时，该成员将出现在结果集的底部。 请注意，该标志被指定为第四个参数。  
  
 此示例有效的原因是计算成员所处的级别与非计算成员相同。 计算成员 [West Coast] 由来自 [United States] 的成员以及 [United States] 的下一个级别的所有成员组成。  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 如果仅删除标志，然后重新运行该查询，你会得到与减去计算成员 [West Coast] 相同的结果。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
