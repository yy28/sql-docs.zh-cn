---
title: DrilldownLevel (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b9c623a1e99053e796609dc82f27519f27c07a9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049287"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  将某个集的成员深化到该集中所表示的最低级别的下一个级别。  
  
 指定的级别要向下钻取列表是可选的但如果您设置级别，可以使用**级别表达式**或**索引级别**。 这两种参数互相排斥。 最后，如果计算成员出现在查询中，你可指定一个聚合以将这些成员包含在行集中。  
  
## <a name="syntax"></a>语法  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 （可选）。 显式标识要深化的级别的 MDX 表达式。 如果指定了级别表达式，请跳过下面的索引参数。  
  
 *Index*  
 （可选）。 有效的数值表达式，它指定在集中要深化的层次结构编号。 你可使用索引级别而不是 Level_Expression 显式标识要深化的级别。  
  
 *Include_Calc_Members*  
 （可选）。 指示是否在深化级别包括计算成员（如果存在）的标志。  
  
## <a name="remarks"></a>备注  
 **DrilldownLevel**函数的层次结构顺序，根据包含在指定集中的成员返回一组子成员。 指定集中原始成员的顺序将保持不变，只不过该函数的结果集中包含的所有子成员都位于其父成员下方并紧随其父成员。  
  
 根据多级别分层数据结构，你可显式选择要深化的级别。 有两种独占方式可指定级别。 第一种方法是设置**level_expression**自变量使用 MDX 表达式，返回的级别，另一种方法是指定**索引**参数，使用数值表达式，指定按编号的级别。  
  
 如果指定了级别表达式，函数将只检索指定级别的成员的子成员，然后用这些子成员按层次结构顺序构造一个集。 如果指定了级别表达式且该级别没有成员，则忽略该级别表达式。  
  
 如果指定了索引值，此函数将基于从零开始的索引只检索指定集中引用的层次结构的下一最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 如果级别表达式和索引值均未指定，此函数将只检索指定集中引用的第一个维度的最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
## <a name="examples"></a>示例  
 你可使用 Adventure Works 多维数据集在 SSMS 中的 MDX 查询窗口中尝试下面的示例。  
  
 **示例 1-演示最简语法**  
  
 第一个示例演示最简语法**DrilldownLevel**。 所需的唯一参数是集表达式。 请注意，运行此查询时，你着手的父 [All Categories] 和下一级别的成员: [Accessories] 和 [Bikes] 等。 虽然这个示例很简单，但它所演示的基本用途**DrilldownLevel**函数，即深化到下一个级别。  
  
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
  
 在此示例中，向下钻取的级别开始 [City] 作为第二个参数的**DrilldownLevel**函数。 运行此查询时，深化从华盛顿和俄勒冈州的 [City] 级别开始。 每个**DrilldownLevel**函数，结果集还包括下 [Postal codes] 下一级别的成员。  
  
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
  
 **示例 4-包括计算的成员**  
  
 添加时，设置结果的底部将显示计算的成员的最后一个示例所示**include_calculated_members**标志。 请注意，该标志被指定为第四个参数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
