---
title: Linux 上的 SQL Server 中使用第三方 Active Directory 提供程序
titleSuffix: SQL Server
description: 本教程提供了 Active Directory 身份验证与第三方提供商的配置步骤
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: de28696efd16a2be61864a810b3fd713b1066258
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160565"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Linux 上的 SQL Server 中使用第三方 Active Directory 提供程序

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]具有 Active Directory 身份验证时使用第三方 Active Directory 提供程序的 Linux 主机计算机上。 示例包括[PowerBroker 标识服务 (PBI)](https://www.beyondtrust.com/)，[一个标识](https://www.oneidentity.com/products/authentication-services/)，并[Centrify](https://www.centrify.com/)。 本指南包括检查 Active Directory 配置的步骤。 它不具有应指示如何将计算机加入到域。 有关详细说明加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过使用 realmd 和 SSSD 托管到域，请参阅[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

## <a name="prerequisites"></a>先决条件

配置 Active Directory 身份验证之前，需要设置 Active Directory 域控制器，Windows，在网络上。 然后，加入你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 Active Directory 域的 Linux 主机上。 可以使用[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。

> [!NOTE]
>
>本教程使用**`contoso.com`** 并**`CONTOSO.COM`** 示例域和领域名称，作为分别。 它还使用**`DC1.CONTOSO.COM`** 如示例中完全限定的域名的域控制器。 这些名称应替换你自己的值。

## <a name="check-the-connection-to-a-domain-controller"></a>检查与域控制器的连接

检查可以联系域控制器，具有域的简短和完全限定名称：

```bash
ping contoso

ping contoso.com
```

如果任一这些名称检查失败，则更新域搜索列表：

- **Ubuntu**

  编辑`/etc/network/interfaces`文件，以便你的 Active Directory 域的域搜索列表中： 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > 网络接口**eth0**，对于不同的计算机可能会有所不同。 若要确定使用哪一个，请运行**ifconfig**。 然后，复制具有一个 IP 地址和传输和接收的字节数的接口。

  编辑此文件之后，重启网络服务：

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  现在检查你`/etc/resolv.conf`文件均包含一行如下例所示：  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件，以便你的 Active Directory 域的域搜索列表中。 或编辑相应的另一个接口配置文件：

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

  如果仍不能 ping 的域控制器，请查找完全限定的域名和域控制器的 IP 地址。 示例中的域名称是`DC1.CONTOSO.COM`。 添加以下条目到`/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  编辑`/etc/sysconfig/network/config`文件，以便你的 Active Directory 域控制器 IP 用于 DNS 查询，且你的 Active Directory 域是域搜索列表中：

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>检查已正确配置反向 DNS

下面的命令应返回运行 SQL Server 的主机的完全限定的域名。 例如， **`SqlHost.contoso.com`**。

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

如果此命令不会返回主机的 FQDN，或者如果 FQDN 不正确，添加反向 DNS 条目，则为[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到你的 DNS 服务器在 Linux 主机上。

## <a name="check-that-your-krb5-configuration-is-correct"></a>检查 KRB5 配置正确

检查你`/etc/krb5.conf`正确配置。 对于大多数第三方 Active Directory 提供程序，此配置会自动完成。 但是，检查`/etc/krb5.conf`为以下值，以防止任何将来的问题：

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

这篇文章介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]具有 Active Directory 身份验证时使用第三方 Active Directory 提供程序的 Linux 主机计算机上。 若要完成的配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上以支持 Active Directory 帐户，请遵循的说明[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

> [!div class="nextstepaction"]
> [Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> 可以跳过**Active Directory 域加入 SQL Server 宿主**主题中[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)如你刚才执行的在本教程中。
