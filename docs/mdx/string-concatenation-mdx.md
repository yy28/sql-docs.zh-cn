---
description: '+  (MDX (字符串串联) ) '
title: +  (MDX)  (字符串串联) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e92751cb709a93d3d5d8d05ac76361c22bee5fa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386863"
---
# <a name="-string-concatenation-mdx"></a>+（字符串串联）(MDX)


  执行一个字符串运算，以连接两个或更多字符串、元组或字符串和元组组合。  
  
## <a name="syntax"></a>语法  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *String_Expression*  
 返回字符串值的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 具有与优先级较高的参数相同的数据类型的值。  
  
## <a name="remarks"></a>备注  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式求出的值为空值，该运算符将返回另一个表达式的结果。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
