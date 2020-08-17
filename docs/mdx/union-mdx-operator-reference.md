---
description: 联合-MDX 运算符引用
title: +  (MDX)  (联合) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 84e6bc2b6b8460b90013ade5f0981af7f0ed8432
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341186"
---
# <a name="union---mdx-operator-reference"></a>联合-MDX 运算符引用


  执行一个集运算以返回两个集的并集并删除重复成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 一个包含两个指定集的成员的集。  
  
## <a name="remarks"></a>备注  
 **+ (联合) **运算符在功能上等效于[联合 &#40;MDX&#41;](../mdx/union-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
