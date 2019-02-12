---
title: 配置 Reporting Services 以使用使用者可选名称 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: a1b5ead3e2ab16eea905af3312779631ae6344ea
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026761"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>配置 Reporting Services 使用使用者备用名称
  本主题说明了如何通过修改 rsreportserver.config 文件和使用 Netsh.exe 工具配置 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) 以使用使用者可选名称 (SAN)。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式|  
  
 该说明适用于 Reporting Service URL 以及 Web 服务 URL。  
  
 要使用 SAN，SSL 证书必须在服务器上注册，签名并且获得私钥。 你无法使用自签名证书。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的 URL 可配置为使用 SSL 证书。 一个证书通常只有一个使用者名称，此名称针对一个 SSL（安全套接字层）会话只允许一个 URL。 SAN 是证书中的附加字段，允许 SSL 服务进行侦听，对许多 URL 有效，并与其他应用程序共享 SSL 端口。 SAN 的形式如下：www.s2.com。  
  
 有关 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SSL 设置的详细信息，请参阅 [配置本机模式报表服务器上的 SSL 连接](security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>将 SSRS 配置为使用适用于 Web 服务 URL 的使用者备用名称  
  
1.  启动 Reporting Services 配置管理器。  
  
     有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在“Web 服务 URL”  页面上，选择一个 SSL 端口和 SSL 证书。  
  
     ![Reporting Services 配置管理器](media/reportingservices-configurationmanager.png "Reporting Services Configuration Manager")  
  
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
  
## <a name="see-also"></a>请参阅  
 [RSReportServer 配置文件](report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services Configuration Manager（本机模式）](../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [配置报表服务器 URL（SSRS 配置管理器）](install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
