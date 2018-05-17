---
title: 在 Reporting Services 中处理异常 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 75bc7d7f057c9207a0f70525acf61072b82f3469
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="handling-exceptions-in-reporting-services"></a>在 Reporting Services 中处理异常
  在无法完成某一 Reporting Services SOAP API 客户端请求时，报表服务器将返回错误，而非预期调用结果。 在无法完成调用时，针对报表服务器 Web 服务的错误将以 SOAP Fault XML 元素的形式返回。 该错误的主要描述性元素是 detail 元素，它包括报表服务器提供的所有错误消息以及所有附加的 Web 服务错误信息。 detail 元素中的关键信息是报表服务器错误代码。 基于这些消息和错误代码，您可以确定要在应用程序中执行的相应后续操作。 有关 SOAP 错误的详细信息，请参阅万维网联合会 (W3C) 网站，网址为 http://www.w3.org/TR/SOAP。  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 错误和 .NET Framework  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中，如果在对 Web 服务的客户端请求中出现错误，则报表服务器将通过引发 SoapException 对象向调用 Web 服务的客户端代码传达此错误。 SoapException 包装 SOAP 错误中包含的信息。 SoapException 的 Detail 属性映射到 SOAP 错误中的 detail 元素。 应用程序应使用 try/catch 块捕获 SoapException 对象，并且使用 SoapException 的 Detail 属性执行适当操作。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 SoapException 类和 Detail 属性的详细信息，请参阅 [Reporting Services SoapException 类](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)。 有关 SoapException 类的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档。  
  
## <a name="see-also"></a>另请参阅  
 [Detail 属性](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [介绍 Reporting Services 中的异常处理](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
