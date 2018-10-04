---
title: CancelAssociated 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CancelAssociated Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancelassociated
- urn:schemas-microsoft-com:xml-analysis#CancelAssociated
- http://schemas.microsoft.com/analysisservices/2003/engine#CancelAssociated
helpviewer_keywords:
- CancelAssociated element
ms.assetid: fd890440-d1a7-4c05-9e81-c81e6b8c274c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 294f1060c0a52c357e791d5b3db7ad87d0d98309
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126587"
---
# <a name="cancelassociated-element-xmla"></a>CancelAssociated 元素 (XMLA)
  指示父 [Cancel](../xml-elements-commands/cancel-element-xmla.md) 元素是否应该取消所有关联命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[取消](../xml-elements-commands/cancel-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 如果指定此元素并将其设置为`True`，每个对应连接、 会话和命令的父代中标识`Cancel`取消命令。  
  
## <a name="see-also"></a>请参阅  
 [ConnectionID 元素&#40;XMLA&#41;](id-element-xmla.md)   
 [SessionID 元素&#40;XMLA&#41;](sessionid-element-xmla.md)   
 [SPID 元素&#40;XMLA&#41;](spid-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
