---
description: Comment-MDX 运算符参考
title: -- (注释)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ef1ba2fda9cd5eb6a82ea3d437c8e663c442cf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487600"
---
# <a name="comment---mdx-operator-reference"></a>Comment-MDX 运算符参考


  表示用户提供的注释文本。  
  
## <a name="syntax"></a>语法  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>参数  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 注释可以在单独的一行插入，也可以在多维表达式 (MDX) 脚本行的结尾处嵌入，还可以嵌入在 MDX 语句中。 服务器不对注释进行计算。  
  
 该运算符用于单行或嵌套的注释。 用 -- 插入的注释由换行符分隔。  
  
 注释没有最大长度限制。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>另请参阅  
 [注释 (MDX)](../mdx/comment-mdx.md)   
 [&#40;注释&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
