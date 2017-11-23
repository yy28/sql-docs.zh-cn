---
title: "Hierarchize (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: HIERARCHIZE
dev_langs: kbMDX
helpviewer_keywords: Hierarchize function
ms.assetid: e9795003-70e7-4b4c-9074-45b5b9b817fa
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 71df425f851f4f7ffcf5eee6628cad6292fba339
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对层次结构中的某个集的成员进行排序。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **Hierarchize**函数组织分层顺序排列指定集的成员。 此函数始终保留重复项。  
  
-   如果**POST**未指定，则该函数对按其自然顺序级别中的成员进行排序。 如果未指定其他排序条件，则成员的自然顺序就是它们在层次结构中的默认排序顺序。 子成员会紧跟在它们的父成员之后。  
  
-   如果**POST**指定，则**Hierarchize**函数对使用非自然顺序排序的级别中的成员进行排序。 也就是说，子成员优先于他们的父级。  
  
## <a name="example"></a>示例  
 下例浅化了 Canada 成员。 **Hierarchize**函数用于组织分层顺序中的指定的组成员所需的**DrillUpMember**函数。  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，在某段中包含的 2003 年的第一个九个月聚合`Date`维度，从**Adventure Works**多维数据集。 **PeriodsToDate**函数定义元组集中的聚合函数对其进行操作。 **Hierarchize**函数将组织从分层顺序中的产品维度的成员组成的指定集的成员。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
