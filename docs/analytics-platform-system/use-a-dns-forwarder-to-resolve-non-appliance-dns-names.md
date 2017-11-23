---
title: "使用 DNS 转发器来解析非设备 DNS 名称 (AP)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 123d8a83-b7fd-4dc9-90d4-fa01af2d629d
caps.latest.revision: "21"
ms.openlocfilehash: 6e91828bcc64a47d942959a2522af0e53041e027
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names"></a>使用 DNS 转发器来解析非设备 DNS 名称
可以在 Active Directory 域服务节点上配置 DNS 转发器 (***appliance_domain*-AD01**和 ***appliance_domain*-AD02**)你分析平台系统的设备为允许脚本和访问外部服务器的软件应用程序。  
  
## <a name="ResolveDNS"></a>使用 DNS 转发器  
分析平台系统设备被配置为阻止不在该设备的服务器的 DNS 名称解析。 某些进程，如 Windows 软件更新服务 (WSUS)，将需要访问外部设备的服务器。 若要支持这种使用方案分析平台系统 DNS 可以配置为支持将允许使用外部 DNS 服务器来解析外部设备的名称 Analytics Platform System 主机和虚拟机 (Vm) 的外部名称转发器。 不支持自定义配置的 DNS 后缀，这意味着你必须使用完全限定的域名来解析非设备服务器名称。  
  
**使用 DNS GUI 创建 DNS 转发器**  
  
1.  登录到 ***appliance_domain*-AD01**节点。  
  
2.  打开 DNS 管理器 (**dnsmgmt.msc**)。  
  
3.  右键单击服务器的名称，然后单击**属性**。  
  
4.  在**高级**选项卡上，取消选择**禁用递归 （也禁用转发器）**选项，并依次**应用**。)  
  
5.  单击**转发器**选项卡，然后单击**编辑**。  
  
6.  将提供的名称解析的外部 DNS 服务器输入的 IP 地址。 虚拟机和设备中的服务器 （主机） 将使用连接到外部服务器完全限定的域名。  
  
7.  重复步骤 1 – 6 上 ***appliance_domain*-AD02**节点  
  
**若要使用 Windows PowerShell 创建 DNS 转发器**  
  
1.  登录到 ***appliance_domain*-AD01**节点。  
  
2.  运行以下 Windows PowerShell 脚本从 ***appliance_domain*-AD01**节点。 在运行之前的 Windows PowerShell 脚本，将替换为你非设备的 DNS 服务器的 IP 地址的 IP 地址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在执行同一命令 ***appliance_domain*-AD02**节点。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>为 WSUS 配置 DNS 解析  
SQL Server PDW 2012 提供集成服务和修补功能。 SQL Server PDW 使用 Microsoft 更新和其他 Microsoft 服务技术。 若要启用该设备必须能够连接到公司的 WSUS 存储库中或 Microsoft 公共 WSUS 存储库的更新。  
  
对于选择配置设备以查找 Microsoft 公共 WSUS 存储库上的更新的客户，按照以下说明在设备上设置正确的配置详细信息。  
  
> [!NOTE]  
> 客户网络管理员必须为企业 DNS 服务器可以解析的名称提供 IP 地址**Microsoft.com**。  
  
1.  使用远程桌面，登录到 VMM VM (<fabric domain>VMM) 使用的 fabric 域管理员帐户。  
  
2.  打开控制面板，单击**网络和 Internet**，然后单击**网络和共享中心**。  
  
3.  在连接列表中，单击**VMSEthernet**，然后单击**属性**。  
  
4.  选择**Internet 协议版本 4 (TCP/IPv4)**，然后单击**属性**。  
  
5.  在**备用 DNS 服务器**框中，添加客户网络管理员提供的 IP 地址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
