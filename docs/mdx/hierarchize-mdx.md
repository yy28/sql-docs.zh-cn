---
description: Hierarchize (MDX)
title: Hierarchize (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c1683819420d150e2f9b330ba94bc9e228d167f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429909"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  对层次结构中的某个集的成员进行排序。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **Hierarchize**函数将指定集的成员组织成层次顺序。 此函数始终保留重复项。  
  
-   如果未指定 **POST** ，则函数将按其自然顺序对级别中的成员进行排序。 如果未指定其他排序条件，则成员的自然顺序就是它们在层次结构中的默认排序顺序。 子成员会紧跟在它们的父成员之后。  
  
-   如果指定了 **post** ， **Hierarchize** 函数将使用后自然顺序对级别中的成员进行排序。 也就是说，子成员优先于他们的父级。  
  
## <a name="example"></a>示例  
 下例浅化了 Canada 成员。 **Hierarchize**函数用于按层次结构顺序组织指定集成员，这是**DrillUpMember**函数所必需的。  
  
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
  
 下面的示例 `Measures.[Order Quantity]` `Date` 从 **艾德工作** 多维数据集中返回维度中包含的前九个月（2003）聚合的成员的总和。 **PeriodsToDate**函数定义聚合函数对其进行运算的集中的元组。 **Hierarchize**函数以分层顺序从产品维度中组织指定成员集的成员。  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
