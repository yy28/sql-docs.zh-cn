---
title: '* 乘（DMX） |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 13ec459afba8080b9708fa49a00ff945ce7e320b
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83667677"
---
# <a name="-multiply-dmx"></a>*（乘）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行一个算术运算，将一个数与另一个数相乘。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *Numeric_Expression*  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
## <a name="return-value"></a>返回值  
 与优先级较高的参数具有相同数据类型的值。  
  
## <a name="remarks"></a>注解  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式的值为空值，则此运算符返回空值。  
  
## <a name="see-also"></a>另请参阅  
 [算术运算符 &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
