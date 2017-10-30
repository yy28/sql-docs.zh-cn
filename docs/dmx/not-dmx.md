---
title: "不 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOT
dev_langs:
- DMX
helpviewer_keywords:
- NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 947d066f9dd13d7f4af15407987fcf218c275cc2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>注释  
 在运算符执行逻辑非运算之前，该参数被视为布尔值（0 为 FALSE；否则为 TRUE）。 如果*Expression1*为 TRUE 时，该运算符将返回 FALSE。 如果*Expression1*为 FALSE 时，该运算符将返回 TRUE。 下表阐释了执行逻辑与运算的方式。  
  
|如果 Expression1 为|则返回值为|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [逻辑运算符 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

