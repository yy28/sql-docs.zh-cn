---
title: SELECT FROM&lt;模型&gt;(DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5611ce3da4f12bca5cb271cabe8af3e149dcbf35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928326"
---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM&lt;模型&gt;(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行空预测联接，并为指定列返回一个或多个最可能的值。 创建预测时只使用来自挖掘模型的内容。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *表达式列表*  
 一组以逗号分隔的表达式、预测列或仅预测列。  
  
 *n*  
 可选。 一个指定返回行数的整数。  
  
 *model*  
 模型标识符。  
  
 *条件列表*  
 可选。 限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>备注  
 中的列*表达式列表*必须定义为 predict 或 predict 仅，或与可预测列相关。  
  
## <a name="naive-bayes-example"></a>Naive Bayes 示例  
 以下示例对 Bike Buyer 列执行一个空的预测联接，并返回 TM Naive Bayes 挖掘模型中最可能的状态。  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>时间序列示例  
 以下示例对预测模型中的 Amount 列执行预测，并返回接下来的四个时间步长。 Model Region 列将 bike models 和 regions 组合为一个标识符。 该查询使用[PredictTimeSeries &#40;DMX&#41; ](../dmx/predicttimeseries-dmx.md)函数来执行预测。  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>请参阅  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
