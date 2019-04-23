---
title: 使用 Reporting Services SOAP 标头 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f48be183398d4d441b5781c9f9467178c3011e32
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155243"
---
# <a name="using-reporting-services-soap-headers"></a>使用 Reporting Services SOAP 标头
  使用 SOAP 与 Web 服务方法的通信遵循标准的格式。 此格式中的部分内容为在 XML 文档中编码的数据。 XML 文档由根 Envelope 元素组成，而根 Envelope 元素又由必需的 Body 元素和可选的 Header 元素组成。 Body 元素包含特定于相应消息的数据。 可选的 Header 元素包含与特定消息并不直接相关的其他信息。 Header 元素的每一子元素都称为 SOAP 标头。  
  
 尽管 SOAP 标头可以包含与相应消息相关的数据，但是一般而言， SOAP 标头包含的是 Web 服务器基础结构所处理的信息。  
  
 报表服务器 Web 服务定义几个可在 SOAP 标头中使用的类：<xref:ReportService2005.BatchHeader>、<xref:ReportService2010.ItemNamespaceHeader>、<xref:ReportService2010.ServerInfoHeader>、<xref:ReportService2010.TrustedUserHeader> 和 <xref:ReportExecution2005.ExecutionHeader>。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[批处理方法](batching-methods.md)|介绍如何使用 <xref:ReportService2005.BatchHeader> 将多个操作纳入一个事务中进行批处理。|  
|[标识执行状态](identifying-execution-state.md)|介绍如何使用 SessionHeader 管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的会话状态。|  
|[为 GetProperties 方法设置项命名空间](setting-the-item-namespace-for-the-getproperties-method.md)|介绍如何通过使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法和 <xref:ReportService2010.ItemNamespaceHeader> SOAP 标头来根据项的路径或 ID 检索属性。|  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技术参考 (SSRS)](../technical-reference-ssrs.md)  
  
  
