---
title: "配置 Reporting Services 使用使用者可选名称 |Microsoft 文档"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 73f48b2978055481f1ee93952fb3a35eb84ec416
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>配置 Reporting Services 使用使用者可选名称

本主题说明如何配置 Reporting Services (SSRS) 用于使用者可选名称 (SAN) 通过修改 rsreportserver.config 文件并使用 Netsh.exe 工具。

该说明适用于 Reporting Service URL 以及 Web 服务 URL。

要使用 SAN，SSL 证书必须在服务器上注册，签名并且获得私钥。 你无法使用自签名证书。  
  
 Reporting Services 中的 Url 可以配置为使用 SSL 证书。 一个证书通常只有一个使用者名称，此名称针对一个 SSL（安全套接字层）会话只允许一个 URL。 SAN 是允许 SSL 服务侦听多个 Url，并与其他应用程序共享 SSL 端口的证书中的附加字段。 SAN 如下所示`www.s2.com`。  
  
 有关 Reporting Services 的 SSL 设置的详细信息，请参阅[配置本机模式报表服务器上的 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>SSRS 配置为使用 web 服务 URL 的使用者备用名称
  
1.  启动 Reporting Services 配置管理器。  
  
     有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在“Web 服务 URL”  页面上，选择一个 SSL 端口和 SSL 证书。  
  
     ![Reporting Services 配置管理器](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services 配置管理器")  
  
     配置管理器注册端口的 SSL 证书。  
  
3.  打开 rsreportserver.config 文件。  
  
     SSRS 本机模式下，该文件位于以下文件夹中的默认情况下：  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  复制 Report Server Web 服务应用程序的 URL 部分。  
  
     例如，以下的初始 URL 部分是：  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     以下修改后的 URL 部分是：
  
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
  
8.  通过键入以下内容显示现有 urlacl:
  
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
  
## <a name="see-also"></a>另请参阅

 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 配置管理器](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [修改 Reporting Services 配置文件](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [配置报表服务器 Url](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
