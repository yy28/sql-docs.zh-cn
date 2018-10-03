---
title: Subscribe 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf88b3e4e2fd990ad786b8e505c908f96f53ce6e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079337"
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Subscribe`命令订阅和流返回行集上指定的跟踪[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果在指定的对象而非跟踪`Object`元素，就会出错。  
  
 如果未指定 `Object` 元素，则将会在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例定义并订阅会话跟踪。 会话跟踪可从当前会话返回一组固定的跟踪事件。  
  
 如果客户端应用程序关闭到的连接终止此命令返回的行集流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，或者如果该会话上的`Subscribe`命令执行将终止。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
