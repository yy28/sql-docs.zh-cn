---
description: CurrentOrdinal (MDX)
title: CurrentOrdinal (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68119266fd9460a28e036914fce036ec165e553a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413153"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal (MDX)


  返回迭代过程中集内的当前迭代数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 在循环访问集时（如使用 [筛选器 (mdx) ](../mdx/filter-mdx.md) 或 [生成 (mdx) ](../mdx/generate-mdx.md) 函数时， **CurrentOrdinal** 函数将返回迭代号。  
  
## <a name="examples"></a>示例  
 以下简单示例演示了 **CurrentOrdinal** 如何与 " **生成** " 一起使用，以返回一个字符串，其中包含集内每个项的名称及其在集中的位置：  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal 的实际用法仅限于非常复杂的计算。 下面的示例返回集合中唯一的产品数，并使用 **order** 函数对非空元组进行排序，然后再使用 **筛选器** 函数。 **CurrentOrdinal**函数用于比较和消除绑定。  
  
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
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
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
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
