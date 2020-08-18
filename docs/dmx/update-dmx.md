---
description: UPDATE (DMX)
title: 更新 DMX)  (|Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d74a59aaea079a5d3c1945b92813f6d276591b78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394873"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  更改数据挖掘模型中的 **NODE_CAPTION** 列。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>参数  
 *model*  
 模型标识符。  
  
 *新标题*  
 一个包含 **NODE_CAPTION** 列的新名称的字符串。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
## <a name="examples"></a>示例  
 在下面的示例中， **UPDATE** 语句将群集的默认名称更改 `Cluster 1` `001` 为更具描述性的名称 `Likely Customers` 。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
