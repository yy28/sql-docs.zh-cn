---
title: 多维数据集空间 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2428dbe1eba0ac652e87709a28526592cc01e6b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cube-space"></a>多维数据集空间
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  “多维数据集空间”是多维数据集属性层次结构的成员与多维数据集的度量值的乘积。 因此，多维数据集空间由多维数据集中所有属性层次结构成员和多维数据集的度量值的组合乘积确定，并且定义多维数据集的最大大小。 需要特别注意的是，此空间包括属性层次结构成员的所有可能组合；甚至包括在真实世界可能会认定为不可能的组合，例如城市是巴黎而国家/地区是英国、西班牙、日本、印度或其他地方的组合。  
  
## <a name="autoexists-and-cube-space"></a>Autoexists 和多维数据集空间  
  “autoexists”的概念将此多维数据集空间限制为那些实际存在的单元。 维度中属性层次结构的成员可能不与相同维度中其他属性层次结构的成员共存。  
  
 例如，某多维数据集具有 City 属性层次结构、Country 属性层次结构和 Internet Sales Amount 度量值，则此多维数据集的空间仅包含那些共存的成员。 例如，如果 City 属性层次结构包含城市 New York、London、Paris、Tokyo 和 Melbourne，而 Country 属性层次结构包含国家（地区）United States、United Kingdom、France、Japan 和 Australia，则该多维数据集的空间不包含 Paris 和 United States 相交处的空间（单元）。  
  
 当查询单元不存在时，不存在的单元返回空，即它们无法包含计算结果，并且您不能定义写入此空间的计算。 例如，下面的语句包含不存在的单元。  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  此查询使用 [Members (Set) (MDX)](../../../mdx/members-set-mdx.md) 函数返回列轴上 Gender 属性层次结构的成员集，并将此集与行轴上 Customer 属性层次结构的指定成员集相交。  
  
 执行前面的查询时，Aaron A. Allen 与 Female 相交处的单元将显示空。 同样，Abigail Clark 与 Male 相交处的单元也将显示空。 这些单元不存在并且不能包含值，但不存在的单元可出现在查询返回的结果中。  
  
 如果使用 [Crossjoin (MDX)](../../../mdx/crossjoin-mdx.md) 函数返回同一维度中属性层次结构中的属性层次结构成员的叉积，自动共存将限制只返回那些实际存在的元组集，而不是返回整个笛卡尔乘积的元组。 例如，运行以下查询并检查其结果。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  请注意 0 用于表示列轴的名称，它是列轴“axis(0)”的简称。  
  
 前面的查询仅为查询中每个属性层次结构的共存成员返回单元。 前面的查询还可以使用 [* (Crossjoin) (MDX)](../../../mdx/crossjoin-mdx-operator-reference.md) 函数新的 * 变量来编写。  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 前面的查询还可以通过以下方式来编写：  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 虽然结果集中的元数据将不同，但返回的单元值将是相同的。 例如，在前面的查询中，Country 层次结构已移到切片器轴（在 WHERE 子句中），因此没有显式显示在结果集中。  
  
 前面的这三个查询均阐释了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中自动共存行为所带来的影响。  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>用户定义的层次结构和多维数据集空间  
 本主题前面的示例使用属性层次结构定义了多维数据集空间中的位置。 不过，您还可以使用根据维度中属性层次结构所定义的用户定义的层次结构来定义多维数据集空间中的位置。 用户定义的层次结构是属性层次结构的层次结构，旨在帮助用户浏览多维数据集数据。  
  
 例如，上节中的 **CROSSJOIN** 查询也可以按照如下方式编写：  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 在前面的查询中，Customer 维度中的 Customer Geography 用户定义的层次结构用于定义先前使用属性层次结构定义的多维数据集空间中的位置。 可以使用属性层次结构或用户定义的层次结构来定义多维数据集空间中的同一个位置。  
  
##  <a name="AttribRelationships"></a> 属性关系和多维数据集空间  
 定义相关属性间的属性关系（通过促进相应聚合的创建）将提高查询性能，并影响与属性层次结构成员一同显示的相关属性层次结构的成员。 例如，您定义了包含 City 属性层次结构的成员的元组并且该元组未显式定义 Country 属性层次结构成员时，您可能希望默认 Country 属性层次结构成员是 Country 属性层次结构的相关成员。 不过，只有定义了 City 属性层次结构和 Country 属性层次结构之间的属性关系时，才会出现上述预期结果。  
  
 以下示例返回未显式包含在查询中的相关属性层次结构的成员。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  请注意，**WITH** 关键字与 [CurrentMember (MDX)](../../../mdx/currentmember-mdx.md) 和 [Name (MDX)](../../../mdx/name-mdx.md) 函数一起用于创建在查询中使用的计算成员。 有关详细信息，请参阅[基本 MDX 查询 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)。  
  
 在前面的查询中，返回了与 State 属性层次结构各成员相关联的 Country 属性层次结构的成员名称。 出现了预期的 Country 成员（因为定义了 City 和 Country 属性之间的属性关系）。 不过，如果在同一维度中没有定义属性层次结构间的任何属性关系，将返回“(全部)”成员，如以下查询所示。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 在前面的查询中，返回了“(全部)”成员（“All Customers”），因为 Education 和 City 间不存在任何关系。 因此，Education 属性层次结构的“(全部)”成员将是任何涉及 City 属性层次结构（未在其中显式提供 Education 成员）的元组中使用的 Education 属性层次结构的默认成员。  
  
## <a name="calculation-context"></a>计算上下文  
  
## <a name="see-also"></a>另请参阅  
 [MDX & #40; 中的重要概念Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [元组](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [使用成员、 元组，和集 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [直观合计和非直观合计](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 语言参考 & #40;MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)   
 [多维表达式 & #40;MDX & #41;引用](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
