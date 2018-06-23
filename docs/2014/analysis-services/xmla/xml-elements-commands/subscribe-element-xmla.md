---
title: Subscribe 元素 (XMLA) |Microsoft 文档
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
- Subscribe Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 94caa1327febf0c7fd5a489c7558ea793977d027
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026200"
---
# <a name="subscribe-element-xmla"></a>Subscribe 元素 (XMLA)
  订阅跟踪，并返回包含来自跟踪事件的行集[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Subscribe`命令订阅和流将从指定的跟踪行集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果在指定的对象而非跟踪，则`Object`元素，就会出错。  
  
 如果未指定 `Object` 元素，则将会在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例定义并订阅会话跟踪。 会话跟踪可从当前会话返回一组固定的跟踪事件。  
  
 客户端应用程序关闭之间的连接将终止此命令返回的行集流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，或者，如果在其中的会话`Subscribe`执行命令会终止。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  