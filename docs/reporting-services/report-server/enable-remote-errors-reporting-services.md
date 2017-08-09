---
title: "启用远程错误 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 20adc5eb8b830b960fe07d39f3717279abca3f23
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="enable-remote-errors-reporting-services"></a>启用远程错误 (Reporting Services)
  可以将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器上的服务器属性设置为返回远程服务器上所发生的错误情形的其他信息。 如果错误消息中包含文本“有关此错误的详细信息，请导航到本地服务器上的报表服务器或启用远程错误”，则可以将 **EnableRemoteErrors** 属性设置为访问可帮助您解决问题的其他信息。 有关详细信息，请参阅 [联机丛书中的](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md) 报表服务器系统属性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 本主题内容：  
  
-   [为 SharePoint 模式启用远程错误](#bkmk_sharepoint)  
  
-   [通过 SQL Server Management Studio 启用远程错误（本机模式）](#bkmk_mgtStudio)  
  
-   [通过脚本启用远程错误（本机模式）](#bkmk_script)  
  
-   [修改 ConfigurationInfo 表（本机模式）](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a> 为 SharePoint 模式启用远程错误  
 可以通过两个不同的过程为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式启用远程错误。 对于两个不同的报表服务器体系结构，过程是不同的。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本中引入的基于较新的 SharePoint 服务的体系结构利用可为每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序配置的设置。 较旧的体系结构利用单一站点级别的设置。  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>为 Reporting Services 服务应用程序启用远程错误  
  
1.  对于随 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或较新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一起安装的 SharePoint 模式报表服务器，启用服务应用程序设置 **“启用远程错误”**。 可为每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序配置该设置。  
  
2.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
3.  找到您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序并单击其名称。  
  
4.  单击 **“系统设置”**。  
  
5.  在 **“安全性”** 部分，单击 **“启用远程错误”** 。  
  
6.  单击 **“确定”**。  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>为 SharePoint 站点启用远程错误  
  
1.  对于随 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之前的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本安装的 SharePoint 模式报表服务器，启用站点设置 **“启用本地模式下的远程错误”**。  
  
2.  在 **“站点操作”** 中，单击您要修改的站点对应的 **“站点设置”** 。  
  
3.  在 **“Reporting Services”** 组，单击 **“Reporting Services 站点设置”** 。  
  
4.  单击 **“启用本地模式下的远程错误”**。  
  
5.  单击 **“确定”**。  
  
##  <a name="bkmk_mgtStudio"></a> 通过 SQL Server Management Studio 启用远程错误（本机模式）  
  
1.  启动 Management Studio 并连接到报表服务器实例。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[连接到 Management Studio 中的报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
2.  右键单击报表服务器节点，然后选择“属性”。  
  
3.  单击 **“高级”** 以打开属性页。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[服务器属性（“高级”页）- Reporting Services](../../reporting-services/tools/server-properties-advanced-page-reporting-services.md)。  
  
4.  在 **EnableRemoteErrors**中，选择 **True**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a> 通过脚本启用远程错误（本机模式）  
  
1.  创建文本文件并将以下脚本复制到该文件中。  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  将文件另存为 EnableRemoteErrors.rss。  
  
3.  单击 **“开始”**，指向 **“运行”**，键入 **cmd**，再单击 **“确定”** 打开命令提示符窗口。  
  
4.  导航到包含您刚刚创建的 .rss 文件的目录。  
  
5.  键入以下命令行，并将 *servername* 替换为服务器的实际名称：  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  有关详细信息，请参阅 [RS.exe 实用工具 (SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md)  
  
##  <a name="bkmk_ConfigurationInfo"></a> 修改 ConfigurationInfo 表（本机模式）  
  
1.  > [!NOTE]  
    >  您可以通过编辑报表服务器数据库中的 **ConfigurationInfo** 表将 **EnableRemoteErrors** 设置为 **True**，但是如果报表服务器正在使用中，则应使用 SQL Server Management Studio 或脚本来修改此设置。 如果修改了数据库中的设置，则需要重新启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务，然后更改才会生效。  
  
  
