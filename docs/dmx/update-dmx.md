---
title: "更新 (DMX) |Microsoft 文档"
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
- UPDATE
dev_langs:
- DMX
helpviewer_keywords:
- NODE_CAPTION column
- mining models [Analysis Services], content changes
- modifying mining model content
- UPDATE statement [SQL Server], DMX
ms.assetid: 8a2b0942-c490-410c-b1cf-ff2e0fd8e24b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8f58eb94fb2700e8a2d614d31e12c260c352db97
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改**NODE_CAPTION**数据挖掘模型中的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>参数  
 *model*  
 一个模型标识符。  
  
 *新标题*  
 包含的新名称的字符串**NODE_CAPTION**列。  
  
 *条件表达式*  
 選擇性。 一个限制条件，用于限制从列列表返回的值。  
  
## <a name="examples"></a>示例  
 在下面的示例中，**更新**语句会更改默认名称， `Cluster 1`，群集`001`为更具描述性的名称， `Likely Customers`。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>另請參閱  
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

