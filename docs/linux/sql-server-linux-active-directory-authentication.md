---
title: 教程：为 Linux 上的 SQL Server 使用 AD 身份验证
titleSuffix: SQL Server
description: 本教程提供对 Linux 上的 SQL Server 进行 AD 身份验证的配置步骤。
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027327"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教程：对 Linux 上的 SQL Server 使用 Active Directory 身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何在 Linux 上配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以支持 Active Directory (AD) 身份验证（也称为集成身份验证）。 有关概述，请参阅 [Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-auth-overview.md)。

本教程包含以下任务：

> [!div class="checklist"]
> * 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主机加入 AD 域
> * 为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 创建 AD 用户并设置 SPN
> * 配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务 keytab
> * 保护 keytab 文件
> * 将 SQL Server 配置为使用 keytab 文件进行 Kerberos 身份验证
> * 在 Transact-SQL 中创建基于 AD 的登录名
> * 使用 AD 身份验证连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

## <a name="prerequisites"></a>必备条件

在配置 AD 身份验证前，需要：

* 在网络上设置 AD 域控制器 (Windows)  
* 安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主机加入 AD 域

必须将 SQL Server Linux 主机加入 Active Directory 域控制器。 有关如何加入 Active Directory 域的信息，请参阅[将 Linux 主机上的 SQL Server 加入 Active Directory 域](sql-server-linux-active-directory-join-domain.md)。

## <a id="createuser"></a> 为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 创建 AD 用户（或 MSA）并设置 SPN

