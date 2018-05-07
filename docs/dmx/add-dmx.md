---
title: + （添加）(DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- + (add)
- add operator (+)
ms.assetid: 35e7636f-814c-44c3-94a7-384a305d65ea
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b28cf10467c7c321c60ba0a433fc1c883d58d403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="-add-dmx"></a>+ (加) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行将两数相加的算术运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *Numeric_Expression*  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
## <a name="return-value"></a>返回值  
 与优先级较高的参数具有相同数据类型的值。  
  
## <a name="remarks"></a>注释  
 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。 如果一个表达式求出的值为空值，该运算符将返回另一个表达式的结果。  
  
## <a name="see-also"></a>另请参阅  
 [算术运算符&#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
