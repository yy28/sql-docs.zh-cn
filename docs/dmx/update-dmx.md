---
title: 更新 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d28df68512f9c97faebf3ee00b2aa34a2b8d1a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028668"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  更改**NODE_CAPTION**数据挖掘模型中的列。  
  
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
 包含的新名称的字符串**NODE_CAPTION**列。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
## <a name="examples"></a>示例  
 在以下示例中，**更新**语句更改默认名称， `Cluster 1`，为群集`001`为更具说明性的名称， `Likely Customers`。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
