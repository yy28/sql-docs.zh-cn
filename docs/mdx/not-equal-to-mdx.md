---
title: '&lt;&gt;（不等于）（MDX） |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088322"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt;（不等于）并用


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否不等于另一个 MDX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   如果两个参数均非空，并且第一个参数不等于第二个参数，**则为 true** 。  
  
-   如果两个参数均非空，并且第一个参数等于第二个参数，则**为 false** 。  
  
-   如果两个参数或其中任何一个参数计算出来的值为空值，则为 Null。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
