---
title: 交叉联接 (MDX) |Microsoft 文档
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
- CROSSJOIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Crossjoin function
ms.assetid: 503b8376-d244-4855-8f44-a749764162e4
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0529245668d3456af58e6907635c42570a70a882
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回一个或多个集的叉积。  
  
## <a name="syntax"></a>语法  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **叉积**函数返回跨产品的两个或多个指定集。 所得集中元组的顺序取决于要联接的集的顺序以及其成员的顺序。 例如，当第一组包含 {x1，x2，...，x*n*}，并在第二个集包含 {y1、 y2，...，y*n*}，个这些集的叉积是：  
  
 {(x1，y1)，(x1，y2)，...，(x1，y*n*)，(x2，y1)，(x2，y2)，...，  
  
 (x2，y*n*)，...，(x*n*，y1)，(x*n*，y2)，...，(xn，y*n*)}  
  
> [!IMPORTANT]  
>  如果交叉联接中的集由同一维度中不同属性层次结构中的元组组成，此函数将只返回实际存在的那些元组。 有关详细信息，请参阅[在 MDX 中的关键概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。  
  
## <a name="examples"></a>示例  
 以下查询说明在查询的列轴和行轴上使用 Crossjoin 函数的简单示例：  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 以下示例说明交叉联接同一维度中的不同层次结构时发生的自动筛选：  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 以下三个示例返回相同的结果 - United States 各州的 Internet Sales Amount（按州显示）。 前两个示例使用两个交叉联结语法，第三个示例演示了使用 WHERE 子句返回相同的信息。  
  
### <a name="example-1"></a>示例 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>示例 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>示例 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
