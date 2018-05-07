---
title: '- （减）(DMX) |Microsoft 文档'
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
- '- (subtract)'
- subtract operator (-)
ms.assetid: 9602e908-e80c-442a-a412-073e10d0abd4
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9f865752bc9e1a0ea268ba3dbb7b29aaa5a70571
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="--subtract-dmx"></a>-（减）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行一个算术运算，将一个数减去另一个数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric_Expression - Numeric_Expression  
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
  
  
