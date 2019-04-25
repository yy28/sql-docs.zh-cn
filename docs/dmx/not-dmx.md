---
title: NOT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 053eb905edb1379bfdc40ec010dc6d4efadcba26
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503857"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  一种逻辑运算符，用于对数值表达式执行逻辑非运算。  
  
## <a name="syntax"></a>语法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 一个返回数值的有效 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，在参数的计算结果为 TRUE 时返回 FALSE；否则将返回 FALSE。  
  
## <a name="remarks"></a>备注  
 在运算符执行逻辑非运算之前，该参数被视为布尔值（0 为 FALSE；否则为 TRUE）。 如果*Expression1*为 TRUE 时，该运算符将返回 FALSE。 如果*Expression1*为 FALSE 时，运算符将返回 TRUE。 下表阐释了执行逻辑与运算的方式。  
  
|如果 Expression1 为|则返回值为|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符&#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
