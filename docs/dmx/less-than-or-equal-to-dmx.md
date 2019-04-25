---
title: '&lt;= （小于或等于） (DMX) |Microsoft 文档'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 12dc7ca07dba7d36e7f65c9c6097b8b42457d3da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62502967"
---
# <a name="lt-less-than-or-equal-to-dmx"></a>&lt;= （小于或等于） (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行比较运算，以确定一个数据挖掘扩展插件 (DMX) 表达式的值是否小于等于另一个 DMX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
DMX_Expression <= DMX_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *DMX_Expression*  
 一个有效的 DMX 表达式。  
  
## <a name="return-value"></a>返回值  
 如果两个参数都非空，并且第一个参数的值小于或等于第二个参数的值，则返回包含 TRUE 的布尔值。 如果两个参数都非空，并且第一个参数的值大于第二个参数的值，则返回包含 FALSE 的布尔值。 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该布尔值包含空值。  
  
## <a name="see-also"></a>请参阅  
 [比较运算符&#40;DMX&#41;](../dmx/operators-comparison.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
