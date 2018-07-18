---
title: 删除挖掘结构 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b83de343e94c9263ba1ca6c6c8f09be90f3793b2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052315"
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  从数据库中删除指定的挖掘结构， 同时从数据库中删除与该结构关联的所有挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>参数  
 *结构*  
 结构标识符。  
  
## <a name="examples"></a>示例  
 以下示例从数据库中删除 New Mailing 挖掘结构。  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
