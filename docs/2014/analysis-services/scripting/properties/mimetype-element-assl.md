---
title: MimeType 元素 (ASSL) |Microsoft 文档
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
- MimeType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MimeType element
ms.assetid: 710e2519-6892-4ce8-a10f-a4edf7077e18
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5ae8ddac41536e2857fb51cfe7fe6420d5c74c15
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017612"
---
# <a name="mimetype-element-assl"></a>MimeType 元素 (ASSL)
  如果适用，所表示的数据包含多用途 Internet 邮件扩展 (MIME) 类型， [DataItem](../data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem  
   ...  
  <MimeType>...</MimeType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)  
  
  