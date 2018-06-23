---
title: SPID 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SPID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#SPID
- microsoft.xml.analysis.spid
- urn:schemas-microsoft-com:xml-analysis#SPID
helpviewer_keywords:
- SPID element
ms.assetid: c4a54dcb-a0cd-4255-9e0f-a34eb990854f
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d203225045314115604a8b99d82ab291c5960376
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123697"
---
# <a name="spid-element-xmla"></a>SPID 元素 (XMLA)
  标识对其执行父活动服务器进程标识符 (SPID)[取消](../xml-elements-commands/cancel-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[取消](../xml-elements-commands/cancel-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `SPID`元素表示服务器进程 ID (SPID) 用于指定会话的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [CancelAssociated 元素&#40;XMLA&#41;](cancelassociated-element-xmla.md)   
 [ConnectionID 元素&#40;XMLA&#41;](id-element-xmla.md)   
 [SessionID 元素&#40;XMLA&#41;](sessionid-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  