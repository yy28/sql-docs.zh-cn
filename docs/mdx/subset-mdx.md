---
description: Subset (MDX)
title: 子集 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386723"
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
  
 *启动*  
 指定要返回第一个元组位置的有效数值表达式。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 从指定的集中， **子集** 函数返回一个子集，其中包含从指定的起始位置开始的指定数量的元组。 开始位置基于以零为基的索引；即 0 对应于指定集中的第一个元组，1 对应于第二个元组，依此类推。  
  
 如果未指定 *Count* ，则函数将返回从 *开始* 到集末尾的所有元组。  
  
## <a name="example"></a>示例  
 下例根据 Reseller Gross Profit（分销商毛利润），返回前五个销售产品子类别的分销商销售额度量值，而不管层次结构如何。 使用**Order**函数对结果进行排序后，只使用**子集**函数返回结果中的前五个集。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
