---
title: 使用 DNS 转发器
description: 使用 DNS 转发器解析分析平台系统中的非设备 DNS 名称。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399436"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>使用 DNS 转发器解析分析平台系统中的非设备 DNS 名称
可以在分析平台系统设备的 Active Directory 域服务节点（**_设备\_域_-AD01**和**_设备\_域_-AD02**）上配置 DNS 转发器，以允许脚本和软件应用程序访问外部服务器。  
  
## <a name="ResolveDNS"></a>使用 DNS 转发器  
分析平台系统设备配置为阻止解析不在设备中的服务器的 DNS 名称。 某些进程（如 Windows 软件更新服务（WSUS））将需要访问设备之外的服务器。 若要支持此使用方案，可将分析平台系统 DNS 配置为支持外部名称转发器，这将允许分析平台系统主机和虚拟机（Vm）使用外部 DNS 服务器来解析设备之外的名称。 不支持 DNS 后缀的自定义配置，这意味着必须使用完全限定的域名来解析非设备服务器名称。  
  
**使用 DNS GUI 创建 DNS 转发器**  
  
1.  登录到** _\_设备 "域_-AD01** " 节点。  
  
2.  打开 DNS 管理器（**dnsmgmt.msc**）。  
  
3.  右键单击服务器的名称，然后单击 "**属性**"。  
  
4.  在 "**高级**" 选项卡上，取消选中 "**禁用递归（也禁用转发器）** " 选项，然后单击 "**应用**"。）  
  
5.  单击 "**转发器**" 选项卡，然后单击 "**编辑**"。  
  
6.  输入将提供名称解析的外部 DNS 服务器的 IP 地址。 设备中的 Vm 和服务器（主机）将使用完全限定的域名连接到外部服务器。  
  
7.  在**_设备\__** 上重复步骤 1-6-AD02 节点  
  
**使用 Windows PowerShell 创建 DNS 转发器的方法**  
  
1.  登录到** _\_设备 "域_-AD01**" 节点。  
  
2.  从** _\_设备的域_-AD01**节点运行以下 Windows PowerShell 脚本。 在运行 Windows PowerShell 脚本之前，请将 IP 地址替换为非设备 DNS 服务器的 IP 地址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在**_设备\__** 上执行相同的命令-AD02 节点。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>为 WSUS 配置 DNS 解析  
SQL Server PDW 2012 提供集成的服务和修补功能。 SQL Server PDW 使用 Microsoft 更新和其他 Microsoft 维护技术。 若要启用更新，设备必须能够连接到公司 WSUS 存储库或 Microsoft 公共 WSUS 存储库。  
  
对于选择将设备配置为在 Microsoft 公共 WSUS 存储库中查找更新的客户，以下说明在设备上设置了正确的配置详细信息。  
  
> [!NOTE]  
> 客户网络管理员必须提供可解析**Microsoft.com**中的名称的企业 DNS 服务器的 IP 地址。  
  
1.  使用远程桌面，使用 fabric 域管理员帐户登录<fabric domain>到 vmm VM （-vmm）。  
  
2.  打开 "控制面板"，单击 "**网络和 Internet**"，然后单击 "**网络和共享中心**"。  
  
3.  在 "连接" 列表中，单击 " **VMSEthernet**"，然后单击 "**属性**"。  
  
4.  选择“Internet 协议版本 4 (TCP/IPv4)”****，然后单击“属性”****。  
  
5.  在 "**备用 DNS 服务器**" 框中，添加客户网络管理员提供的 IP 地址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
