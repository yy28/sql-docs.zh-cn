---
title: 次序 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055678"
---
# <a name="order-mdx"></a>Order (MDX)


  排列指定集的成员，可以选择保留或打乱原有的层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *String_Expression*  
 通常是单元坐标（返回以字符串表示的数字）的有效多维表达式 (MDX) 的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 **顺序**函数可以是层次结构 (通过使用指定**ASC**或**DESC**标志) 或非层次结构 (通过使用指定**BASC**或**BDESC**标志; **B**代表"打乱层次结构")。 如果**ASC**或**DESC**指定，则**顺序**函数首先排列是根据其位置在层次结构中的成员，然后每个级别进行排序。 如果**BASC**或**BDESC**指定，则**顺序**函数排列集中而不考虑层次结构成员。 指定任何标志， **ASC**是默认值。  
  
 如果**顺序**函数用于使用一组在两个或多个层次结构执行叉积，并**DESC**使用标志，只有在集中的最后一个层次结构的成员进行排序。 这与 Analysis Services 2000 不同，后者对集合中的所有层次结构进行排序。  
  
## <a name="examples"></a>示例  
 下面的示例返回从**Adventure Works**多维数据集，在日期维度的 Calendar 层次结构中所有日历季度的分销商订单数。**顺序**函数重新为 ROWS 轴的集进行排序。 **顺序**函数进行排序的集`[Reseller Order Count]`降序所确定的那样的层次结构顺序`[Calendar]`层次结构。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 请注意如何在此示例中，当**DESC**标志将变为**BDESC**、 层次结构被破坏，而不考虑层次结构返回日历季度的列表：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 **子集**函数用于后使用排序结果集中返回仅前 5 个元组**顺序**函数。  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 下面的示例使用**排名**函数进行排名的 City 层次结构成员基于 Reseller Sales Amount 度量值，然后按照排名高低显示它们。 通过使用**顺序**函数先对 City 层次结构的成员的集，排序是仅执行一次，并再后跟线性扫描之前显示按排序顺序。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例中是唯一的使用的集返回的产品数量**顺序**函数进行排序之前使用的非空元组**筛选器**函数。 **CurrentOrdinal**函数用于比较和消除等同值。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 若要了解如何**DESC**标志使用元组集的是，请首先考虑以下查询的结果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 行轴上您可以看到，Sales Territory Groups 已按降序按 Tax Amount，如下所示：North America、 Europe、 Pacific、 na。 现在，看会发生什么情况我们叉积的一套产品子类别的 Sales Territory Groups 集并应用**顺序**功能的方式相同，按如下所示：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 而按降序，层次结构顺序排序的一套产品子类别 Sales Territory Groups 现在未排序，并将显示在层次结构的顺序出现：欧洲、 NA、 North America 和 Pacific。 其原因在于，仅对元组集合中最后一个层次结构 Product Subcategories 进行了排序。 若要重现 Analysis Services 2000 的行为，请使用一系列嵌套**生成**函数对每个组进行排序，才使用它执行叉积，例如：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
