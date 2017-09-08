---
title: "Subscribe 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Subscribe Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0af4762aec4d048f19ee47f8d07445aa5e7a8b3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **订阅**命令订阅和流将从指定的跟踪行集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果在 **Object** 元素中指定对象而非跟踪，则会出错。  
  
 如果**对象**元素未指定，则会话跟踪定义，并会在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 会话跟踪可从当前会话返回一组固定的跟踪事件。  
  
 客户端应用程序关闭之间的连接将终止此命令返回的行集流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，或者，如果在其中的会话**订阅**执行命令会终止。  
  
## <a name="see-also"></a>另请参阅  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
