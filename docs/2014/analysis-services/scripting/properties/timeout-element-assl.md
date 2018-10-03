---
title: Timeout 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Timeout Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Timeout
helpviewer_keywords:
- Timeout element
ms.assetid: 7694872b-bd05-459f-b5dc-3cfbd92a9664
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 051da6eafdd75cc8c3a041dc6ec9115dd962363d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058807"
---
# <a name="timeout-element-assl"></a>Timeout 元素 (ASSL)
  指定以秒为单位的一段时间，这段时间之后再试图检索数据将报告超时。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <Timeout>...</Timeout>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Duration|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../objects/datasource-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`Timeout`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
