---
title: 和（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 930fe19abe7b1d783b4c69ef54b9b2550a05d538
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017096"
---
# <a name="and-mdx"></a>AND (MDX)


  对两个数值表达式执行逻辑与运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>parameters  
 Expression1   
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 Expression2   
 返回数值的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果两个参数的计算结果都为**true**，则返回 true;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑与运算之前，**和**运算符将两个表达式都视为布尔值（零，0，为**false**; 否则为**true**）。 下表说明了**和**运算符如何执行逻辑与运算。  
  
|Expression1 |Expression2 |返回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**false**|  
|**false**|**true**|**false**|  
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
  
  
