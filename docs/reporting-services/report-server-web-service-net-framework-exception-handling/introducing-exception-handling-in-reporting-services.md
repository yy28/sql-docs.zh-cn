---
title: 介绍 Reporting Services 中的异常处理 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 823cf50514c9eae18b000d28f72e9f3f3c7ef81c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265723"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>介绍 Reporting Services 中的异常处理
  如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序将某一请求发送到报表服务器 Web 服务但该服务无法处理该请求，则该服务会将一个 SOAP 异常返回到客户端。 处理报表服务器 Web 服务引发的异常是您开发的应用程序的重要一环，因为可以在错误发生时将有用信息返回给用户。  
  
 本节包含有关处理异常、防止无效用户输入和向用户返回有意义的错误信息的具体信息。 有关异常处理的一般信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的“处理和引发异常”。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[在 Reporting Services 中处理异常](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|概述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的异常以及 SOAP 在从 Web 服务返回错误时的角色。|  
|[Reporting Services 异常处理的最佳做法](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|就如何在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中处理异常提供建议。|  
|[Reporting Services SoapException 类](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 SoapException 类。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
