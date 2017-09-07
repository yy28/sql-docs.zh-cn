---
title: "SELECT FROM&lt;模型&gt;(DMX) |Microsoft 文档"
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
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- empty prediction joins [DMX]
- SELECT FROM <model> statement
ms.assetid: dc5b9a01-e308-4ee8-84fc-ba4b991c60aa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c51d5d3f3a5a1c8e9b94f72367739d592f1918c8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM&lt;模型&gt;(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 選擇性。 一个指定返回行数的整数。  
  
 *model*  
 一个模型标识符。  
  
 *条件列表*  
 選擇性。 限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 選擇性。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>注释  
 中的列*表达式列表*必须定义为预测或预测仅，或与可预测列相关的。  
  
## <a name="naive-bayes-example"></a>Naive Bayes 示例  
 以下示例对 Bike Buyer 列执行一个空的预测联接，并返回 TM Naive Bayes 挖掘模型中最可能的状态。  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>时间序列示例  
 以下示例对预测模型中的 Amount 列执行预测，并返回接下来的四个时间步长。 Model Region 列将 bike models 和 regions 组合为一个标识符。 该查询使用[PredictTimeSeries &#40; DMX &#41;](../dmx/predicttimeseries-dmx.md)函数进行预测。  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>另請參閱  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

