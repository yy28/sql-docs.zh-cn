---
title: PredictSequence （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: acb1982e61e622b150ee79af08e36ddcf24048ba
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970723"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  为一组指定的序列数据预测将来的序列值。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>返回类型  
 一个 \<table expression>。  
  
## <a name="remarks"></a>备注  
 如果指定了*n*参数，它将返回以下值：  
  
-   如果*n*大于零，则在接下来的*n*步中最可能的序列值。  
  
-   如果同时指定了*n 开头*和*n 端*，则序列值从*n 开始*到*n*端。  
  
## <a name="examples"></a>示例  
 以下示例根据 Sequence Clustering 挖掘模型返回 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 数据库中客户最可能购买的五种产品的顺序。  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
