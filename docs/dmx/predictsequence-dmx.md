---
title: PredictSequence (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 813641b7fa72405a0ba5a026e255f03feb94bd05
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841550"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  为一组指定的序列数据预测将来的序列值。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>返回类型  
 A\<表表达式 >。  
  
## <a name="remarks"></a>Remarks  
 如果*n*指定参数，它将返回以下值：  
  
-   如果*n*大于零，下一步中最可能的序列值*n*步骤。  
  
-   如果这两个*n 开始*和*n 端*指定，序列值从*n 开始*到*n 端*。  
  
## <a name="examples"></a>示例  
 以下示例根据 Sequence Clustering 挖掘模型返回 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 数据库中客户最可能购买的五种产品的顺序。  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
