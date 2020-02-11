---
title: Tail （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d48a374d7d84c1137f082eb12dec638557b14e5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036659"
---
# <a name="tail-mdx"></a>Tail (MDX)


  返回集末尾的子集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **Tail**函数从指定集的末尾返回指定数目的元组。 会保留元素的顺序。 *Count*的默认值为1。 如果指定的元组数目小于 1，则该函数返回空集。 如果指定的元组数目超过了集中的元组数目，则此函数返回原始集。  
  
## <a name="example"></a>示例  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 当使用**Order**函数对结果进行反序排序后， **Tail**函数用于仅返回结果中的最后五个集。  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
