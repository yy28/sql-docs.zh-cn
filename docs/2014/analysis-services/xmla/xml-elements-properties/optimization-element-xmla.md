---
title: Optimization 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Optimization Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Optimization
- urn:schemas-microsoft-com:xml-analysis#Optimization
- microsoft.xml.analysis.optimization
helpviewer_keywords:
- Optimization element
ms.assetid: fb9ff737-59e2-4d8b-9f0e-af392eb25d08
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b20e8875f982f16a3f7ee128552c65fbbfca0f60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261303"
---
# <a name="optimization-element-xmla"></a>Optimization 元素 (XMLA)
  指定使用的优化临界值百分比[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)命令用于设计聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Optimization>...</Optimization>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|双精度|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
