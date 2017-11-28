---
title: "&lt;&gt;（不等于）(DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- not equal operator (<>)
- <> (not equal to operator)
ms.assetid: df0e7901-9e31-452a-af14-471f5130c09d
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: df165d14cacfde172fa8d242c3fae7add30f87db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="ltgt-not-equal-to-dmx"></a>&lt;&gt;（不等于）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行比较运算，以确定一个数据挖掘扩展插件 (DMX) 表达式的值是否不等于另一个 DMX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
DMX_Expression <> DMX_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *DMX_Expression*  
 一个有效的 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 如果两个参数都为非空值，并且第一个参数的值不等于第二个参数的值，则返回包含 TRUE 的布尔值。 如果两个参数都为非空值，并且第一个参数的值等于第二个参数的值，则返回包含 FALSE 的布尔值。 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该布尔值包含空值。  
  
## <a name="see-also"></a>另请参阅  
 [比较运算符 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [运算符 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
