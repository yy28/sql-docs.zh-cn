---
title: "报表服务器 Web 服务 |Microsoft 文档"
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
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 10769f49396bcf32d437e4bee9b04cbc2a3c8d9c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-web-service"></a>报表服务器 Web 服务
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供对报表服务器通过报表服务器 Web 服务的完整功能的访问。 报表服务器 Web 服务是具有 SOAP API 的 XML Web 服务。 它使用 HTTP 上的 SOAP (SOAP over HTTP)，并且充当客户端程序与报表服务器之间的通信接口。 该 Web 服务提供两个端点（一个用于报表执行，一个用于报表管理）以及公开报表服务器的功能和使您能够为报表生命周期的任何部分创建自定义工具的方法。  
  
 有三种主要方式开发[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]基于 Web 服务应用程序。 您可以：  
  
-   开发应用程序使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。 有关使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]若要生成 Web 服务应用程序，请参阅[生成应用程序使用 Web 服务和.NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
-   开发应用程序使用**rs**实用工具 (RS.exe)[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]脚本环境。 与[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]脚本，你可以运行任何报表服务器 Web 服务操作。 有关详细信息中脚本[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请参阅[脚本使用 rs.exe 实用工具和 Web 服务](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)。  
  
-   使用任何支持 SOAP 的开发工具集开发应用程序。 有关详细信息，请参阅[The Role of SOAP in Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)。  
  
## <a name="programming-diagram"></a>编程关系图  
 ![报表服务器 Web 服务开发选项](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "报表服务器 Web 服务开发选项")  
Reporting Services 可用 Web 服务开发选项  
  
## <a name="in-this-section"></a>本節內容  
 [报表服务器 Web 服务方法](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 介绍每个报表服务器 Web 服务的功能和方法。  
  
 [SOAP 在 Reporting Services 中的作用](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 概述 SOAP 以及如何在报表服务器 Web 服务中使用 SOAP。  
  
 [访问 SOAP API](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 介绍 Web 服务描述语言 (WSDL) 并提供用于访问 Reporting Services WSDL 文件的 URL。  
  
 [使用 Web 服务和.NET Framework 构建应用程序](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 包含与开发调用 Reporting Services SOAP API 的应用程序和 Web 服务有关的信息。  
  
 [使用 rs.exe 实用工具和 Web 服务的脚本](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 概要介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 脚本编写环境。  
  
 [技术参考 &#40;SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
 包含特定于报表服务器 Web 服务方法以及相应复杂类型的参考材料。  
  
## <a name="user-requirements-for-web-service-development"></a>针对 Web 服务开发的用户要求  
 若要使用报表服务器 Web 服务开发应用程序，您需要：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 5.5 或更高版本安装在具有 Internet 连接和访问报表服务器的计算机上。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]如果你想要开发和部署的计算机上安装的 SDK[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]使用应用程序[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。  
  
-   深入了解[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特性和功能。  
  
-   扎实理解 SOAP 和 [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)]。  
  
-   中的开发体验[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-兼容语言[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[csprcs](../../includes/csprcs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]，如果你打算使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]作为你的开发平台。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
