---
title: Linux 上的 SQL Server 的 active Directory 身份验证教程 |Microsoft Docs
description: 本教程提供了 Linux 上的 SQL Server 的 AAD 身份验证的配置步骤。
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 7f5f7a4840582afda25551161c4702a40c4977c8
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980379"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教程： 使用 Linux 上的 SQL Server 使用 Active Directory 进行身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持 Active Directory (AD) 身份验证，也称为集成身份验证的 linux 操作系统上。 有关概述，请参阅[Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-auth-overview.md)。

本教程包括以下任务：

> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的主机
> * 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并设置 SPN
> * 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab
> * 在 TRANSACT-SQL 中创建基于 AD 的登录名
> * 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

## <a name="prerequisites"></a>必要條件

配置 AD 身份验证之前，需要：

* 设置你的网络上的 AD 域控制器 (Windows)  
* 安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 域的主机

使用以下步骤以加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机到 Active Directory 域：

1. 使用**[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** 将主机加入 AD 域。 如果你尚未安装 realmd 和 Kerberos 客户端包上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机使用 Linux 分发的包管理器：

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 客户端程序包安装将提示您输入的领域名称，输入你的域名以大写形式。

   > [!NOTE]
   > 本演练中使用"contoso.com"和"CONTOSO.COM"作为示例域和领域名称，分别。 应将其替换为自己的值为。 这些命令是区分大小写，因此请确保你使用大写它在本演练中使用的位置。

1. 配置你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机以使用 AD 域控制器的 IP 地址作为 DNS 名称服务器。 

   - **Ubuntu**:

      编辑`/etc/network/interfaces`文件，以便你的 AD 域控制器的 IP 地址被列为 dns 名称服务器。 例如： 

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

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件 （或其他界面配置文件根据需要），以便你的 AD 域控制器的 IP 地址列出 DNS 服务器：

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     编辑此文件之后，重启网络服务：

     ```bash
     sudo systemctl restart network
     ```

     现在检查你`/etc/resolv.conf`文件均包含一行如下例所示：  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. 加入域

   一旦确认您的 DNS 配置正确后，通过运行以下命令来加入域。 您必须进行身份验证使用 AD 将新计算机加入到域中有足够的特权的 AD 帐户。

   具体而言，此命令将在 AD 中创建新的计算机帐户，创建`/etc/krb5.keytab`托管 keytab 文件和配置的域中`/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > 如果你看到的错误，"未安装必要的包，"，则应安装这些包使用你的 Linux 分发的包管理器运行之前`realm join`试命令。
   >
   > 如果收到错误，"权限不足，无法加入域，"，然后需要与域管理员检查有足够的权限将 Linux 计算机加入到你的域。
   >
   > 如果收到错误，"KDC 答复与预期值，不匹配"您可能未指定用户的正确的领域名称。 领域名称区分大小写、 通常大写，并可以使用命令标识`realm discover contoso.com`。
   
   > SQL Server 使用 SSSD 和 NSS 用于映射到的安全标识符 (SID) 的用户帐户和组。 SSSD 必须配置并运行 SQL Server 已成功创建 AD 的登录名的顺序。 Realmd 通常自动执行此操作一部分的加入域，但在某些情况下您必须单独执行此操作。
   >
   > 请查看以下内容，以配置[SSSD 手动](https://access.redhat.com/articles/3023951)，和[配置 NSS 用于 SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. 验证，可以现在从域中，收集有关用户的信息，以及你可以获取作为该用户的 Kerberos 票证。

   下面的示例使用**id**，  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**，和**[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** 这样的命令。

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
   > 如果`id user@contoso.com`返回，"没有这种用户，"请确保 SSSD 服务成功启动运行命令`sudo systemctl status sssd`。 如果该服务正在运行并且您仍然看到"没有此类用户"错误，请尝试启用详细日志记录的 SSSD。 有关详细信息，请参阅 Red Hat 文档[故障诊断 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)。
   >
   > 如果`kinit user@CONTOSO.COM`返回，"KDC 应答不符期望获取初始的凭据，同时"确保大写指定领域。

有关详细信息，请参阅 Red Hat 文档[发现和加入标识域](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)。 

## <a id="createuser"></a> 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并设置 SPN

  > [!NOTE]
  > 下一个步骤使用您[完全合格的域名称](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果您是在**Azure**，您必须**[创建一个](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 在继续操作之前。

1. 在您的域控制器上运行[New ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令来创建一个新的 AD 用户使用永不过期的密码。 本示例名称帐户"mssql，"但该帐户名称可以是您喜欢的任何。 系统将提示您为帐户输入新密码：

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 这样，SQL Server 凭据并不与其他服务使用同一帐户共享是有专门的广告帐户为 SQL Server 安全最佳做法。 但是，您可以重用现有的 AD 帐户如果您愿意，如果您知道该帐户的密码 （所需的下一步生成 keytab 文件）。

2. 设置为此帐户使用的 ServicePrincipalName (SPN)`setspn.exe`工具。 SPN 必须完全按照下面的示例中指定的方式进行格式化。 可以找到的完全限定的域名[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机通过运行`hostname --all-fqdns`在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机和 TCP 端口应是 1433年，除非您已配置了[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用不同的端口号。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果您收到错误，"没有足够的访问权限，"则需要与域管理员联系，检查您具有足够的权限对该帐户设置 SPN。
   >
   > 如果您在以后更改 TCP 端口，则需要再次运行 setspn 命令，使用新的端口号。 您还需要在下一节中的步骤添加 SQL Server 服务 keytab 新 SPN。

3. 有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab

1. 检查上一步中创建的广告帐户密钥版本编号 (kvno)。 它通常为 2，但它可能是另一个整数，如果多次更改该帐户的密码。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机，运行以下命令：

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. 创建具有的 keytab 文件**[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** AD 用户在上一步中创建的。 出现提示时，输入密码的 AD 帐户。

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > Ktutil 工具不验证密码，所以请确保您正确地输入。

3. 任何人都有权访问此`keytab`文件可以模拟[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]域，因此，请确保您限制访问此类文件，仅`mssql`帐户具有读取访问权限：

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用此`keytab`Kerberos 身份验证的文件：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a id="createsqllogins"></a> 在 TRANSACT-SQL 中创建基于 AD 的登录名

1. 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，并创建一个新的、 基于 AD 的登录：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. 确保现在在登录[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系统目录视图：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

登录到客户端计算机使用您的域凭据。 现在，您可以连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无需密码，重新输入使用 AD 身份验证。 如果您创建了一个 AD 组的登录名，任何 AD 用户是该组的成员可以以相同的方式连接。

客户端以使用 AD 身份验证的特定连接字符串参数取决于你正在使用哪个驱动程序。 请考虑下列示例：

* `sqlcmd` 已加入域的 Linux 客户端上

   登录到已加入域的 Linux 客户端使用`ssh`和您的域凭据：

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   请确保已安装[mssql 工具](sql-server-linux-setup-tools.md)包，然后使用连接`sqlcmd`无需指定任何凭据：

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* 已加入域的 Windows 客户端上的 SSMS

   登录到已加入域的 Windows 客户端使用你的域凭据。 请确保[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]安装，则连接到你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过指定实例**Windows 身份验证**中**连接到服务器**对话框。

* 使用其他客户端驱动程序的 AD 身份验证

  * JDBC:[使用 Kerberos 集成身份验证连接 SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC:[使用集成身份验证](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET:[连接字符串语法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
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
>[加密连接到 Linux 上的 SQL Server](sql-server-linux-encrypted-connections.md)
