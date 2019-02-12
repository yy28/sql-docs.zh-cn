---
title: 在 Web 应用程序中使用 SOAP API | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a68100af72b7680ed1a9212f5d7c6c54ed07bec1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013020"
---
# <a name="using-the-soap-api-in-a-web-application"></a>在 Web 应用程序中使用 SOAP API
  可以通过 Reporting Services SOAP API 访问报表服务器的完整功能。 因为它是一个 Web 服务，所以您可以轻松地访问 SOAP API 以向自定义业务应用程序提供企业报表功能。 从 Web 应用程序访问报表服务器 Web 服务的方法与从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序访问 SOAP API 的方法非常类似。 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，可以生成一个代理类，它公开报表服务器 Web 服务的属性和方法，并使你能够使用熟悉的基础结构和工具来生成建立在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 技术之上的业务应用程序。  
  
 从 Web 应用程序访问 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表管理功能与从 Windows 应用程序进行访问一样简单。 在 Web 应用程序中，您可以从报表服务器数据库添加和删除项，设置项安全性，修改报表服务器数据库项，管理计划和传递以及等等。  
  
## <a name="enabling-impersonation"></a>启用模拟  
 配置 Web 应用程序的第一步是从 Web 服务客户端启用模拟。 在模拟模式中，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序可以使用它们实际运行时所用的客户端身份来运行。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 依赖于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 来对用户身份进行验证，并将已验证的标记传递到 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序，或者，在无法对用户身份进行验证的情况下，传递未通过身份验证的标记。 在任一种情况下，如果启用了模拟，则无论收到哪种标记，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序都会进行模拟。 您可以对于客户端启用模拟，为此，请按以下所示修改客户端应用程序的 Web.config 文件：  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  默认情况下，模拟处于禁用状态。  
  
 有关 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 模拟的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档。  
  
## <a name="managing-the-report-server-using-soap-api"></a>使用 SOAP API 管理报表服务器  
 还可以使用 Web 应用程序管理报表服务器及其内容。 随 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供的报表管理器是完全使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 和 Reporting Services SOAP API 生成的 Web 应用程序的一个示例。 您可以将报表管理器的报表管理功能添加到自定义 Web 应用程序。 例如，你可能想要在报表服务器数据库中返回可用报表的列表，并将它们显示在[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]`Listbox`为您的用户可供选择的控件。 下面的代码连接到报表服务器数据库并返回报表服务器数据库中的项列表。 然后，将可用报表添加到 Listbox 控件，而该控件显示每个报表的路径。  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [将 Reporting Services 集成到应用程序中](../application-integration/integrating-reporting-services-into-applications.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 [在 Windows 应用程序中使用 SOAP API](integrating-reporting-services-using-soap-windows-application.md)  
  
  
