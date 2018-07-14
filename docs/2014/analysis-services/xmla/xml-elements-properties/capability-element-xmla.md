---
title: Capability 元素 (XMLA) |Microsoft Docs
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
- Capability Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a5b14b43b41f74c05d433c599b18486c5737b27c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201887"
---
# <a name="capability-element-xmla"></a>Capability 元素 (XMLA)
  指示父代中的协议功能的支持[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)标头元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Capability`元素指示一个特定的功能，如二进制或压缩，受包含的任一应用程序`ProtocolCapabilities`SOAP 标头的 SOAP 请求，或由的实例中的标头元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含`ProtocolCapabilities`SOAP 响应的 SOAP 标头中的标头元素。 `Capability` 元素的值为所支持的功能的名称。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持下表所列出的功能。  
  
|功能名称|Description|  
|---------------------|-----------------|  
|sx|二进制 XML 支持|  
|xpress|压缩支持|  
  
## <a name="see-also"></a>请参阅  
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
