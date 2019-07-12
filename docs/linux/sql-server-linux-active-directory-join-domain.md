---
title: 将 SQL 服务器加入到 Active Directory 的 Linux 上
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
manager: jroth
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4cee4ca0edcc5a49a34b6c352ae0121bed3b40ca
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834443"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>加入到 Active Directory 域 Linux 主机上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供有关如何将 SQL Server Linux 主机加入到 Active Directory (AD) 域的常规指南。 有两种方法： 使用内置的 SSSD 包或使用第三方 Active Directory 提供程序。 第三方域联接产品的示例包括[PowerBroker 标识服务 (PBI)](https://www.beyondtrust.com/)，[一个标识](https://www.oneidentity.com/products/authentication-services/)，并[Centrify](https://www.centrify.com/)。 本指南包括检查 Active Directory 配置的步骤。 但是，它不用于提供有关如何将计算机加入到域时使用第三方实用程序的说明。

## <a name="prerequisites"></a>先决条件

配置 Active Directory 身份验证之前，需要设置 Active Directory 域控制器，Windows，在网络上。 然后将您的 SQL Server 加入到 Active Directory 域的 Linux 主机上。

> [!IMPORTANT]
> 本文中所述的示例步骤是仅供指导。 实际步骤可能略有不同具体取决于整体环境的配置方式在环境中。 咨询您的环境特定的配置、 自定义和任何所需故障排除的系统和域管理员。

## <a name="check-the-connection-to-a-domain-controller"></a>检查与域控制器的连接

检查可以联系域控制器，具有域的简短和完全限定名称：

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> 本教程使用**contoso.com**并**CONTOSO.COM**示例域和领域名称，作为分别。 它还使用**DC1。CONTOSO.COM**如示例中完全限定的域名的域控制器。 必须使用你自己的值替换这些名称。

如果任一这些名称检查失败，则更新域搜索列表。 以下各节分别提供有关 Ubuntu、 Red Hat Enterprise Linux (RHEL) 和 SUSE Linux Enterprise Server (SLES) 的说明。

### <a name="ubuntu"></a>Ubuntu

1. 编辑 **/etc/network/interfaces**文件，以便你的 Active Directory 域的域搜索列表中：

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > 网络接口的`eth0`，对于不同的计算机可能会有所不同。 若要确定使用哪一个，请运行**ifconfig**。 然后，复制具有一个 IP 地址和传输和接收的字节数的接口。

1. 编辑此文件之后，重启网络服务：

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 接下来，检查你 **/etc/resolv.conf**文件均包含一行如下例所示：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. 编辑 **/etc/sysconfig/network-scripts/ifcfg-eth0**文件，以便你的 Active Directory 域的域搜索列表中。 或编辑相应的另一个接口配置文件：

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. 编辑此文件之后，重启网络服务：

   ```bash
   sudo systemctl restart network
   ```

1. 现在检查你 **/etc/resolv.conf**文件均包含一行如下例所示：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. 如果仍不能 ping 的域控制器，请查找完全限定的域名和域控制器的 IP 地址。 示例中的域名称是**DC1。CONTOSO.COM**。 添加到以下一项 **/主机**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. 编辑 **/etc/sysconfig/network/config**文件，以便你的 Active Directory 域控制器 IP 用于 DNS 查询，且你的 Active Directory 域是域搜索列表中：

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. 编辑此文件之后，重启网络服务：

   ```bash
   sudo systemctl restart network
   ```

1. 接下来，检查你 **/etc/resolv.conf**文件均包含一行如下例所示：

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>加入 AD 域

基本配置并与域控制器的连接进行验证后，有两个用于加入 SQL Server Linux 主机计算机与 Active Directory 域控制器选项：

