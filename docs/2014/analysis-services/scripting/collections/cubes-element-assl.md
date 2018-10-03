---
title: 多维数据集元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cubes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Cubes
helpviewer_keywords:
- Cubes element
ms.assetid: 0eaaaf3f-0c78-4eb4-bc3a-d266579eca56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f289951caa8357c1fe5f63162636e3dee9999de3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222057"
---
# <a name="cubes-element-assl"></a>Cubes 元素 (ASSL)
  包含的集合[多维数据集](../objects/cube-element-assl.md)与关联的元素[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
   ...  
   <Cubes>  
            <Cube>...</Cube>  
   </Cubes>  
      ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](../objects/database-element-assl.md)|  
|子元素|[Cube](../objects/cube-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
