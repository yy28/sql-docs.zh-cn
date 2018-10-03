---
title: EndOfData 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EndOfData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EndOfData
helpviewer_keywords:
- EndOfData element
ms.assetid: 4cee48bc-d486-4125-9d65-f323c6ec9d09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f8d5b7038d767c6d261840edb63f9c1ebee7328
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211567"
---
# <a name="endofdata-element-assl"></a>EndOfData 元素 (ASSL)
  指示从接收的数据的结尾[PushedDataSource](../data-type/datasource-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PushedDataSource>  
   ...  
   <EndOfData>...</EndOfData>  
   ...  
</PushedDataSource  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PushedDataSource](../data-type/datasource-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 来自 `PushedDataSource` 的最后一个数据包必须将 `EndOfData` 元素设置为 `True`。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
