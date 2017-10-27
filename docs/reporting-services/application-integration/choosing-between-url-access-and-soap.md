---
title: "选择 URL 访问和 SOAP in Reporting Services 之间 |Microsoft 文档"
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
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 1d9b4df388cd1d6bb96d88b64bf319f5fd9866e9
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>URL 访问和 SOAP in Reporting Services 之间选择

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义应用程序的过程可能充满挑战。 然而，这样的挑战并不在于编程模型或 API 有多么复杂，而在于如何从众多可能的集成方法中选择一种合适的方法。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 最初的设计就是一个开发平台，因此在构建时考虑了编程的灵活性。 在满足灵活性要求后，接下来需要决定如何将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航和管理功能集成到现有业务应用程序中。

> [!NOTE]
> 从开始 SQL Server 自 2017 年 Reporting Services，REST API 访问权限是可用于开发解决方案。 已弃用 SOAP API 访问。 有关详细信息，请参阅[Reporting Services REST api 开发](../developer/rest-api.md)。
  
 可以通过两种方法将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义应用程序中：URL 访问和 Reporting Services SOAP API。 具体使用哪种方法取决于若干因素。 在某些情况下，将集成[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到自定义业务应用程序需要使用 URL 访问和 SOAP。 您应提出以下问题：  
  
-   您或您的最终用户需要哪种企业报表功能？ 您是需要一种简单的方法来启动和导航报表，还是需要由自定义业务解决方案提供更高级的报表服务器管理功能？  
  
-   您的用户通常在哪种环境下运行？ 您的业务应用程序是 Web 应用程序还是 Windows 应用程序？ 如何轻松地可以最终用户从切换 Win32 环境到 Web 环境？ 您需要对在其中运行和管理报表的环境具有哪种控制权？  
  
 一旦您回答了前面的问题，您就可以决定如何将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到您的 IT 基础结构中。 通常，若要查看和导航单独的报表，将首选 URL 访问。 借助于 URL 访问，您可以顺畅、快速地导航报表，而没有 Web 服务的开销。 此外，URL 访问目前是使用完整的 HTML 查看器（其中包含报表工具栏）进行报表导航的唯一编程技术。 此外，由于 URL 访问绕过了针对进出服务器的 SOAP 请求进行封送处理的过程，因此，其性能高于 SOAP。 在要求使用内置工具进行查看和导航以轻松快捷地访问报表的集成方案中，URL 访问是更好的选择。  
  
> [!NOTE]  
> 报表服务器 URL 访问支持 HTML 查看器以及报表工具栏的扩展功能。 SOAP API 不支持这一类型的呈现的报表。 如果呈现报表使用 SOAP API，设计和开发您自己的报表工具栏。
  
 有关报表工具栏的详细信息，请参阅[HTML 查看器和报表工具栏](../../reporting-services/html-viewer-and-the-report-toolbar.md)。  
  
 有关 URL 访问的详细信息，请参阅[URL 访问](../../reporting-services/url-access-ssrs.md)。  
  
 URL 访问可用于查看报表，但它不提供报表和命名空间管理功能，而这一功能对于任何企业报表方案是必不可少的。 在这种情况下，建议使用 Reporting Services SOAP API 的广泛和丰富的功能。 通过 SOAP API，您可以管理和部署报表、创建计划、配置服务器属性、管理报表服务器命名空间、创建订阅等等。 SOAP API 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中公开一组完整的管理功能。 借助于 SOAP API，还可以通过 API 的 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法查看和导航报表。 但是，查看通过 SOAP API 的报表不启用报表工具栏上，也不会自动处理 URL 访问提供的报表交互性的内置的查看功能。  
  
 有关 Reporting Services SOAP API 的详细信息，请参阅[报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)。  
  
 在绝大多数情况下，要求同时使用 URL 访问和 SOAP 调用以满足您的报表需要。 最初连接到报表服务器数据库并在用户界面中提供可用的报表列表时，将使用 SOAP；而 URL 访问用于实际访问和导航单独的报表。  
  
 URL 访问与 Web 服务以提供集成的报告的组合示例，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

