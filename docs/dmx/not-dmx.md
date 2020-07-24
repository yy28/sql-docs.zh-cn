---
title: 不是（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 98c40dba282c82f124d4e4ac009a046a44a283cb
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971625"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  一种逻辑运算符，用于对数值表达式执行逻辑非运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>参数  
 Expression1  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，在参数的计算结果为 TRUE 时返回 FALSE；否则将返回 FALSE。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑非运算之前，该参数被视为布尔值（0 为 FALSE；否则为 TRUE）。 如果*表达式*值为 TRUE，则运算符返回 FALSE。 如果*表达式*值为 FALSE，则运算符返回 TRUE。 下表阐释了执行逻辑与运算的方式。  
  
|如果 Expression1 为|则返回值为|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符 &#40;DMX&#41;](../dmx/operators-logical.md)   
 [运算符 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
