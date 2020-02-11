---
title: 更新（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d28df68512f9c97faebf3ee00b2aa34a2b8d1a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028668"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  更改数据挖掘模型中的**NODE_CAPTION**列。  
  
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
 一个包含**NODE_CAPTION**列的新名称的字符串。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
## <a name="examples"></a>示例  
 在下面的示例中， **UPDATE**语句将群集`Cluster 1` `001`的默认名称更改为更具描述性的名称。 `Likely Customers`  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
