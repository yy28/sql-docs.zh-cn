---
title: "BottomCount (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BOTTOMCOUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomCount function
ms.assetid: 1441dab3-7885-4e92-9d48-21d832286677
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 972ec04cf1a64e5e2a20b0befa4c85afd31631de
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  按升序对集进行排序，并返回指定集中具有最小值的指定数目的元组。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果指定了数值表达式，则此函数根据在指定集中计算出的指定数值表达式的值，对指定集中的元组按升序进行排序。 **BottomCount**函数然后返回指定的数目的最低值的元组。  
  
> [!IMPORTANT]  
>  **BottomCount**函数，如[TopCount](../mdx/topcount-mdx.md)函数中，始终中断层次结构。  
  
 如果未指定数值表达式，函数将返回成员组成的集在自然顺序排序，不进行任何排序，如行为[结尾 (MDX)](../mdx/tail-mdx.md)函数。  
  
## <a name="example"></a>示例  
 下例将返回每个日历年中最后五个“产品子类别”销售额的“分销商订单数量”度量值，并根据“分销商销售额”度量值进行排序。  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

