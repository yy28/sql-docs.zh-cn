---
title: "在 Linux 上的 SQL 服务器的 active Directory 身份验证 |Microsoft 文档"
description: "在 Linux 上的 SQL Server 的 AAD 身份验证的配置步骤"
author: tmullaney
ms.date: 08/23/2017
ms.author: rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4358a69b354964841e5e1f58a9a0d046afd85052
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="active-directory-authentication-with-sql-server-on-linux"></a>在 Linux 上的 SQL 服务器的 active Directory 身份验证

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文档介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持 Active Directory (AD) 身份验证，也称为集成身份验证的 linux 操作系统上。 AD 身份验证使在 Windows 或 Linux 进行身份验证到已加入域的客户端[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用其域凭据和 Kerberos 协议。

AD 身份验证通过具有以下优点[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证：

* 用户进行身份验证通过单一登录，而不会提示输入密码。   
* 通过创建的 AD 组的登录名，你可以管理访问和权限中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 组成员身份。  
* 每个用户组织，具有单个标识，因此不必能够跟踪其[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登录名对应于哪些用户。   
* AD，可在你的组织之间强制实施了集中式的密码策略。   

## <a name="prerequisites"></a>必要條件

在配置 AD 身份验证之前，您需要：

* 设置你的网络上的 AD 域控制器 (Windows)  
* 安装[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

> [!IMPORTANT]
> 在此期间，数据库镜像终结点支持的唯一身份验证方法是证书。 将在未来版本中启用 WINDOWS 身份验证方法。

## <a name="step-1-join-includessnoversionincludesssnoversion-mdmd-host-to-ad-domain"></a>步骤 1： 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机到 AD 域

存在大量的工具以帮助您加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到你的 AD 域的主机。 本演练使用 **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)**，流行的开放源包。 如果你尚未安装的 realmd 和 Kerberos 客户端包上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用你的 Linux 分发的包管理器的主机：

```bash
# RHEL
sudo yum install realmd krb5-workstation

# SUSE
sudo zypper install realmd krb5-client

# Ubuntu
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

如果 Kerberos 客户端程序包安装将提示您输入的领域名称，请以大写形式输入你的域名。

> [!NOTE]
> 本演练使用"contoso.com"和"CONTOSO.COM"作为示例的域和领域名称，分别。 你应将其与你自己的值。 这些命令是区分大小写，因此请确保你使用大写只要在本演练中使用。

运行以下命令以确认[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机配置为使用的 AD 域控制器作为 DNS 名称服务器：

```bash
sudo realm discover contoso.com -v
```

如果找不到你的域，需要配置你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机机以用作 DNS 名称服务器的 AD 域控制器的 IP 地址。 若要执行此操作的特定步骤取决于你的网络设备配置、 域配置和 Linux 分发。 以下是一些示例方法。

### <a name="example-dns-configuration-ubuntu"></a>示例 DNS 配置： Ubuntu

编辑`/etc/network/interfaces`文件，以便你的 AD 域控制器的 IP 地址被列为 dns 名称服务器。 例如： 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 网络接口 (eth0) 可能会与不同机不同。 若要了解你使用哪一个，运行 ifconfig，并复制有一个 IP 地址和传输和接收的字节的接口。

编辑此文件之后, 重新启动网络服务：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

现在请检查你`/etc/resolv.conf`文件包含如下所示的行：  

```Code
nameserver **<AD domain controller IP address>**
```

### <a name="example-dns-configuration-rhel"></a>示例 DNS 配置： RHEL

编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件 （或文件根据其他接口配置），以便你的 AD 域控制器的 IP 地址被列为 DNS 服务器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

编辑此文件之后, 重新启动网络服务：

```bash
sudo systemctl restart network
```

现在请检查你`/etc/resolv.conf`文件包含如下所示的行：  

```Code
nameserver **<AD domain controller IP address>**
```

### <a name="join-the-domain"></a>加入域

一旦你已确认您的 DNS 配置正确，请通过运行以下命令以加入域。 你将需要使用在 AD 将新计算机加入到域中具有足够的权限的 AD 帐户进行身份验证。

具体而言，此命令将在 AD 中创建新的计算机帐户、 创建`/etc/krb5.keytab`承载 keytab 文件和配置中的域`/etc/sssd/sssd.conf`:

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
 * Successfully enrolled machine in realm
```

> [!NOTE]
> 如果你看到的错误，"未安装必需的包，"，然后应安装这些包使用你的 Linux 分发的包管理器在运行前`realm join`试命令。
>
> 如果收到错误，"权限不足，无法加入域，"你将需要与域管理员检查有足够的权限将 Linux 计算机加入到你的域。

验证，可以现在从域中，收集有关用户的信息以及您可以获取作为该用户的 Kerberos 票证。

We will use **id**, **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)** and **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** commands for this.

```bash
id user@contoso.com
uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

kinit user@CONTOSO.COM
Password for user@CONTOSO.COM:

klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: user@CONTOSO.COM
<...>
```

> [!NOTE]
> 如果`id user@contoso.com`返回时，"没有此类用户，"请确保通过运行命令已成功启动 SSSD 服务`sudo systemctl status sssd`。 如果服务正在运行，并且你仍看到"这样的用户"错误，请尝试启用的 SSSD 详细日志记录。 有关详细信息，请参阅的 Red Hat 文档[疑难解答 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)。
>
> 如果`kinit user@CONTOSO.COM`返回时，"KDC 答复不匹配期望获取初始凭据时"请确保以大写形式指定领域。

有关详细信息，请参阅的 Red Hat 文档[发现和加入标识域](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)。 

## <a name="step-2-create-ad-user-for-includessnoversionincludesssnoversion-mdmd-and-set-spn"></a>步骤 2： 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和设置 SPN

> [!NOTE]
> 在下一步的步骤中，我们将使用你[完全限定的域名称](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果你在**Azure**，你将需要**[创建一个](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)**在继续操作之前。

在你的域控制器上运行[New-aduser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令以创建新的 AD 用户使用永不过期的密码。 本示例将命名的帐户"mssql，"但帐户名称可以是您喜欢的任何。 系统将提示您输入的帐户的新密码：

```PowerShell
Import-Module ActiveDirectory

New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
```

> [!NOTE]
> 它是安全的最佳做法，对于 SQL Server，有一个专用的 AD 帐户，以便不会与其他服务使用同一个帐户共享 SQL Server 的凭据。 但是，你可以重用现有的 AD 帐户如果您愿意，如果你知道该帐户的密码 （需要在下一步中生成 keytab 文件）。

现在，设置此帐户使用 ServicePrincipalName (SPN)`setspn.exe`工具。 SPN 必须格式化为完全按照下面的示例中指定的方式： 你可以找到的完全限定的域名称[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过运行的主机`hostname --all-fqdns`上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机和 TCP 端口应为 1433年，除非已配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]若要使用不同的端口号。

```PowerShell
setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
```

> [!NOTE]
> 如果收到错误，"没有足够的访问权限，"然后你需要检查与域管理员您具有足够的权限，此帐户上设置 SPN。
>
> 如果在将来更改的 TCP 端口，你将需要再次运行 setspn 命令，使用新的端口号。 你还需要将新的 SPN 添加到 SQL Server 服务 keytab，按照下一节中的步骤。

有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a name="step-3-configure-includessnoversionincludesssnoversion-mdmd-service-keytab"></a>步骤 3： 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab

首先，在上一步中创建 AD 帐户中查看此密钥版本编号 (kvno)。 通常，它将是 2，但它可能是另一个整数，如果您多次更改帐户的密码。 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机计算机，运行以下命令：

```bash
kinit user@CONTOSO.COM

kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
```

现在创建上一步中创建的 AD 用户的 keytab 文件。 为此，我们将使用 **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**。 出现提示时，输入该 AD 帐户的密码。

```bash
sudo ktutil

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

quit
```

> [!NOTE]
> 不，ktutil 工具不验证的密码，因此请确保正确输入。

任何人有权访问此`keytab`文件可以模拟[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在域中，因此请确保你限制对此类的文件访问，它仅`mssql`帐户具有读取权限：

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

接下来，配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才能使用此`keytab`Kerberos 身份验证的文件：

```bash
sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

## <a name="step-4-create-ad-based-logins-in-transact-sql"></a>步骤 4： 在 TRANSACT-SQL 中创建基于 AD 的登录名

连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并创建新的、 基于 AD 的登录名：

```sql
CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
```

验证登录名现在列在[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系统目录视图：

```sql
SELECT name FROM sys.server_principals;
```

## <a name="step-5-connect-to-includessnoversionincludesssnoversion-mdmd-using-ad-authentication"></a>步骤 5： 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

登录到客户端计算机使用域凭据。 现在你可以连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无需你的密码，重新输入通过使用 AD 身份验证。 如果你创建的 AD 组的登录名，只要 AD 用户是该组的成员可以连接的方式相同。

客户端使用 AD 身份验证的特定连接字符串参数取决于你正在使用哪个驱动程序。 下面是几个示例。

## <a name="examples"></a>示例

### <a name="example-1-sqlcmd-on-a-domain-joined-linux-client"></a>示例 1:`sqlcmd`已加入域的 Linux 客户端上

登录到已加入域的 Linux 客户端使用`ssh`和你的域凭据：

```bash
ssh -l user@contoso.com client.contoso.com
```

请确保已安装[mssql 工具](sql-server-linux-setup-tools.md)包，然后使用连接`sqlcmd`没有指定任何凭据：

```bash
sqlcmd -S mssql.contoso.com
```

### <a name="example-2-ssms-on-a-domain-joined-windows-client"></a>示例 2： 已加入域的 Windows 客户端上的 SSMS

登录到已加入域的 Windows 客户端使用域凭据。 请确保[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]安装，然后连接到你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过指定实例**Windows 身份验证**中**连接到服务器**对话框。

### <a name="ad-authentication-using-other-client-drivers"></a>使用其他客户端驱动程序的 AD 身份验证

* JDBC:[使用 Kerberos 集成身份验证连接 SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
* ODBC:[使用集成身份验证](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
* ADO.NET:[连接字符串语法](https://docs.microsoft.com/dotnet/framework/data/adonet/connection-string-syntax)

