---
title: "将 Reporting Services 集成到应用程序中 | Microsoft Docs"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7c3b7555475c79f41fe0fbf577df5263bc166ce5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-into-applications"></a>将 Reporting Services 集成到应用程序中

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是一个开放和可扩展的报表平台，设计用于向开发人员提供一整套用于开发解决方案的 API。

> [!NOTE]
> 从 SQL Server 2017 Reporting Services 开始，REST API 访问可用于开发解决方案。 已弃用 SOAP API 访问。 有关详细信息，请参阅[使用 Reporting Services 的 REST API 进行开发](../developer/rest-api.md)。
  
 有三个选项可用于将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义应用程序中：报表服务器 Web 服务（也称作 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API）、用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的 ReportViewer 控件和 URL 访问。 每个选项都提供一个不同的方法来将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到应用程序中。
  
## <a name="report-server-web-service"></a>报表服务器 Web 服务

 报表服务器 Web 服务是针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 进行开发的主接口。 无论您是开发代码以管理报表目录，还是开发代码以便用支持的格式呈现报表，该 Web 服务都公开所有必需的方法以便将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到您的应用程序中。 报表管理器就是此类应用程序的一个示例，报表管理器随 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 一起提供，它使用该 Web 服务管理报表服务器数据库。  
  
## <a name="reportviewer-controls-for-visual-studio"></a>用于 Visual Studio 的 ReportViewer 控件

 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 随附的 ReportViewer 控件用于将报表查看集成到应用程序中。 存在两个此类控件：一个用于基于 Windows 窗体的应用程序，另一个用于 Web 窗体应用程序。 每个控件都提供查看已部署到报表服务器的报表的功能以及呈现在尚未安装报表服务器的环境中存在的报表的功能。  
  
## <a name="url-access"></a>URL 访问  
 URL 访问是用于将报表查看集成到您的应用程序中的另一个选项（如果无法选择 ReportViewer 控件）。 此外，URL 访问还用于通过电子邮件将指向报表的链接发送给用户。  
  
## <a name="in-this-section"></a>在本节中

 [使用 SOAP 集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 说明如何使用报表服务器 Web 服务将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航和管理集成到您的现有业务应用程序中。  
  
 [使用 ReportViewer 控件集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 说明如何使用 ReportViewer 控件将报表查看集成到您的现有应用程序中。  
  
 [使用 URL 访问集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 说明如何使用 URL 访问将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航集成到您的现有业务应用程序中。  
  
## <a name="next-steps"></a>后续步骤

要决定是使用 URL 访问还是 SOAP API，请参阅[在 Reporting Services 中的 URL 访问和 SOAP 之间选择](choosing-between-url-access-and-soap.md)。

有关 SQL Server 2017 Reporting Services REST API 的信息，请参阅[使用 Reporting Services 的 REST API 进行开发](../developer/rest-api.md)。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
