---
title: "不 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: NOT
dev_langs: DMX
helpviewer_keywords: NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c242a6767e60b04249d69d340806d0cf78a374e2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
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
  
## <a name="remarks"></a>Remarks  
 在运算符执行逻辑非运算之前，该参数被视为布尔值（0 为 FALSE；否则为 TRUE）。 如果*Expression1*为 TRUE 时，该运算符将返回 FALSE。 如果*Expression1*为 FALSE 时，该运算符将返回 TRUE。 下表阐释了执行逻辑与运算的方式。  
  
|如果 Expression1 为|则返回值为|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