- [选项 1:使用 SSSD 包](#option1)
- [选项 2:使用第三方 openldap 提供程序实用程序](#option2)

### <a id="option1"></a> 选项 1:SSSD 包用于加入 AD 域

此方法联接到 AD 域使用的 SQL Server 主机**realmd**并**sssd**包。

> [!NOTE]
> 这是加入 AD 域控制器到 Linux 主机的首选的方法。

使用以下步骤以加入到 Active Directory 域的 SQL 服务器主机：

1. 使用[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join)将主机加入 AD 域。 您必须首先安装两者**realmd**和使用 Linux 分发的包管理器在 SQL Server 主机计算机上的 Kerberos 客户端包：

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu：**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 客户端程序包安装将提示您输入的领域名称，输入你的域名以大写形式。

1. 确认您的 DNS 配置正确后，通过运行以下命令来加入域。 您必须进行身份验证使用 AD 将新计算机加入到域中有足够的特权的 AD 帐户。 此命令将在 AD 中创建新的计算机帐户、 创建 **/etc/krb5.keytab**托管 keytab 文件，配置中的域 **/etc/sssd/sssd.conf**，并更新 **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   应会看到消息， `Successfully enrolled machine in realm`。

   下表列出了一些您可能会收到错误消息和解决这些建议：

   | 错误消息 | 建议 |
   |---|---|
   | `Necessary packages are not installed` | 安装这些包再次运行领域的联接命令之前使用 Linux 分发的包管理器。 |
   | `Insufficient permissions to join the domain` | 请与域管理员具有足够的权限将 Linux 计算机加入到你的域。 |
   | `KDC reply did not match expectations` | 你可能未指定用户的正确的领域名称。 领域名称区分大小写、 通常大写，并可以标识与命令领域发现 contoso.com。 |

   SQL Server 使用 SSSD 和 NSS 用于映射到安全标识符 (Sid) 的用户帐户和组。 SSSD 必须配置并运行 SQL server 已成功创建 AD 的登录名。 **realmd**通常执行此操作会自动作为一部分的加入域，但在某些情况下，您必须单独执行此操作。

   有关详细信息，请参阅如何[手动配置 SSSD](https://access.redhat.com/articles/3023951)，并[配置 NSS 用于 SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)。

1. 验证，可以现在从域中，收集有关用户的信息，以及你可以获取作为该用户的 Kerberos 票证。 下面的示例使用**id**， [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)，并[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)此命令。

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - 如果**id user@contoso.com** 返回时， `No such user`，请确保通过运行命令已成功启动 SSSD 服务`sudo systemctl status sssd`。 如果服务正在运行并且您仍看到此错误，请尝试启用 SSSD 详细日志记录。 有关详细信息，请参阅 Red Hat 文档[故障诊断 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)。
   >
   > - 如果**kinit user@CONTOSO.COM** 返回， `KDC reply did not match expectations while getting initial credentials`，请确保以大写形式指定领域。

有关详细信息，请参阅 Red Hat 文档[发现和加入标识域](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)。

### <a id="option2"></a> 选项 2:使用第三方 openldap 提供程序实用程序

您可以使用第三方实用程序，如[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。 本文不涉及每个单独的实用程序的步骤。 首先必须使用这些实用程序向前继续操作之前将 SQL Server Linux 主机加入到域。  

SQL Server 不使用有关任何与 AD 相关的查询的第三方集成器的代码或库。 SQL Server 始终查询直接在此安装程序中使用 openldap 库调用的 AD。 第三方集成商仅用于 Linux 主机到 AD 域加入和 SQL Server 不具有任何与这些实用程序进行直接通信。

> [!IMPORTANT]
> 使用的建议，请参阅**mssql conf** `network.disablesssd`中的配置选项**其他配置选项**本文的相关部分[使用活动使用 Linux 上的 SQL Server directory 身份验证](sql-server-linux-active-directory-authentication.md#additionalconfig)。

验证你 **/etc/krb5.conf**正确配置。 对于大多数第三方 Active Directory 提供程序，此配置会自动完成。 但是，检查 **/etc/krb5.conf**为以下值，以防止任何将来的问题：

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>检查已正确配置反向 DNS

下面的命令应返回的运行 SQL Server 的主机的完全限定的域名 (FQDN)。 例如， **SqlHost.contoso.com**。

```bash
host **<IP address of SQL Server host>**
```

此命令的输出应类似于`**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`。 如果此命令不返回主机的 FQDN，或者如果 FQDN 不正确，将反向 DNS 条目添加到你的 DNS 服务器的 Linux 主机上的 SQL server。

## <a name="next-steps"></a>后续步骤

这篇文章介绍如何使用 Active Directory 身份验证的 Linux 主机上配置 SQL Server 的系统必备组件。 若要完成 Linux 支持 Active Directory 帐户上配置 SQL Server，请遵循的说明[使用 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。