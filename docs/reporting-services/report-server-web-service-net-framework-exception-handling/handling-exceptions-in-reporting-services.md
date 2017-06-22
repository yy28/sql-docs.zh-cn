---
title: "Reporting Services 中处理异常 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
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
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1cf3ca01075260274b363736bd53c245809e521c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>在 Reporting Services 中处理异常
  在无法完成某一 Reporting Services SOAP API 客户端请求时，报表服务器将返回错误，而非预期调用结果。 在完成后调用，不能作为 SOAP 返回报表服务器 Web 服务错误**错误**XML 元素。 错误的密钥描述性元素是**详细信息**元素，其中包括所有由报表服务器以及任何附加的 Web 服务错误信息提供的错误信息。 中的密钥信息**详细信息**元素是报表服务器错误代码。 基于这些消息和错误代码，您可以确定要在应用程序中执行的相应后续操作。 有关 SOAP 错误的详细信息，请参阅万维网联合会 (W3C) 网站，网址为 http://www.w3.org/TR/SOAP。  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 错误和 .NET Framework  
 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，如果对 Web 服务客户端请求中发生错误，报表服务器进行通信，客户端调用的代码，Web 服务通过引发的错误**SoapException**对象。 **SoapException**包装 SOAP 错误中包含的信息。 **详细信息**属性**SoapException**映射到**详细信息**SOAP 错误中的元素。 应用程序应捕获**SoapException**对象使用 try/catch 块，并使用**详细信息**属性**SoapException**以采取相应的操作。 有关详细信息**SoapException**类和**详细信息**中的属性[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请参阅[Reporting Services SoapException 类](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)。 有关详细信息**SoapException**类，请参阅[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档。  
  
## <a name="see-also"></a>另请参阅  
 [详细信息属性](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [引入了 Reporting Services 中的异常处理](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
