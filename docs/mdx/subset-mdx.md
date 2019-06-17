---
title: 子集 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07d813587dc530924becbb187a970f78022e5476
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136092"
---
# <a name="subset-mdx"></a>Subset (MDX)


  返回指定集中元组的子集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *开始*  
 指定要返回第一个元组位置的有效数值表达式。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 从指定集中**子集**函数返回包含指定的数目的元组，从指定的开始位置开始的子集。 开始位置基于以零为基的索引；即 0 对应于指定集中的第一个元组，1 对应于第二个元组，依此类推。  
  
 如果*计数*未指定，则该函数将返回中的所有元组*启动*到集的末尾。  
  
## <a name="example"></a>示例  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 **子集**函数用于仅返回前五个集的结果后将结果排序使用**顺序**函数。  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
