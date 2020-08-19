---
description: PredictAdjustedProbability (DMX)
title: PredictAdjustedProbability (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e923e96aec1f001818f5dcff300de0d13af2f5a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426179"
---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回指定状态调整后的概率。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>适用于  
 标量列。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>备注  
 如果未提供预测状态，将使用具有最大可预测概率的状态，不包括缺少状态存储桶。 若要包含缺少的状态存储桶，请将设置 \<predicted state> 为 **INCLUDE_NULL**。  
  
 若要为缺少的状态返回调整后的概率，请将设置 \<predicted state> 为 NULL。  
  
 **PredictAdjustedProbability**函数是 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] 数据挖掘规范 OLE DB 的扩展。  
  
## <a name="examples"></a>示例  
 以下示例根据 TM Decision Tree 挖掘模型，使用自然预测联接确定某个人是否可能购买自行车，并且还确定该测校正后的概率。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
