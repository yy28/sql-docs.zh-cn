---
title: 在 Linux 上的 SQL Server 的 active Directory 身份验证教程 |Microsoft 文档
description: 本教程提供有关在 Linux 上的 SQL Server 的 AAD 身份验证的配置步骤。
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
ms.openlocfilehash: df3cea6d47d50464fe0b8a7f2573c230585b9cb1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>在 Linux 上的 SQL 服务器的教程： 使用 Active Directory 身份验证

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持 Active Directory (AD) 身份验证，也称为集成身份验证的 linux 操作系统上。 有关概述，请参阅[在 Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-auth-overview.md)。

本教程包括以下任务：

> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机到 AD 域
> * 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和设置 SPN
> * 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab
> * 在 TRANSACT-SQL 中创建基于 AD 的登录名
> * 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

## <a name="prerequisites"></a>必要條件

在配置 AD 身份验证之前，您需要：

* 设置你的网络上的 AD 域控制器 (Windows)  
* 安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机到 AD 域

使用以下步骤以加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 Active Directory 域的主机：

1. 使用**[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** 加入你的 AD 域的主机。 如果你尚未安装的 realmd 和 Kerberos 客户端包上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用你的 Linux 分发的包管理器的主机：

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 客户端程序包安装将提示您输入的领域名称，请以大写形式输入你的域名。

   > [!NOTE]
   > 本演练使用"contoso.com"和"CONTOSO.COM"作为示例的域和领域名称，分别。 你应将其与你自己的值。 这些命令是区分大小写，因此请确保你使用大写只要在本演练中使用。

1. 配置你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机机以用作 DNS 名称服务器的 AD 域控制器的 IP 地址。 

   - **Ubuntu**:

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
      > 网络接口 (eth0) 可能因不同的计算机而不同。 若要了解你使用哪一个，运行 ifconfig，并复制有一个 IP 地址和传输和接收的字节的接口。

      编辑此文件之后, 重新启动网络服务：

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      现在请检查你`/etc/resolv.conf`文件包含类似下面的示例行：  

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

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

     现在请检查你`/etc/resolv.conf`文件包含类似下面的示例行：  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. 加入域

   一旦你已确认您的 DNS 配置正确，请通过运行以下命令加入域。 你必须进行身份验证使用 AD 将新计算机加入到域中具有足够的权限的 AD 帐户。

   具体而言，此命令将在 AD 中创建新的计算机帐户、 创建`/etc/krb5.keytab`承载 keytab 文件和配置中的域`/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > 如果你看到的错误，"未安装必需的包，"，然后应安装这些包使用你的 Linux 分发的包管理器在运行前`realm join`试命令。
   >
   > 如果收到错误，"权限不足，无法加入域，"，然后需要与域管理员检查有足够的权限将 Linux 计算机加入到你的域。
   >
   > 如果收到错误，"KDC 答复不匹配的预期目标，"你可能未指定用户的正确领域名称。 领域名称区分大小写、 通常大写，并可以使用命令标识`realm discover contoso.com`。
   
   > SQL Server 使用 SSSD 和 NSS 用于将用户帐户和组映射到安全标识符 (SID)。 SSSD 必须进行配置并运行 SQL Server 已成功创建 AD 登录名的顺序。 Realmd 通常自动执行此操作一部分的加入域，但在某些情况下你必须单独执行此操作。
   >
   > 请查看以下配置[SSSD 手动](https://access.redhat.com/articles/3023951)，和[配置 NSS 用于 SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. 验证，可以现在从域中，收集有关用户的信息以及您可以获取作为该用户的 Kerberos 票证。

   下面的示例使用**id**，  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**，和**[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** 此的命令。

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

## <a id="createuser"></a> 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和设置 SPN

  > [!NOTE]
  > 下一个步骤使用你[完全限定的域名称](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果你在**Azure**，你必须**[创建一个](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)** 在继续操作之前。

1. 在你的域控制器上运行[New-aduser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令以创建新的 AD 用户使用永不过期的密码。 本示例将命名的帐户"mssql，"但帐户名称可以是您喜欢的任何。 系统将提示您输入的帐户的新密码：

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 它是安全的最佳做法，对于 SQL Server，有一个专用的 AD 帐户，以便不会与其他服务使用同一个帐户共享 SQL Server 的凭据。 但是，你可以重用现有的 AD 帐户如果您愿意，如果你知道该帐户的密码 （需要在下一步中生成 keytab 文件）。

2. 设置此帐户使用的 ServicePrincipalName (SPN)`setspn.exe`工具。 SPN 必须完全按照下面的示例中指定的方式进行格式化。 你可以找到的完全限定的域名称[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过运行的主机`hostname --all-fqdns`上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机和 TCP 端口应为 1433年，除非已配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]若要使用不同的端口号。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果收到错误，"没有足够的访问权限，"然后你需要检查与域管理员您具有足够的权限，此帐户上设置 SPN。
   >
   > 如果在将来更改的 TCP 端口，然后你需要使用新的端口号再次运行 setspn 命令。 你还需要将新的 SPN 添加到 SQL Server 服务 keytab，按照下一节中的步骤。

3. 有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab

1. 在上一步中创建 AD 帐户，请检查密钥版本号 (kvno)。 它通常为 2，但它可能是另一个整数，如果您多次更改帐户的密码。 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机计算机，运行以下命令：

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. 创建具有的 keytab 文件**[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** 为你在上一步中创建的 AD 用户。 出现提示时，输入该 AD 帐户的密码。

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > 不，ktutil 工具不验证的密码，因此请确保正确输入。

3. 任何人有权访问此`keytab`文件可以模拟[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在域中，因此请确保你限制对此类的文件访问，它仅`mssql`帐户具有读取权限：

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]才能使用此`keytab`Kerberos 身份验证的文件：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a id="createsqllogins"></a> 在 TRANSACT-SQL 中创建基于 AD 的登录名

1. 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]并创建新的、 基于 AD 的登录名：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. 验证登录名现在列在[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系统目录视图：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

登录到客户端计算机使用域凭据。 现在你可以连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无需你的密码，重新输入通过使用 AD 身份验证。 如果你创建的 AD 组的登录名，只要 AD 用户是该组的成员可以连接的方式相同。

客户端使用 AD 身份验证的特定连接字符串参数取决于你正在使用哪个驱动程序。 请考虑下列示例：

* `sqlcmd` 在已加入域的 Linux 客户端

   登录到已加入域的 Linux 客户端使用`ssh`和你的域凭据：

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   请确保已安装[mssql 工具](sql-server-linux-setup-tools.md)包，然后使用连接`sqlcmd`没有指定任何凭据：

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* 已加入域的 Windows 客户端上的 SSMS

   登录到已加入域的 Windows 客户端使用域凭据。 请确保[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]安装，然后连接到你[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]通过指定实例**Windows 身份验证**中**连接到服务器**对话框。

* 使用其他客户端驱动程序的 AD 身份验证

  * JDBC:[使用 Kerberos 集成身份验证连接 SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC:[使用集成身份验证](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET:[连接字符串语法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
## <a name="next-steps"></a>后续步骤

在本教程中，我们在遍历如何设置与在 Linux 上的 SQL Server 的 Active Directory 身份验证。 你应该了解一下如何到：
> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机到 AD 域
> * 创建 AD 用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和设置 SPN
> * 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服务 keytab
> * 在 TRANSACT-SQL 中创建基于 AD 的登录名
> * 连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 身份验证

接下来，将介绍其他安全方案适用于 SQL Server 上 Linux。

> [!div class="nextstepaction"]
>[加密连接到 Linux 上的 SQL Server](sql-server-linux-encrypted-connections.md)
