---
title: "标头 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 854d879b85ad5e70c21bd87240215b343aab96e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---headers"></a>XML 元素-标头
  XML for Analysis (XMLA) 协议使用 SOAP 标头内的 XML 元素来管理协议级别功能，例如会话支持以及协商支持的功能。  
  
## <a name="in-this-section"></a>本节内容  
 以下主题介绍了由实现的 XMLA 标头元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|方法|Description|  
|------------|-----------------|  
|[BeginSession 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上启动新会话。|  
|[EndSession 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头结束 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有会话。|  
|[会话元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有显式会话。|  
|[ProtocolCapabilities 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|使用 SOAP 请求消息中的 SOAP 标头标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例和客户端应用程序之间的协议功能。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 元素 &#40;XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 数据类型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 元素 &#40;XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
