---
title: 尾部 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5192deedcb6085767fc00f68bb17f6adddb38679
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581239"
---
# <a name="tail-mdx"></a>Tail (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回集末尾的子集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>Remarks  
 **结尾**函数从指定集的末尾返回指定的数目的元组。 会保留元素的顺序。 默认值*计数*为 1。 如果指定的元组数目小于 1，则该函数返回空集。 如果指定的元组数目超过了集中的元组数目，则此函数返回原始集。  
  
## <a name="example"></a>示例  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 **结尾**函数用于在结果中返回仅的最后五个集后结果都反向-使用订购**顺序**函数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
