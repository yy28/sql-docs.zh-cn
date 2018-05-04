---
title: 和 (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AND
dev_langs:
- DMX
helpviewer_keywords:
- AND, DMX
ms.assetid: d337b20c-f80e-48be-9354-371367e53735
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4968fc4f42ffe33e6e8926d8eccbc661060c30a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  对两个数值表达式执行逻辑与运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
 *Expression2*  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值。如果两个参数的处理结果均为 TRUE，则返回 TRUE；否则返回 FALSE。  
  
## <a name="remarks"></a>注释  
 在运算符执行逻辑与运算之前，两个参数都被视为布尔值（0 为 FALSE；其他为 TRUE）。 下表列出了不同参数值组合的返回值。  
  
|如果 Expression1 为|如果 Expression2 为|则返回值为|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符&#40;DMX&#41;](../dmx/operators-logical.md)   
 [运算符&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
