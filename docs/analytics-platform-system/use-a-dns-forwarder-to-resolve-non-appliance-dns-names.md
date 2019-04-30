---
title: 在分析平台系统中使用 DNS 转发器 |Microsoft Docs"
description: 使用 DNS 转发器解析非设备 DNS 名称分析平台系统中。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6ce978d7b05382b1a02018f3d5022b0f8bfaf585
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243793"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>使用 DNS 转发器分析平台系统中解析非设备 DNS 名称
可以在 Active Directory 域服务节点上配置 DNS 转发器 (**_装置\_域_-AD01**并**_设备\_域_-AD02**) 的分析平台系统的设备，可允许脚本和访问外部服务器的软件应用程序。  
  
## <a name="ResolveDNS"></a>使用 DNS 转发器  
分析平台系统设备配置为阻止不在设备中的服务器的 DNS 名称解析。 某些进程，如 Windows Software Update Services (WSUS)，将需要访问设备外的服务器。 若要支持这种使用方案分析平台系统 DNS 可以被配置为支持分析平台系统主机和虚拟机 (Vm) 以使用外部 DNS 服务器解析外部设备的名称将允许的外部名称转发器。 不支持自定义配置的 DNS 后缀，这意味着你必须使用完全限定的域名解析非设备服务器名称。  
  
**若要使用 DNS GUI 创建 DNS 转发器**  
  
1.  登录到**_装置\_域_-AD01**节点。  
  
2.  打开 DNS 管理器 (**dnsmgmt.msc**)。  
  
3.  右键单击服务器的名称，然后单击**属性**。  
  
4.  在**高级**选项卡上，取消选中**禁用递归 （也禁用转发器）** 选项，并单击**应用**。)  
  
5.  单击**转发器**选项卡，然后单击**编辑**。  
  
6.  输入将提供的名称解析的外部 DNS 服务器的 IP 地址。 Vm 和设备中的服务器 （主机） 将连接到外部服务器使用完全限定的域名。  
  
7.  上重复步骤 1-6 **_装置\_域_-AD02**节点  
  
**若要使用 Windows PowerShell 创建 DNS 转发器**  
  
1.  登录到**_装置\_域_-AD01**节点。  
  
2.  运行中的以下 Windows PowerShell 脚本**_装置\_域_-AD01**节点。 在运行之前的 Windows PowerShell 脚本，替换非设备 DNS 服务器的 IP 地址的 IP 地址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在执行同一命令**_装置\_域_-AD02**节点。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>对于 WSUS，请配置 DNS 解析  
SQL Server PDW 2012 提供集成的服务和修补功能。 SQL Server PDW 使用 Microsoft Update 和其他 Microsoft 服务技术。 若要启用该设备必须能够连接到公司的 WSUS 存储库或 Microsoft 公共 WSUS 存储库的更新。  
  
对于选择配置的设备，可查看 Microsoft 公共 WSUS 存储库上的更新的客户，按照以下说明在设备上设置正确的配置详细信息。  
  
> [!NOTE]  
> 客户的网络管理员必须为可解析名称在公司 DNS 服务器提供的 IP 地址**Microsoft.com**。  
  
1.  使用远程桌面，登录到 VMM VM (<fabric domain>VMM) 使用的 fabric 域管理员帐户。  
  
2.  打开控制面板中，单击**网络和 Internet**，然后单击**网络和共享中心**。  
  
3.  在连接列表中，单击**VMSEthernet**，然后单击**属性**。  
  
4.  选择**Internet 协议版本 4 (TCP/IPv4)**，然后单击**属性**。  
  
5.  在中**备用 DNS 服务器**框中，添加客户的网络管理员提供的 IP 地址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
