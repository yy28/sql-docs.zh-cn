---
title: "配置 Reporting Services 使用使用者可选名称 |Microsoft 文档"
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
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c4d975e93e77f43c481b44644faaa310963527b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>配置 Reporting Services 使用使用者备用名称
  本主题说明了如何通过修改 rsreportserver.config 文件和使用 Netsh.exe 工具配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) 以使用使用者可选名称 (SAN)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
 该说明适用于 Reporting Service URL 以及 Web 服务 URL。  
  
 要使用 SAN，SSL 证书必须在服务器上注册，签名并且获得私钥。 你无法使用自签名证书。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 URL 可配置为使用 SSL 证书。 一个证书通常只有一个使用者名称，此名称针对一个 SSL（安全套接字层）会话只允许一个 URL。 SAN 是证书中的附加字段，允许 SSL 服务进行侦听，对许多 URL 有效，并与其他应用程序共享 SSL 端口。 SAN 的形式如下：www.s2.com。  
  
 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SSL 设置的详细信息，请参阅 [配置本机模式报表服务器上的 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>将 SSRS 配置为使用适用于 Web 服务 URL 的使用者备用名称  
  
1.  启动 Reporting Services 配置管理器。  
  
     有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在“Web 服务 URL”  页面上，选择一个 SSL 端口和 SSL 证书。  
  
     ![Reporting Services 配置管理器](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services 配置管理器")  
  
     配置管理器注册端口的 SSL 证书。  
  
3.  打开 rsreportserver.config 文件。  
  
     对于 SSL 本机模式，默认情况下，该文件位于以下文件夹。  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  复制 Report Server Web 服务应用程序的 URL 部分。  
  
     例如，以下是初始 URL 部分。  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     以下是修改了的 URL 部分。  
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  保存 rsreportserver.config 文件。  
  
6.  以管理员身份启动一个命令提示符并运行 Netsh.exe 工具。  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  键入以下内容切换至 http 上下文。  
  
    ```  
    Netsh>http  
    ```  
  
8.  键入以下内容显示现有 urlacl。  
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     出现如下条目。  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     一个 urlacl 是一个保留的 URL 的 DACL（自由访问控制列表）。  
  
9. 通过键入以下内容，为使用者备用名称创建一个用户和 SDDL 与现有条目相同的新条目。  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. 在 Reporting Services 配置管理器的“报表服务器状态”  页面上单击“停止”  ，然后单击“启动”  以重启报表服务器。  
  
## <a name="see-also"></a>另請參閱  
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 配置管理器 &#40;本机模式 &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [修改 Reporting Services 配置文件 &#40;RSreportserver.config &#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [配置报表服务器 Url &#40;SSRS 配置管理器 &#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
