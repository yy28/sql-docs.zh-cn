---
title: "“创建网站”对话框（Master Data Services 配置管理器）| Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 72b03df097b9951384674abbb984636b8999abf7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>“创建网站”对话框（Master Data Services 配置管理器）
  使用 **“创建网站”** 对话框可以在本地计算机上创建新网站。 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中创建网站时，该网站将添加到本地计算机上的 Internet Information Services (IIS)，并且具有配置为 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的根应用程序。 还将创建一个新的应用程序池，并且 Web 应用程序将放置在该应用程序池中。  
  
## <a name="web-site"></a>网站  
  
|控件名称|Description|  
|------------------|-----------------|  
|**网站名称**|为网站键入名称，或使用默认名称。 此名称是仅用来在 IIS 中标识站点的友好名称。 它不用于从 Web 浏览器访问网站。<br /><br /> 在本地计算机上 IIS 的所有网站中，该名称必须唯一。|  
|**协议**|显示 **“http”**。 在您不需要通过加密通道进行客户端和服务器通信时，使用超文本传输协议 (HTTP)。<br /><br /> **注意**：不能在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中创建 HTTPS 站点。 HTTPS 是使用安全套接字层 (SSL) 的 HTTP 协议；在交换机密数据或个人数据时，或者用户希望在传输个人信息前确认服务器的标识时，HTTPS 将很有用。 如果需要通过加密通道在服务器和客户端之间传输信息，则必须使用 IIS 工具（如 IIS 管理器）来配置该站点绑定到 HTTPS，并使该网站绑定与服务器证书关联起来；只有这样做才能在 Web 浏览器中成功打开该网站。 有关服务器证书的详细信息，请参阅 [TechNet 上的](http://go.microsoft.com/fwlink/?LinkId=163220) 在 IIS 7 中配置服务器证书 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。|  
|**IP 地址**|选择用户可用于访问网站的 IP 地址。 默认情况下，选择 **“所有未分配的”** 。 除非您另有原因来使用特定的 IPv4 或 IPv6 地址，否则将使用默认值。<br /><br /> 使用 **“所有未分配的”**，该网站将响应针对您指定的端口和可选主机名上所有 IP 地址的请求。 如果该服务器上的另一个网站在相同端口上具有一个绑定，但采用特定的 IP 地址，则该网站将接收对该端口和特定 IP 地址的 HTTP 请求，并且具有 **“所有未分配的”** IP 地址的网站将接收对该端口和其他 IP 地址的所有其他 HTTP 请求。|  
|**端口**|键入请求访问此网站时所对应的端口。 如果选择 HTTP 协议，则默认端口为 80。 如果您指定不同于默认端口的端口，则客户端必须指定端口号以便连接到该网站。<br /><br /> **注意**：IIS 中的“默认网站”配置为在端口 80 上将 HTTP 协议用于所有未分配的 IP 地址。 如果您尝试在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中使用默认绑定信息创建网站，则将收到一个错误消息，指示存在重复的绑定。 您必须或者更改 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中网站的绑定信息，或者通过使用 IIS 管理器之类的 IIS 工具更改默认网站的绑定信息。 或者，您可以指定一个主机标头以使 IIS 能够唯一标识该网站。 请确保将防火墙配置为通过您指定的端口接受通信。|  
|**主机标头**|可选值。 键入主机标头名称。 在您想要将一个主机名（也称作域名）分配给使用单个 IP 地址或端口的计算机时，使用此主机标头。 在您指定主机名后，客户端必须使用该名称而非 IP 地址来访问网站。 在您配置主机名后，在您的 DNS 服务器具有针对该主机名的条目之前，不能在 Web 浏览器中打开该网站。<br /><br /> 例如，如果希望用户访问位于 `http://www.contoso.com/` 的站点，则必须指定 www.contoso.com 作为主机名，并且 DNS 服务器必须具有针对它的条目。<br /><br /> 如果可在 Intranet 上找到网站，当用户在浏览器中键入服务器名称（例如，`http://server_name`）时，无需指定主机名。 但是，如果您的环境中的 DNS 服务器被配置为存储此 Web 服务器的其他名称，则您可以为每个主机名创建单独的绑定，以便用户可以使用 DNS 服务器存储的其他名称。 如果您必须为您的网站配置多个主机名，则应使用 IIS 管理器之类的 IIS 工具添加附加的网站绑定。|  
  
## <a name="application-pool"></a>应用程序池  
  
|控件名称|Description|  
|------------------|-----------------|  
|**名称**|为新的应用程序池键入唯一的友好名称，或者使用提供的默认名称。 此网站的根 Web 应用程序在此应用程序池中运行。<br /><br /> 应用程序池提供的边界可防止一个应用程序池中的应用程序影响另一个应用程序池中的应用程序。|  
|**用户名**|键入来自 Active Directory 的域名和用户名。 此帐户是 Web 应用程序运行所在的应用程序池的标识。<br /><br /> 此帐户添加到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的 mds_exec 数据库角色，以便访问数据库。 有关详细信息，请参阅[数据库登录、用户和角色 (Master Data Services)](../master-data-services/database-logins-users-and-roles-master-data-services.md)。 它还会被添加到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows 组 **MDS_ServiceAccounts**，该组有权访问文件系统中的临时编译目录 **MDSTempDir**。 有关详细信息，请参阅[文件夹和文件权限 (Master Data Services)](../master-data-services/folder-and-file-permissions-master-data-services.md)。|  
|**密码**|键入指定用户帐户的密码。|  
|**确认密码**|重新键入指定用户帐户的密码。 **“密码”** 字段和 **“确认密码”** 字段必须包含相同的密码。|  
  
## <a name="see-also"></a>另请参阅  
 [“Web 配置”页（Master Data Services 配置管理器）](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)[Web 应用程序要求 &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [创建主数据管理器 Web 应用程序 &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  

