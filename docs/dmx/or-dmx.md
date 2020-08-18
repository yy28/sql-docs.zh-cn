---
description: OR (DMX)
title: 或 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 86a9aede9f1b9b12f465fa52b0343cf22c04b295
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395433"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  一个逻辑运算符，用于对两个数值表达式执行逻辑或运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>参数  
 Expression1  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
 Expression2  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 如果任意一个参数或两个参数的计算结果为 TRUE，则返回 TRUE 布尔值；否则将返回 FALSE。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑或运算之前，两个参数均被视为布尔值（0 为 FALSE；否则为 TRUE）。 如果任何一个参数或两个参数的计算结果均为 TRUE，则该运算符将返回 TRUE。 如果 *表达式* 2 的计算结果为 TRUE 并且 *表达式* 2 的计算结果为 FALSE，则运算符返回 TRUE。  
  
 下表阐释了执行逻辑或运算的方式。  
  
|如果 Expression1 为|如果 Expression2 为|则返回值为|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|true|false|true|  
|false|TRUE|true|  
|false|false|false|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
