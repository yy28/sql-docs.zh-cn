---
title: 子集 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e063d295480cff8e5db44f5ea30668a7a06ff74b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581389"
---
# <a name="subset-mdx"></a>Subset (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定集中元组的子集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *启动*  
 指定要返回第一个元组位置的有效数值表达式。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>Remarks  
 从指定的集，**子集**函数将返回包含元组，从指定的开始位置开始的指定的数目的子集。 开始位置基于以零为基的索引；即 0 对应于指定集中的第一个元组，1 对应于第二个元组，依此类推。  
  
 如果*计数*未指定，则该函数将返回所有元组从*启动*到集的末尾。  
  
## <a name="example"></a>示例  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 **子集**函数用于使用排序结果后，结果中返回仅的前五个集**顺序**函数。  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
