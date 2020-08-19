---
description: AND (MDX)
title: 和 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: baff2f517f5fdd6dfbb23eb24ad51ed12589df52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429969"
---
# <a name="and-mdx"></a>AND (MDX)


  对两个数值表达式执行逻辑与运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>参数  
 Expression1  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2  
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果两个参数的计算结果都为 **true**，则返回 true;否则 **为 false**。  
  
## <a name="remarks"></a>备注  
 **AND**运算符将两个表达式视为布尔值 (零，0，为**false**;否则，**在**运算符执行逻辑与运算之前) 。 下表说明了 **和** 运算符如何执行逻辑与运算。  
  
|Expression1|Expression2|返回值|  
|-------------------|-------------------|------------------|  
|true|true|true|  
|true|**false**|**false**|  
|**false**|true|**false**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>示例  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is between 20% and 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .3 AND   
      [Measures].[Gross Profit Margin] >= .2,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
