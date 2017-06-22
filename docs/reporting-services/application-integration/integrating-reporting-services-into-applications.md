---
title: "到应用程序集成 Reporting 服务 |Microsoft 文档"
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
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
caps.latest.revision: 57
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8a1cabc088c7c0ec6c69c8290549e035a4cec7bb
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-into-applications"></a>将 Reporting Services 集成到应用程序中
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是一个开放和可扩展的报表平台，设计用于向开发人员提供一整套用于开发解决方案的 API。  
  
 有三个选项用于集成[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到自定义应用程序： 报表服务器 Web 服务，也称为[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SOAP API 的 ReportViewer 控件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]，和 URL 访问。 每个选项都提供一个不同的方法来将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到应用程序中。  
  
## <a name="report-server-web-service"></a>报表服务器 Web 服务  
 报表服务器 Web 服务是针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 进行开发的主接口。 无论您是开发代码以管理报表目录，还是开发代码以便用支持的格式呈现报表，该 Web 服务都公开所有必需的方法以便将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到您的应用程序中。 这样一个应用程序的一个示例是报表管理器，它又包括在[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; 它使用 Web 服务来管理报表服务器数据库。  
  
## <a name="reportviewer-controls-for-visual-studio"></a>用于 Visual Studio 的 ReportViewer 控件  
 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] 随附的 ReportViewer 控件用于将报表查看集成到您的应用程序中。 存在两个此类控件：一个用于基于 Windows 窗体的应用程序，另一个用于 Web 窗体应用程序。 每个控件都提供查看已部署到报表服务器的报表的功能以及呈现在尚未安装报表服务器的环境中存在的报表的功能。  
  
## <a name="url-access"></a>URL 访问  
 URL 访问是用于将报表查看集成到您的应用程序中的另一个选项（如果无法选择 ReportViewer 控件）。 此外，URL 访问还用于通过电子邮件将指向报表的链接发送给用户。  
  
## <a name="in-this-section"></a>本节内容  
 [集成使用 SOAP 的 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 说明如何使用报表服务器 Web 服务将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航和管理集成到您的现有业务应用程序中。  
  
 [集成 Reporting Services 使用的 ReportViewer 控件](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 说明如何使用 ReportViewer 控件将报表查看集成到您的现有应用程序中。  
  
 [将使用 URL 访问的 Reporting Services 的集成](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 说明如何使用 URL 访问将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航集成到您的现有业务应用程序中。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [URL 访问和 SOAP 之间进行选择](../../reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [技术参考 (SSRS)](../../reporting-services/technical-reference-ssrs.md)   
 [报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
