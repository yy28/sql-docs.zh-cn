---
title: 存储元素 (XMLA) |Microsoft 文档
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
- Storage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.storage
- urn:schemas-microsoft-com:xml-analysis#Storage
- http://schemas.microsoft.com/analysisservices/2003/engine#Storage
helpviewer_keywords:
- Storage element
ms.assetid: c3590af8-a24b-4fd3-b846-17edbd399b6d
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8bccf119846d699d653a480f6479412b46dcc4f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129333"
---
# <a name="storage-element-xmla"></a>Storage 元素 (XMLA)
  以字节为单位，使用指定的最大存储量[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)命令设计聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Storage>...</Storage>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
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
  
  