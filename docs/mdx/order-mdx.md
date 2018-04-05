---
title: 次序 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ORDER
dev_langs:
- kbMDX
helpviewer_keywords:
- Order function
ms.assetid: 84acff52-2443-4424-a09e-694e6f14c109
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c67e4106b760f9218172e7ada5628e34dd308f8a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="order-mdx"></a>Order (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 **顺序**函数可以是分层 (所指定的使用**ASC**或**DESC**标志) 或非层次结构 (通过使用指定**BASC**或**BDESC**标志; **B**代表"中断层次结构")。 如果**ASC**或**DESC**指定，则**顺序**函数首先将根据其位置在位于层次结构的成员，然后订单每个级别。 如果**BASC**或**BDESC**指定，则**顺序**函数排列而不考虑层次结构集中的成员。 在任何标志指定如何， **ASC**是默认设置。  
  
 如果**顺序**函数用于处理一组其中两个或多个层次结构是交叉联接，和**DESC**使用标志，则只有组中的最后一个层次结构的成员进行排序。 这与 Analysis Services 2000 不同，后者对集合中的所有层次结构进行排序。  
  
## <a name="examples"></a>示例  
 下面的示例返回时，从**Adventure Works**多维数据集，从日期维度上的日历层次结构的所有日历季度的分销商订单数。**顺序**函数重新排序为 ROWS 轴的集。 **顺序**函数进行排序的集`[Reseller Order Count]`降序分层所确定的那样`[Calendar]`层次结构。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 请注意如何在此示例中，当**DESC**标志更改为**BDESC**、 层次结构已断开，且而不考虑为层次结构返回的日历季度的列表：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 **子集**函数用于后使用排序结果集中返回仅前 5 元组**顺序**函数。  
  
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
  
 下面的示例使用**级别**函数来进行排名的市/县层次结构中，成员基于 Reseller Sales Amount 度量值，，然后按排序顺序显示它们。 通过使用**顺序**函数到第一个订单的市/县层次结构的成员组成的集，排序仅一次执行，并对后跟线性扫描之前要呈现在排序顺序。  
  
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
  
 下面的示例中是唯一的使用的集返回的产品数目**顺序**函数进行排序之前使用的非空元组**筛选器**函数。 **CurrentOrdinal**函数用于比较并消除等同值。  
  
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
  
 若要了解如何**DESC**标志适用于集的元组，首先，请考虑以下查询的结果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 在行轴上，您可以看到 Sales Territory Groups 已按 Tax Amount 的降序排序，如下所示：North America、Europe、Pacific、NA。 发生什么情况，现在请参阅我们叉积的一套产品子类别的销售区域组的集，并将应用**顺序**函数相同的方式，如下所示：  
  
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
  
 尽管 Product Subcategories 的集合已按层次结构顺序的降序进行排序，但 Sales Territory Groups 现在未排序并且以它们在层次结构上出现的顺序出现：Europe、NA、North America 和 Pacific。 其原因在于，仅对元组集合中最后一个层次结构 Product Subcategories 进行了排序。 若要重现的 Analysis Services 2000 的行为，请使用一系列嵌套**生成**函数对每个组进行排序，才使用它交叉联接，例如：  
  
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
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
