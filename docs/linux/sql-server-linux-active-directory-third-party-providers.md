---
title: Linux 上的 SQL Server 中使用第三方 Active Directory 提供程序 |Microsoft Docs
description: 本教程提供了与第三方提供程序的 AD 身份验证的配置步骤
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: 288f46a2084166a1b7164ff8f0c0ef82b81fb16b
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381524"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Linux 上的 SQL Server 中使用第三方 Active Directory 提供程序

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主机上使用 AD 身份验证时使用第三方 AD 提供程序，如[PowerBroker 标识服务 (PBI)](https://www.beyondtrust.com/)， [Vintela 身份验证服务 (VAS)](https://www.oneidentity.com/products/authentication-services/)，并[Centrify](https://www.centrify.com/)。 本指南包括步骤检查 AD 配置，并且不应以指示如何将计算机加入到域。 有关详细说明加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]承载到使用领域和 SSSD 域，请参阅[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

## <a name="prerequisites"></a>必要條件

配置 AD 身份验证之前，需要设置 AD 域控制器 (Windows) 网络并加入你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的 Linux 主机上。 可以使用[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。

> [!NOTE]
>
>本教程使用"contoso.com"和"CONTOSO.COM"作为示例域和领域名称分别。 它还使用"DC1。CONTOSO.COM"作为示例完全限定的域名的域控制器。 应将其替换为自己的值为。

## <a name="check-connection-to-domain-controller"></a>检查与域控制器的连接

检查可以联系域控制器的域的短期和完全限定名称。

   ```bash
   ping contoso

   ping contoso.com
   ```

   如果其中任何一个失败，请更新你的域搜索列表。

   - **Ubuntu**:

     编辑`/etc/network/interfaces`文件，以便你的 AD 域的域搜索列表中： 

     ```/etc/network/interfaces
     <...>
     # The primary network interface
     auto eth0
     iface eth0 inet dhcp
     dns-nameservers **<AD domain controller IP address>**
     dns-search **<AD domain name>**
     ```

     > [!NOTE]
     > 对于不同的计算机，网络接口 (eth0) 可能会有所不同。 若要确定使用哪一个，请运行 ifconfig 并复制具有一个 IP 地址和传输和接收的字节数的接口。

     编辑此文件之后，重启网络服务：

     ```bash
     sudo ifdown eth0 && sudo ifup eth0
     ```

     现在检查你`/etc/resolv.conf`文件均包含一行如下例所示：  

     ```/etc/resolv.conf
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   - **RHEL**:

     编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件 （或其他界面配置文件根据需要），以便你的 AD 域的域搜索列表中：

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     DOMAIN="contoso.com com"
     ```

     编辑此文件之后，重启网络服务：

     ```bash
     sudo systemctl restart network
     ```

     现在检查你`/etc/resolv.conf`文件均包含一行如下例所示：  

     ```/etc/resolv.conf
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   如果仍不能 ping 的域控制器，请查找完全限定的域名 (例如 DC1。CONTOSO.COM) 和域控制器的 IP 地址，并添加以下条目到 `/etc/hosts`

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

   - **SLES**:

     编辑`/etc/sysconfig/network/config`文件，以便你的 AD 域控制器 IP 将用于 DNS 查询和你的 AD 域是域搜索列表中：

     ```/etc/sysconfig/network/config
     <...>
     NETCONFIG_DNS_STATIC_SEARCHLIST=""
     NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
     ```

     编辑此文件之后，重启网络服务：
     ```bash
     sudo systemctl restart network
     ```

     现在检查你`/etc/resolv.conf`文件均包含一行如下例所示：

     ```/etc/resolv.conf
     search contoso.com com
     nameserver **<AD domain controller IP address>**
     ```

## <a name="check-reverse-dns-is-properly-configured"></a>检查正确配置反向 DNS

下面的命令应返回 （例如运行 SQL Server 的主机的完全限定的域名"SqlHost.contoso.com")。

   ```bash
   host **<IP address of SQL Server host>**
   # **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
   ```

   如果这不会返回主机的 FQDN 或 FQDN 不正确，添加的反向 DNS 条目将[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到你的 DNS 服务器在 Linux 主机上。

## <a name="check-your-krb5-configuration-is-correct"></a>检查 KRB5 配置正确

检查你`/etc/krb5.conf`正确配置。 对于大多数第三方 AD 提供程序，这是自动完成。 但是，检查`/etc/krb5.conf`为以下值，以防止任何将来的问题：

   ```/etc/krb5.conf
   [libdefaults]
   default_realm = CONTOSO.COM

   [realms]
   CONTOSO.COM = {
   }

   [domain_realm]
   contoso.com = CONTOSO.COM
   .contoso.com = CONTOSO.COM
   ```

## <a name="next-steps"></a>后续步骤

在本文中，我们介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主机上使用 AD 身份验证时使用第三方 AD 提供程序。 若要完成的配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上以支持 AD 帐户，请遵循的说明[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

> [!div class="nextstepaction"]
> [Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> 可以跳过中的"联接的 SQL Server 主机到 AD 域"一节[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)为只具有在本教程中完成的。