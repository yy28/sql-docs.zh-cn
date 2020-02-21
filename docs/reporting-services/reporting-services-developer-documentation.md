---
title: Reporting Services 开发人员文档 | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.date: 03/17/2017
ms.openlocfilehash: e2db4a113ebdb53756200879e3797ccbbeec8a52
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68259608"
---
# <a name="reporting-services-developer-documentation"></a>Reporting Services 开发人员文档
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了多个编程接口，你可以在自己的应用程序中利用这些接口。 您可以使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的现有特性和功能将自定义报表和管理工具置入网站和 Windows 应用程序，也可以扩展 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 平台。  
  
 扩展 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 平台包括创建可用于数据访问、报表传递等等的新组件和资源。 可以向在其组织中使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的公司销售这些组件和资源。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括可帮助您入门的编程示例和教程。 有关详细信息，请参阅 [Reporting Services 示例](https://msdn.microsoft.com/library/ms160954\(v=sql.110\).aspx)和[开发人员指南：教程 (Reporting Services)](https://msdn.microsoft.com/library/aa337423\(v=sql.110\).aspx)。  
  
## <a name="in-this-section"></a>本节内容  
 [将 Reporting Services 集成到应用程序中](../reporting-services/application-integration/integrating-reporting-services-into-applications.md)  
 概述如何使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 将报表功能集成到自定义应用程序中。 介绍何时使用直接 URL 访问以及何时使用 Web 服务来访问报表服务器。  
  
 [适用于 ASP.net 和传统应用程序的报表服务器 Web 服务](../reporting-services/report-server-web-service/report-server-web-service.md)  
 通过报表服务器 Web 服务，可以访问报表服务器的完整功能。 Web 服务使用 HTTP 上的 SOAP (SOAP over HTTP)，它旨在充当客户端程序与报表服务器之间的通信接口。 Web 服务及其方法公开报表服务器的功能，并使您能够为报表生命周期的任何部分（从管理到执行）创建自定义工具。  
 
 [使用适用于现代应用程序的 REST API 进行开发](developer/rest-api.md)</br>
 Reporting Services REST API 提供对 Reporting Services 报表服务器目录中对象的编程访问。 使用 REST API 时，可以导航到文件夹层次结构、发现文件夹的内容或下载报表定义。 此外还可创建、更新和删除对象。

 [URL 访问 (SSRS)](../reporting-services/url-access-ssrs.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持一组完整的基于 URL 的请求，您可以将这些请求用作进行报表导航和查看的快捷访问点。 可以将此技术与报表服务器 Web 服务结合使用，以便将完整的报表解决方案集成到自定义业务应用程序中。 当将报表作为 Web 门户的一部分集成或从 Web 浏览器查看报表时，URl 访问尤其有用。  
  
 [Reporting Services 扩展插件](../reporting-services/extensions/reporting-services-extensions.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的模块化体系结构旨在实现可扩展性。 提供了一个托管代码 API，以便您能够轻松地开发、安装和管理由许多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 组件使用的扩展插件。 可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 创建程序集，并添加新的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 呈现、安全、传递和数据处理功能以满足不断发展的业务需求。  
  
 [自定义报表项](../reporting-services/custom-report-items/custom-report-items.md)  
 介绍如何创建自定义报表项，以便向 RDL 添加功能或扩展现有控件的功能。  
  
 [将自定义程序集用于报表](../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
 介绍如何通过在报表定义中加入代码引用，将自定义程序集用于报表。  
  
 [访问 Reporting Services WMI 提供程序](../reporting-services/tools/access-the-reporting-services-wmi-provider.md)  
 介绍如何使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] WMI 提供程序以管理报表服务器部署。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services (SSRS)](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)   
 [技术参考 (SSRS)](../reporting-services/technical-reference-ssrs.md)   
 [安全开发 (Reporting Services)](../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
