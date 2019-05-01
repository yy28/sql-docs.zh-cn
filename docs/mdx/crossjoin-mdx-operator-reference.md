---
title: '* (Crossjoin)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 132b237fd8baa9c50dc254b02d90ed95d7159a0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249623"
---
# <a name="crossjoin----mdx-operator-reference"></a>叉积的 MDX 运算符参考


  执行一个集运算以返回两个集的叉积。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 一个包含两个指定参数的叉积的集。  
  
## <a name="remarks"></a>备注  
  **\* （叉积）** 运算符在功能上等效于[叉积](../mdx/crossjoin-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
