---
title: = （等于） (DMX) |Microsoft 文档
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
- equal operator (=)
- = (equals operator)
ms.assetid: 6ac019b1-6373-4e2c-a1ad-fe2dc6188ac3
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c4f962dbda2fbd1c13725d64ddc9519d14cb9275
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="-equal-to-dmx"></a>=（等于）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行比较运算，以确定一个数据挖掘扩展插件 (DMX) 表达式的值是否等于另一个 DMX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>Parameters  
 *DMX_Expression*  
 一个有效的 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 如果两个参数都非空，并且第一个参数值与第二个参数值相等，则将返回包含 TRUE 的布尔值。 如果两个参数都非空，并且第一个参数值与第二个参数值不相等，则将返回包含 FALSE 的布尔值。 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该布尔值包含空值。  
  
## <a name="see-also"></a>另请参阅  
 [比较运算符&#40;DMX&#41;](../dmx/operators-comparison.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
