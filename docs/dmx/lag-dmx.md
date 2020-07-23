---
title: Lag （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e011fc48b63aa653cd63e11678b84d8356370bd0
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969238"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回当前事例的日期与定型集的最近日期之间的时间段。  
  
## <a name="syntax"></a>语法  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>返回类型  
 整型类型的标量值。  
  
## <a name="remarks"></a>备注  
 如果对键 TIME 列位于嵌套表中的模型使用**Lag**函数，则该函数必须位于语句的子选择中。  
  
## <a name="examples"></a>示例  
 下面的示例返回在过去12个月内用于为模型定型的事例。  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
