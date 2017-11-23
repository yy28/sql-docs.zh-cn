---
title: "CancelAssociated 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CancelAssociated Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cancelassociated
- urn:schemas-microsoft-com:xml-analysis#CancelAssociated
- http://schemas.microsoft.com/analysisservices/2003/engine#CancelAssociated
helpviewer_keywords: CancelAssociated element
ms.assetid: fd890440-d1a7-4c05-9e81-c81e6b8c274c
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 65d60344142e10f0912c81fdb7062f30b740a9ad
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="cancelassociated-element-xmla"></a>CancelAssociated 元素 (XMLA)
  指示父 [Cancel](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) 元素是否应该取消所有关联命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[取消](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果此元素已指定，并且设置为 **True**，则取消在父级 **Cancel** 命令中标识的所有对应连接、会话和命令。  
  
## <a name="see-also"></a>另请参阅  
 [ConnectionID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [SPID 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
