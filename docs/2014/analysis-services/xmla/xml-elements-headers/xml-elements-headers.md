---
title: 标头 (XMLA) |Microsoft Docs
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b04b85e3267e7432f37c5f70e823c859a82a952
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291293"
---
# <a name="headers-xmla"></a>标头 (XMLA)
  XML for Analysis (XMLA) 协议使用 SOAP 标头内的 XML 元素来管理协议级别功能，例如会话支持以及协商支持的功能。  
  
## <a name="in-this-section"></a>本节内容  
 下面的主题介绍实现的 XMLA 标头元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|方法|Description|  
|------------|-----------------|  
|[BeginSession 元素&#40;XMLA&#41;](session-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上启动新会话。|  
|[EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头结束 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有会话。|  
|[Session 元素&#40;XMLA&#41;](session-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有显式会话。|  
|[ProtocolCapabilities 元素&#40;XMLA&#41;](protocolcapabilities-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例和客户端应用程序之间的协议功能。|  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML 数据类型&#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [XML 元素&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)  
  
  
