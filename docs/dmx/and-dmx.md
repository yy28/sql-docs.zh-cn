---
description: AND (DMX)
title: 和 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17dabee823323c63a2d36a21cd79b81e9a323803
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431199"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  对两个数值表达式执行逻辑与运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>参数  
 Expression1  
 一个返回数值的有效数据挖掘扩展 (DMX) 表达式。  
  
 Expression2  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值。如果两个参数的处理结果均为 TRUE，则返回 TRUE；否则返回 FALSE。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑与运算之前，两个参数都被视为布尔值（0 为 FALSE；其他为 TRUE）。 下表列出了不同参数值组合的返回值。  
  
|如果 Expression1 为|如果 Expression2 为|则返回值为|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|true|false|false|  
|false|true|false|  
|false|false|false|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