> [!NOTE]
> 以下步骤使用[完全限定的域名](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果位于 **Azure** 中，则必须 **[创建一个](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 才能继续操作。

1. 在域控制器上，运行 [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令以创建密码永不过期的新 AD 用户。 以下示例将帐户命名为 `mssql`，但帐户名称可以是你喜欢的任何名称。 系统将提示输入帐户的新密码。

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 为 SQL Server 提供专用 AD 帐户是最佳安全做法，这样一来，SQL Server 的凭据就不会与使用同一帐户的其他服务共享。 但是，如果你知道帐户的密码（在下一步中生成 keytab 文件时需要），则可以选择重复使用现有 AD 帐户。

2. 使用 **setspn.exe** 工具为此帐户设置 ServicePrincipalName (SPN)。 必须完全按照以下示例设置 SPN 的格式。 可通过在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主机上运行 `hostname --all-fqdns` 来查找 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主机的完全限定域名。 除非已将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置为使用其他端口号，否则 TCP 端口应为 1433。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果收到错误 (`Insufficient access rights`)，请与域管理员联系，确保你有足够的权限在此帐户上设置 SPN。
   >
   > 如果以后更改 TCP 端口，则必须使用新端口号再次运行 **setspn** 命令。 还需要按照下一部分中的步骤将新的 SPN 添加到 SQL Server 服务 keytab。

有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务 keytab

可通过两种不同的方法配置 SQL Server 服务 keytab 文件。 第一种方法是使用计算机帐户 (UPN)，第二种方法是使用 keytab 配置中的托管服务帐户 (MSA)。 两种机制具有同样的功能,，你可以选择最适合你的环境的方法。

在两种情况下，都需要在前面步骤中创建的 SPN，并且必须在 keytab 中注册 SPN。

若要配置 SQL Server 服务 keytab 文件，请执行以下操作：

1. 在下一部分中配置 [SPN keytab 条目](#spn)。

1. 然后，按照其各自部分中的步骤，在 keytab 文件中[添加 UPN](#upn)（选项 1）或 [MSA](#msa)（选项 2）条目。

> [!IMPORTANT]
> 如果更改了 UPN/MSA 的密码或更改了 SPN 所分配到的帐户的密码，则必须使用新密码和密钥版本号 (KVNO) 更新 keytab。 某些服务可能还会自动轮换密码。 查看相关帐户的所有密码轮换策略，并使其与计划性维护活动保持一致，以避免产生意外停机时间。

### <a id="spn"></a> SPN keytab 条目

1. 检查上一步中创建的 AD 帐户的密钥版本号 (KVNO)。 它通常为 2，但如果多次更改帐户的密码，则它可能是其他整数。 在 SQL Server 主机上，运行以下命令：

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > SPN 可能需要几分钟才能在域中传播，特别是在域很大的情况下。 如果收到错误 (`kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`)，请等待几分钟，然后重试。  

1. 启动 **ktutil**：

   ```bash
   sudo ktutil
   ```

1. 使用以下命令为每个 SPN 添加 keytab 条目：

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. 将 keytab 写入文件，然后退出 ktutil：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > **ktutil** 工具不会验证密码，因此，请确保在出现提示时正确输入密码。

### <a id="upn"></a> 选项 1：使用 UPN 配置 keytab

使用 **ktutil** 将计算机帐户添加到 keytab。 计算机帐户（也称为 UPN）以 `<hostname>$@<realm.com>` 的形式（例如，`sqlhost$@CONTOSO.COM`）出现在 **/etc/krb5.keytab** 中。 将这些条目从 **/etc/krb5.keytab** 复制到 **mssql.keytab**。

1. 使用以下命令启动 **ktuil**：

   ```bash
   sudo ktutil
   ```

1. 使用 **rkt** 命令读取 **/etc/krb5.keytab** 中的所有条目。

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 接下来，列出条目。

   ```bash
   list
   ```

1. 按照槽号删除所有不是 UPN 的条目。 通过重复以下命令，一次对一个条目执行此操作：

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 删除条目（例如槽 1）后，所有值都会上移一位以取代其位置。 这意味着删除插槽 1 的条目时，插槽 2 中的条目会移至插槽 1。

1. 再次列出条目，直到仅剩下 UPN 条目。

   ```bash
   list
   ```

1. 当仅剩下 UPN 条目时，请将这些值追加到 **mssql.keytab**：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. 退出 **ktutil**。

   ```bash
   quit
   ```

### <a id="msa"></a> 选项 2：使用 MSA 配置 keytab

对于 MSA 选项，必须创建 SQL Server 的 Kerberos keytab。 它应包含[第一步中注册的所有 SPN](#spn) 以及 SPN 注册到的 MSA 的凭据。 

1. 创建 SPN keytab 条目后，从已加入域的 Linux 计算机运行以下命令：

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   此步骤显示分配了 SPN 所有权的用户帐户的 KVNO。 若要此步骤起作用，必须在创建 MSA 帐户时将 SPN 分配给 MSA 帐户。 如果 SPN 未分配给 MSA，则显示的 KVNO 将是当前 SPN 所有者帐户的 KVNO，并且不可用于配置。  

1. 启动 **ktutil**：

   ```bash
   sudo ktutil
   ```

1. 使用以下两个命令添加 MSA：

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. 将 keytab 写入文件，然后退出 ktutil：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. 使用 MSA 方法时，需要使用 **mssql-conf** 工具设置配置选项，以指定访问 keytab 文件时要使用的 MSA。 确保以下值位于 **/var/opt/mssql/mssql.conf** 中。

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > 仅包括 MSA 名称，而不包括域\帐户名称。

## <a id="securekeytab"></a> 保护 keytab 文件

有权访问此 keytab 文件的任何人都可以在域上模拟 SQL Server，因此，请确保限制对该文件的访问，以便只有 mssql 帐户具有读取访问权限：

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> 将 SQL Server 配置为使用 keytab 文件进行 Kerberos 身份验证

使用以下步骤配置 SQL Server，以开始使用 keytab 文件进行 Kerberos 身份验证。

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

（可选）禁用与域控制器的 UDP 连接以提高性能。 在许多情况下，UDP 连接在连接到域控制器时始终会失败，因此，可在 **/etc/krb5.conf** 中设置配置选项以跳过 UDP 调用。 编辑 **/etc/krb5.conf** 并设置以下选项：

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

此时，你已准备好在 SQL Server 中使用基于 AD 的登录名，如下所示。

## <a id="createsqllogins"></a> 在 Transact-SQL 中创建基于 AD 的登录名

1. 连接到 SQL Server 并创建基于 AD 的新登录名：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 验证登录名现在是否在 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 系统目录视图中列出：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 使用 AD 身份验证连接到 SQL Server

使用域凭据登录客户端计算机。 现在，你可以使用 AD 身份验证连接到 SQL Server，而无需重新输入密码。 如果为 AD 组创建登录名，则身为该组成员的任何 AD 用户都能够以相同方式连接。

客户端用于 AD 身份验证的特定连接字符串参数取决于你使用的驱动程序。 请考虑以下部分中的示例。

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>已加入域的 Linux 客户端上的 sqlcmd

使用 **ssh** 和域凭据登录已加入域的 Linux 客户端：

```bash
ssh -l user@contoso.com client.contoso.com
```

确保已安装 [mssql-tools](sql-server-linux-setup-tools.md) 包，然后使用 **sqlcmd** 进行连接，而无需指定任何凭据：

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>已加入域的 Windows 客户端上的 SSMS

使用域凭据登录已加入域的 Windows 客户端。 确保已安装 SQL Server Management Studio，然后通过在“连接到服务器”对话框中指定“Windows 身份验证”来连接到 SQL Server 实例（例如，`mssql-host.contoso.com`）   。

### <a name="ad-authentication-using-other-client-drivers"></a>使用其他客户端驱动程序的 AD 身份验证

下表介绍适用于其他客户端驱动程序的建议：

| 客户端驱动程序 | 建议 |
|---|---|
| **JDBC** | 使用 Kerberos 集成身份验证连接到 SQL Server。 |
| **ODBC** | 使用集成身份验证。 |
| **ADO.NET** | 连接字符串语法。 |

## <a id="additionalconfig"></a> 其他配置选项

如果使用第三方实用工具（例如 [PBIS](https://www.beyondtrust.com/)、[VAS](https://www.oneidentity.com/products/authentication-services/) 或 [Centrify](https://www.centrify.com/)）将 Linux 主机加入 AD 域，并且希望强制 SQL Server 直接使用 openldap 库，则可使用 **mssql-conf** 配置 **disablesssd** 选项，如下所示：

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> 有些实用工具（例如 **realmd**）会设置 SSSD，而其他工具（例如 PBIS、VAS 和 Centrify）则不会设置 SSSD。 如果用于加入 AD 域的实用工具不会设置 SSSD，则建议将 **disablesssd** 选项配置为 `true`。 虽然不是必需的（因为 SQL Server 会在回退到 openldap 机制前尝试将 SSSD 用于 AD），但配置该选项可提高性能，以便 SQL Server 直接绕过 SSSD 机制来进行 openldap 调用。

如果域控制器支持 LDAPS，则可以强制从 SQL Server 到域控制器的所有连接都通过 LDAPS 完成。 若要检查客户端是否可以通过 ldaps 与域控制器通信，请运行以下 bash 命令：`ldapsearch -H ldaps://contoso.com:3269`。 若要将 SQL Server 设置为仅使用 LDAPS，请运行以下命令：

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

如果在主机上通过 SSSD 包加入 AD 域，且 **disablesssd** 未设置为 true，则此设置将使用 LDAPS，而不使用 SSSD。 如果 **disablesssd** 设置为 true 且 **forcesecureldap** 也设置为 true，则它将通过 SQL Server 发出的 openldap 库调用使用 LDAPS 协议。

### <a name="post-sql-server-2017-cu14"></a>发布 SQL Server 2017 CU14

从 SQL Server 2017 CU14 开始，如果 SQL Server 使用第三方提供程序加入 AD 域控制器并配置为通过将 **disablesssd** 设置为 true 来使用 openldap 调用进行常规 AD 查找，则还可以使用 **enablekdcfromkrb5** 选项强制 SQL Server 使用 krb5 库进行 KDC 查找，而不是针对 KDC 服务器进行反向 DNS 查找。

这对于想要手动配置 SQL Server 尝试与之通信的域控制器的方案可能很有用。 通过使用 **krb5.conf** 中的 KDC 列表来使用 openldap 库机制。

首先，将 **disablessd** 和 **enablekdcfromkrb5conf** 设置为 true，然后重启 SQL Server：

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

接下来配置 **/etc/krb5.conf** 中的 KDC 列表，如下所示：

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 尽管不建议这样做，但在将 **disablesssd** 配置为 true 时，可以使用 **realmd** 等实用工具（这些实用工具在将 Linux 主机加入域时设置 SSSD），以便 SQL Server 使用 openldap 调用（而不是 SSSD）进行与 Active Directory 相关的调用。

## <a name="next-steps"></a>后续步骤

在本教程中，我们介绍了如何对 Linux 上的 SQL Server 设置 Active Directory 身份验证。 你已学习如何执行以下操作：
> [!div class="checklist"]
> * 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主机加入 AD 域
> * 为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 创建 AD 用户并设置 SPN
> * 配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务 keytab
> * 在 Transact-SQL 中创建基于 AD 的登录名
> * 使用 AD 身份验证连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

接下来，探索 Linux 上的 SQL Server 的其他安全方案。

> [!div class="nextstepaction"]
> [加密与 Linux 上的 SQL Server 的连接](sql-server-linux-encrypted-connections.md)
