---
title: 介绍 Reporting Services 中的异常处理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
caps.latest.revision: 28
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: de3d63926b2dfde735403b21f5c986d5b4241198
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127243"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>介绍 Reporting Services 中的异常处理
  如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序将某一请求发送到报表服务器 Web 服务但该服务无法处理该请求，则该服务会将一个 SOAP 异常返回到客户端。 处理报表服务器 Web 服务引发的异常是您开发的应用程序的重要一环，因为可以在错误发生时将有用信息返回给用户。  
  
 本节包含有关处理异常、防止无效用户输入和向用户返回有意义的错误信息的具体信息。 有关异常处理的一般信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的“处理和引发异常”。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[在 Reporting Services 中处理异常](handling-exceptions-in-reporting-services.md)|概述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的异常以及 SOAP 在从 Web 服务返回错误时的角色。|  
|[Reporting Services 异常处理的最佳做法](best-practices/best-practices-for-reporting-services-exception-handling.md)|就如何在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中处理异常提供建议。|  
|[Reporting Services SoapException 类](soapexception-class/reporting-services-soapexception-class.md)|介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 SoapException 类。|  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  