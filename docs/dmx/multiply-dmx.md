---
title: "* （乘）(DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: cfab1581-7818-427b-b8b2-cec0b5e3a0cd
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9371f347a8ed72bc8e188ae08acdc3afe15cb525
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="-multiply-dmx"></a>*（乘）(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行一个算术运算，将一个数与另一个数相乘。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *Numeric_Expression*  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
## <a name="return-value"></a>返回值  
 与优先级较高的参数具有相同数据类型的值。  
  
## <a name="remarks"></a>備註  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式的值为空值，则此运算符返回空值。  
  
## <a name="see-also"></a>另请参阅  
 [算术运算符 &#40; DMX &#41;](../dmx/operators-arithmetic.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

