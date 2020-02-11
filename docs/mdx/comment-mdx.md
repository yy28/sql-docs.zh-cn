---
title: 注释（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f0aa1455ffd9f52fd917f68d2bb0bb80e3f25a94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006275"
---
# <a name="comment-mdx"></a>注释（MDX）


  表示用户提供的注释文本。  
  
## <a name="syntax"></a>语法  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>parameters  
 *Comment_Text*  
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
 服务器不会计算注释字符（/* 和\*/）之间的文本。 注释可以插入到单独一行中，也可以插入到多维表达式 (MDX) 语句中。 多行注释必须用/\*和\*/表示。  
  
 注释没有最大长度限制。 注释可以嵌套，例如，`/* Test /*Comment*/ Text*/` 就是一个嵌套注释的例子。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;注释&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40;注释&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
