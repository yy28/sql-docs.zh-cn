---
title: 顺序（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
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
 **Order**函数可以是层次结构（使用**ASC**或**DESC**标志指定）或非层次结构（使用**BASC**或**BDESC**标志指定的）， **B**代表 "中断层次结构"。 如果指定了**ASC**或**DESC** ， **Order**函数将根据成员在层次结构中的位置对其进行排列，然后对每个级别进行排序。 如果指定了**BASC**或**BDESC** ，则**Order**函数将排列集中的成员，而不考虑层次结构。 在未指定标志的情况下， **ASC**为默认值。  
  
 如果对两个或更多层次结构都执行叉积的集使用**Order**函数，并且使用**DESC**标志，则仅对集内最后一个层次结构中的成员进行排序。 这与 Analysis Services 2000 不同，后者对集合中的所有层次结构进行排序。  
  
## <a name="examples"></a>示例  
 下面的示例从**艾德公司工作**多维数据集中返回 "日期" 维度的 "日历" 层次结构中所有日历季度的分销商订单数。**Order**函数对行轴的集进行重新排序。 **Order**函数按`[Calendar]`层次结构的降序`[Reseller Order Count]`顺序对集进行排序。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 请注意，在此示例中，如果**DESC**标志更改为**BDESC**，则会断开层次结构，并返回日历季度列表，而不考虑层次结构：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 使用**Order**函数对结果进行排序后，只使用**子集**函数返回集合中的前5个元组。  
  
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
  
 下面的示例使用**rank**函数根据 "分销商销售额" 度量值对 City 层次结构的成员进行排序，然后按排名顺序显示它们。 通过使用**order**函数对 City 层次结构的成员集进行第一次排序，排序只完成一次，然后在呈现排序顺序之前进行线性扫描。  
  
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
  
 下面的示例返回集合中唯一的产品数，并使用**order**函数对非空元组进行排序，然后再使用**筛选器**函数。 **CurrentOrdinal**函数用于比较和消除绑定。  
  
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
  
 若要了解**DESC**标志如何处理元组集，请先考虑以下查询的结果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 在行轴上，您可以看到 Sales Territory Groups 已按 Tax Amount 的降序排序，如下所示：North America、Europe、Pacific、NA。 现在，如果我们将一组销售区域组与一组产品子类别结合使用并以相同的方式应用**订单**功能，则会发生什么情况，如下所示：  
  
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
  
 尽管 Product Subcategories 的集合已按层次结构顺序的降序进行排序，但 Sales Territory Groups 现在未排序并且以它们在层次结构上出现的顺序出现：Europe、NA、North America 和 Pacific。 其原因在于，仅对元组集合中最后一个层次结构 Product Subcategories 进行了排序。 若要重现 Analysis Services 2000 的行为，请使用一系列嵌套的**生成**函数在执行叉积之前对每个集进行排序，例如：  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
