---
title: 报表服务器 Web 服务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b577fd9a78dbb5f12af79e190709065931ec463a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62520551"
---
# <a name="report-server-web-service"></a>报表服务器 Web 服务
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]通过报表服务器 Web 服务提供对 Report Server 的全部功能的访问。 报表服务器 Web 服务是具有 SOAP API 的 XML Web 服务。 它使用 HTTP 上的 SOAP (SOAP over HTTP)，并且充当客户端程序与报表服务器之间的通信接口。 该 Web 服务提供两个端点（一个用于报表执行，一个用于报表管理）以及公开报表服务器的功能和使您能够为报表生命周期的任何部分创建自定义工具的方法。  
  
 可以通过三个主要方法基于 Web 服务开发 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序。 你可以：  
  
-   使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)]和[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 开发应用程序。 有关使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 生成 Web 服务应用程序的详细信息，请参阅[使用 Web 服务和 .NET Framework 生成应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
-   使用 **rs** 实用工具 (RS.exe)（ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 脚本环境）开发应用程序。 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 脚本，可以运行任何报表服务器 Web 服务操作。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中脚本编写的详细信息，请参阅[使用 rs.exe 实用工具和 Web 服务编写脚本](../tools/script-with-the-rs-exe-utility-and-the-web-service.md)。  
  
-   使用任何支持 SOAP 的开发工具集开发应用程序。 有关详细信息，请参阅 [SOAP 在 Reporting Services 中的作用](../report-server-web-service/the-role-of-soap-in-reporting-services.md)。  
  
## <a name="programming-diagram"></a>编程关系图  
 ![报表服务器 Web 服务部署选项](../../../2014/reporting-services/media/reportserviceswebserviceprog-01.gif "报表服务器 Web 服务部署选项")  
Reporting Services 可用 Web 服务开发选项  
  
## <a name="in-this-section"></a>本节内容  
 [报表服务器 Web 服务方法](../report-server-web-service/methods/report-server-web-service-methods.md)  
 介绍每个报表服务器 Web 服务的功能和方法。  
  
 [The Role of SOAP in Reporting Services](../report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 概述 SOAP 以及如何在报表服务器 Web 服务中使用 SOAP。  
  
 [访问 SOAP API](../report-server-web-service/accessing-the-soap-api.md)  
 介绍 Web 服务描述语言 (WSDL) 并提供用于访问 Reporting Services WSDL 文件的 URL。  
  
 [使用 Web 服务和 .NET Framework 生成应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 包含与开发调用 Reporting Services SOAP API 的应用程序和 Web 服务有关的信息。  
  
 [使用 rs.exe 实用工具和 Web 服务编写脚本](../tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 概要介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 脚本编写环境。  
  
 [技术参考 (SSRS)](../../../2014/reporting-services/technical-reference-ssrs.md)  
 包含特定于报表服务器 Web 服务方法以及相应复杂类型的参考材料。  
  
## <a name="user-requirements-for-web-service-development"></a>针对 Web 服务开发的用户要求  
 若要使用报表服务器 Web 服务开发应用程序，您需要：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 或更高版本安装在具有与报表服务器的 Internet 连接或能够访问报表服务器的计算机上。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]或者，如果要使用开发和部署应用程序，则在计算机上安装 SDK。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   深入了解[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特性和功能。  
  
-   扎实理解 SOAP 和 [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)]。  
  
-   如果你计划将[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]用作开发平台，则[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)]采用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]与兼容的语言（如或）的开发体验。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器 Web 服务](../report-server-web-service/report-server-web-service.md)  
  
  
