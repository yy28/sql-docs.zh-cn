---
title: 教程：Linux 上的 SQL Server 使用 AD 身份验证
titleSuffix: SQL Server
description: 本教程提供了 Linux 上的 SQL Server 的 AD 身份验证的配置步骤。
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027327"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教程：Linux 上的 SQL Server 使用 Active Directory 身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持 Active Directory (AD) 身份验证，也称为集成身份验证的 linux 操作系统上。 有关概述，请参阅[Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-auth-overview.md)。

本教程包括以下任务：

> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的主机
> * 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并设置 SPN
> * 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab
> * 保护 keytab 文件
> * SQL Server 配置为使用 keytab 文件进行 Kerberos 身份验证
> * 在 TRANSACT-SQL 中创建基于 AD 的登录名
> * 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

## <a name="prerequisites"></a>先决条件

配置 AD 身份验证之前，需要：

* 设置你的网络上的 AD 域控制器 (Windows)  
* 安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的主机

您必须加入 Active Directory 域控制器与在 SQL Server Linux 主机。 有关如何加入 active directory 域的信息，请参阅[联接到 Active Directory 域 Linux 主机上的 SQL Server](sql-server-linux-active-directory-join-domain.md)。

## <a id="createuser"></a> 为创建 AD 用户 （或 MSA）[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并设置 SPN

