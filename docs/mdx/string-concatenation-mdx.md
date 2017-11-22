---
title: "+ （字符串串联）(MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: +
dev_langs: kbMDX
helpviewer_keywords:
- string concatenation operators
- + (string concatenation)
ms.assetid: d77636b1-2973-4587-af35-54aba5700d9a
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 026618d4a71e2e3c85df12c1994c4c0b6ffd30f7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="-string-concatenation-mdx"></a>+（字符串串联）(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行一个字符串运算，以连接两个或更多字符串、元组或字符串和元组组合。  
  
## <a name="syntax"></a>语法  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *String_Expression*  
 返回字符串值的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 具有与优先级较高的参数相同的数据类型的值。  
  
## <a name="remarks"></a>注释  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式求出的值为空值，该运算符将返回另一个表达式的结果。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
