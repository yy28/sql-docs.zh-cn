---
title: DrilldownLevel (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2aa0ae2406b7e53445c9c84c98b4240f834f01c6
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740216"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  将某个集的成员深化到该集中所表示的最低级别的下一个级别。  
  
 指定级别的钻取下是可选的但如果你设置级别，你可以使用**级别表达式**或**索引级别**。 这两种参数互相排斥。 最后，如果计算成员出现在查询中，你可指定一个聚合以将这些成员包含在行集中。  
  
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
  
## <a name="remarks"></a>Remarks  
 **DrilldownLevel**函数将返回一组子成员的层次结构顺序，基于包含在指定组的成员。 指定集中原始成员的顺序将保持不变，只不过该函数的结果集中包含的所有子成员都位于其父成员下方并紧随其父成员。  
  
 根据多级别分层数据结构，你可显式选择要深化的级别。 有两种独占方式可指定级别。 第一种方法是将设置**level_expression**参数使用一个 MDX 表达式，返回的级别，另一种方法是指定**索引**自变量，使用指定的级别数由数值表达式。  
  
 如果指定了级别表达式，函数将只检索指定级别的成员的子成员，然后用这些子成员按层次结构顺序构造一个集。 如果指定了级别表达式且该级别没有成员，则忽略该级别表达式。  
  
 如果指定了索引值，此函数将基于从零开始的索引只检索指定集中引用的层次结构的下一最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 如果级别表达式和索引值均未指定，此函数将只检索指定集中引用的第一个维度的最低级别成员的子成员，然后用这些子成员按层次结构顺序构造一个集。  
  
 查询的 XMLA 属性 MdpropMdxDrillFunctions，您可以验证服务器提供钻函数; 支持的级别请参阅[支持 XMLA 属性&#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)有关详细信息。  
  
## <a name="examples"></a>示例  
 你可使用 Adventure Works 多维数据集在 SSMS 中的 MDX 查询窗口中尝试下面的示例。  
  
 **示例 1 – 演示最小的语法**  
  
 第一个示例显示的最小语法**DrilldownLevel**。 所需的唯一参数是集表达式。 请注意，运行此查询时，你会在父 [所有类别] 和下一个级别的成员: [附件] [自行车]，依此类推。 尽管此示例很简单，它演示了基本的用途**DrilldownLevel**函数，向下下面的下一步级别钻取。  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 示例 2 – 使用显式索引级别的替代语法  
  
 此示例演示了替代语法，该语法通过数字表达式指定索引级别。 在本例中，索引级别是 0。 对于从零开始的索引，这是最低级别。  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 请注意，结果集与之前的查询完全相同。 通常，不必设置索引级别，除非你想要从特定级别开始深化。 将索引值设置为 1，然后设置为 2，重新运行之前的查询。 索引值设置为 1 时，你会看到深化从层次结构中的第二个级别开始。 索引值设置为 2 时，深化从第三个级别（本示例中的最高级别）开始。 数字表达式越高，索引级别越高。  
  
 **示例 3 – 演示一个级别表达式**  
  
 下面的示例显示如何使用级别表达式。 基于代表层次结构的集，使用级别表达式可让你在层次结构中选择开始深化的级别。  
  
 在此示例中，向下钻取的级别 [City]，在作为启动的第二个参数**DrilldownLevel**函数。 运行此查询时，深化从华盛顿和俄勒冈州的 [City] 级别开始。 每个**DrilldownLevel**函数，结果集还包括在下一步级别下 [邮政代码] 的成员。  
  
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
  
 **示例 4 – 包括计算的成员**  
  
 一个计算的成员，将出现在结果底部设置添加时的最后一个示例所示**include_calculated_members**标志。 请注意，该标志被指定为第四个参数。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