> [!NOTE]
> 以下步骤使用你[完全限定的域名](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果您是在**Azure**，您必须 **[创建一个](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 在继续操作之前。

1. 在您的域控制器上运行[New ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令来创建一个新的 AD 用户使用永不过期的密码。 下面的示例的帐户名称`mssql`，但帐户名称可以是您喜欢的任何。 系统将提示您输入帐户的新密码。

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 这样，SQL Server 凭据并不与其他服务使用同一帐户共享是有专门的广告帐户为 SQL Server 安全最佳做法。 但是，如果您知道该帐户的密码 （需要在下一步中生成的 keytab 文件） （可选） 可以重用现有的 AD 帐户。

2. 设置此帐户使用的 ServicePrincipalName (SPN) **setspn.exe**工具。 SPN 必须完全按照下面的示例中指定的方式进行格式化。 您可以找到的完全限定的域名[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过运行主机`hostname --all-fqdns`上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机。 TCP 端口应为 1433年，除非已配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]若要使用不同的端口号。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果收到错误， `Insufficient access rights`，请与您的域管理员具有足够的权限来对此帐户设置 SPN。
   >
   > 如果在将来更改 TCP 端口，则必须运行**setspn**命令再次使用新的端口号。 您还需要在下一节中的步骤添加 SQL Server 服务 keytab 新 SPN。

有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab

有两种不同的方式来配置 SQL Server 服务 keytab 文件。 第一个选项是 keytab 配置中使用计算机帐户 (UPN)，而第二个选项使用托管服务帐户 (MSA)。 这两种机制可以同样正常运行，并且可以选择最适合您的环境的方法。

在这两种情况下，在前面步骤中创建的 SPN 是必需的并在 keytab 中必须注册 SPN。

若要配置 SQL Server 服务 keytab 文件：

1. 配置[SPN keytab 条目](#spn)下一节中。

1. 接着可以[添加 UPN](#upn) （选项 1） 或[MSA](#msa) keytab 文件在其各自的节中的步骤中的 （选项 2） 条目。

> [!IMPORTANT]
> 如果 UPN/MSA 的密码已更改，或更改了的 Spn 分配给该帐户的密码，则必须使用新密码和密钥版本数量 (KVNO) 更新 keytab。 某些服务可能还会自动轮换密码。 查看帐户相关的任何密码轮换策略，它们符合计划的维护活动，以避免意外停机时间。

### <a id="spn"></a> SPN keytab 条目

1. 检查上一步中创建的 AD 帐户密钥版本数量 (KVNO)。 它通常为 2，但它可能是另一个整数，如果多次更改该帐户的密码。 SQL Server 主机上，运行以下命令：

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > Spn 可能需要几分钟时间才能传播到你的域，尤其是域较大。 如果收到错误， `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`，请等待几分钟然后重试。  

1. 启动**ktutil**:

   ```bash
   sudo ktutil
   ```

1. 为每个 SPN，使用以下命令添加 keytab 条目：

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Keytab 写入文件，然后退出 ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > **Ktutil**工具不会验证密码，因此请确保在出现提示时输入正确。

### <a id="upn"></a> 选项 1:使用 UPN 配置 keytab

将计算机帐户添加到与你 keytab **ktutil**。 （也称为 UPN） 的计算机帐户是否处在 **/etc/krb5.keytab**形式`<hostname>$@<realm.com>`(例如， `sqlhost$@CONTOSO.COM`)。 复制从这些条目 **/etc/krb5.keytab**到**mssql.keytab**。

1. 启动**ktuil**使用以下命令：

   ```bash
   sudo ktutil
   ```

1. 使用**rkt**命令读取中的项的所有 **/etc/krb5.keytab**。

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 接下来，列出的条目。

   ```bash
   list
   ```

1. 删除由其槽编号不是 UPN 的所有条目。 通过重复以下命令来执行这一次执行一个操作：

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 当项被删除，如槽 1 中上, 一个好接替它的所有值滑。 这表示插槽 2 中的项移至插槽 1 时删除在槽 1 的项。

1. 列出出条目再次之前保留仅 UPN 条目。

   ```bash
   list
   ```

1. 当保留仅 UPN 条目时，将这些值与**mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. 退出**ktutil**。

   ```bash
   quit
   ```

### <a id="msa"></a> 选项 2:使用 MSA 配置 keytab

MSA 选项时，必须创建 SQL Server 的 Kerberos keytab。 它应包含的所有[第一步中注册的 Spn](#spn)和 Spn 注册到 msa 凭据。 

1. SPN keytab 条目被创建后，从已加入域的 Linux 计算机上运行以下命令：

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   此步骤中显示为用户帐户分配 SPN 所有权 KVNO。 若要运行此步骤，为 SPN 必须具有已分配给 MSA 帐户在其创建期间。 如果 SPN 不分配给 MSA，显示 KVNO 将是当前 SPN 所有者帐户，并且是用于配置不正确的。  

1. 启动**ktutil**:

   ```bash
   sudo ktutil
   ```

1. 添加以下两个命令使用 MSA:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Keytab 写入文件，然后退出 ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. 使用 MSA 方法时，需要使用设置的配置选项**mssql conf**指定 MSA 时访问 keytab 文件要使用的工具。 确保在下面的值 **/var/opt/mssql/mssql.conf**。

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > 仅包括 MSA 名称而不是域 \ 帐户名称。

## <a id="securekeytab"></a> 保护 keytab 文件

此 keytab 文件访问权的任何人都可以模拟域上的 SQL Server，因此请确保你到文件限制访问，以便仅 mssql 帐户具有读取权限：

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> SQL Server 配置为使用 keytab 文件进行 Kerberos 身份验证

使用以下步骤配置 SQL Server 以开始使用 keytab 文件进行 Kerberos 身份验证。

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

（可选） 禁用 UDP 连接到域控制器，以提高性能。 在许多情况下，UDP 连接总是出现故障时连接到域控制器，因此你可以设置配置选项 **/etc/krb5.conf**要跳过 UDP 调用。 编辑 **/etc/krb5.conf**并设置以下选项：

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

此时，已准备好，如下所示在 SQL Server 中使用基于 AD 的登录名。

## <a id="createsqllogins"></a> 在 TRANSACT-SQL 中创建基于 AD 的登录名

1. 连接到 SQL Server 并创建新的、 基于 AD 的登录名：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 验证登录名现在列在[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系统目录视图：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 连接到 SQL Server 使用 AD 身份验证

登录到客户端计算机使用您的域凭据。 现在你可以连接到 SQL Server 而不使用 AD 身份验证密码需重新输入。 如果您创建了一个 AD 组的登录名，任何 AD 用户是该组的成员可以以相同的方式连接。

客户端以使用 AD 身份验证的特定连接字符串参数取决于你正在使用哪个驱动程序。 请考虑以下各节中的示例。

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>已加入域的 Linux 客户端上的 sqlcmd

登录到已加入域的 Linux 客户端使用**ssh**和您的域凭据：

```bash
ssh -l user@contoso.com client.contoso.com
```

请确保已安装[mssql 工具](sql-server-linux-setup-tools.md)包，然后使用连接**sqlcmd**无需指定任何凭据：

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>已加入域的 Windows 客户端上的 SSMS

登录到已加入域的 Windows 客户端使用你的域凭据。 请确保已安装 SQL Server Management Studio，然后连接到 SQL Server 实例 (例如， `mssql-host.contoso.com`) 通过指定**Windows 身份验证**中**连接到服务器**对话框。

### <a name="ad-authentication-using-other-client-drivers"></a>使用其他客户端驱动程序的 AD 身份验证

下表介绍了其他客户端驱动程序的建议：

| 客户端驱动程序 | 建议 |
|---|---|
| **JDBC** | 使用 Kerberos 集成身份验证连接 SQL Server。 |
| **ODBC** | 使用集成身份验证。 |
| **ADO.NET** | 连接字符串语法。 |

## <a id="additionalconfig"></a> 其他配置选项

如果你使用第三方实用程序，如[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)将 AD 到 Linux 主机加入域，并且你想要强制使用 openldap 中的 SQL server库直接，你可以配置**disablesssd**选项与**mssql conf** ，如下所示：

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> 如有实用程序**realmd**这设置 SSSD，而其他工具如 PBI、 VAS 和 Centrify 不安装 SSSD。 如果加入 AD 域使用该实用工具不设置 SSSD，建议配置**disablesssd**选项设为`true`。 虽然它不需要为 SQL Server 将尝试使用 SSSD ad 再回退到 openldap 机制，则会更高的性能配置它，使 SQL Server 进行直接跳过 SSSD 机制 openldap 调用。

如果你的域控制器支持 LDAPS，则可以强制所有从 SQL Server 到域控制器无法通过 LDAPS 连接。 若要检查您的客户端可以通过 ldaps，运行以下 bash 命令，与域控制器`ldapsearch -H ldaps://contoso.com:3269`。 若要设置 SQL Server 仅使用 LDAPS，运行以下命令：

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

这将通过 SSSD 使用 LDAPS，如果在加入 AD 域主机已通过 SSSD 包和**disablesssd**未设置为 true。 如果**disablesssd**设置为 true 连同**forcesecureldap**设置为 true，则它将通过 SQL Server 发出的 openldap 库调用使用 LDAPS 协议。

### <a name="post-sql-server-2017-cu14"></a>发布 SQL Server 2017 CU14

从 SQL Server 2017 CU14，开始，如果 SQL Server 已加入 AD 域控制器使用第三方提供程序和配置要用于常规 AD 查找 openldap 调用通过设置**disablesssd**到为 true，还可以使用**enablekdcfromkrb5**选项来强制 SQL Server 以使用 krb5 库进行 KDC 查找而不是 KDC 服务器的反向 DNS 查找。

这可能是你想要手动配置 SQL Server 尝试与通信的域控制器的方案非常有用。 并且通过使用中的 KDC 列表使用 openldap 库机制**krb5.conf**。

首先，设置**disablessd**并**enablekdcfromkrb5conf**为 true，然后重新启动 SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

然后配置中的 KDC 列表 **/etc/krb5.conf** ，如下所示：

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 尽管不推荐这样做，则可以使用实用程序，如**realmd**，，配置时加入到域，Linux 主机时将其设置 SSSD **disablesssd**为 true，以便使用 SQL Serveropenldap 调用改为 SSSD Active directory 相关的调用。

## <a name="next-steps"></a>后续步骤

在本教程中，我们介绍了如何设置与 Linux 上的 SQL Server 的 Active Directory 身份验证。 你将了解到：
> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的主机
> * 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并设置 SPN
> * 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab
> * 在 TRANSACT-SQL 中创建基于 AD 的登录名
> * 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

接下来，浏览其他安全方案适用于 SQL Server Linux 上。

> [!div class="nextstepaction"]
> [加密连接到 Linux 上的 SQL Server](sql-server-linux-encrypted-connections.md)
