---
title: 使用集成身份验证 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0edf87997b8b53266e7597b392bb217288590636
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810142"
---
# <a name="using-integrated-authentication"></a>使用集成身份验证
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持使用 Kerberos 集成身份验证的连接。 它支持 MIT Kerberos 密钥发行中心 (KDC)，并且可以与通用安全服务应用程序编程接口 (GSSAPI) 和 Kerberos v5 库一起使用。
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>使用集成身份验证从 ODBC 应用程序连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

可以启用 Kerberos 集成身份验证，方法是在 SQLDriverConnect 或 SQLConnect 的连接字符串中指定 Trusted_Connection=yes。 例如：  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
当使用 DSN 连接，您还可以添加**Trusted_Connection = yes**中的 DSN 项`odbc.ini`。
  
`-E`的选项`sqlcmd`并`-T`的选项`bcp`还可用于指定集成身份验证; 请参阅[使用连接**sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)和[使用连接**bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md)有关详细信息。

确保要连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的客户端主体已使用 Kerberos KDC 进行身份验证。
  
**ServerSPN** 和 **FailoverPartnerSPN** 不受支持。  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>运行部署的 Linux 或 macOS ODBC 驱动程序应用程序设计，为服务

系统管理员可以将应用程序部署为作为服务运行，以便使用 Kerberos 身份验证连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
首先需要在客户端上配置 Kerberos，然后确保应用程序可以使用默认主体的 Kerberos 凭据。

确保使用 `kinit` 或 PAM（可插入身份验证模块）为主体获取并缓存 TGT 以供连接使用，采用以下任一方法：  
  
-   运行 `kinit`，传入主体名称和密码。  
  
-   运行 `kinit`，传入主体名称和 keytab 文件的位置，该文件包含 `ktutil` 创建的主体密钥。  
  
-   确保已使用 Kerberos PAM（可插入身份验证模块）登录到系统。

应用程序作为服务运行时，因为按照设计 Kerberos 凭据会过期，所以需续订这些凭据以确保服务持续可用。 ODBC 驱动程序不续订凭据重试。请确保有`cron`作业或定期运行以续订其过期前的凭据的脚本。 若要避免为每个续订需要密码，可以使用 keytab 文件。  
  
[“Kerberos 配置和使用”](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 提供有关 Linux 上的 Kerberize 服务的详细信息。
  
## <a name="tracking-access-to-a-database"></a>跟踪对数据库的访问

当通过系统帐户使用集成身份验证访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，数据库管理员可以创建数据库访问的审核线索。  
  
登录到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时需使用系统帐户，并且 Linux 上未提供相关功能来模拟安全上下文。 因此，需要更多信息来确定用户。
  
若要代表用户（而非系统帐户）审核 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的活动，应用程序必须使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE AS。  
  
若要提高应用程序性能，应用程序可以将连接池与集成身份验证和审核结合使用。 但是，合并连接池、集成身份验证和审核会带来安全风险，因为 unixODBC 驱动程序管理器允许不同的用户重复使用已入池的连接。 有关详细信息，请参阅 [ODBC 连接池](http://www.unixodbc.org/doc/conn_pool.html)。  

在重复使用之前，应用程序必须通过执行 `sp_reset_connection` 重置已入池的连接。  

## <a name="using-active-directory-to-manage-user-identities"></a>使用 Active Directory 管理用户身份

应用程序系统管理员不必管理单独的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录凭据集。 可以针对集成身份验证将 Active Directory 配置为密钥发行中心 (KDC)。 请参阅[Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos)有关详细信息。

## <a name="using-linked-server-and-distributed-queries"></a>使用链接服务器和分布式查询

开发人员可以部署可使用链接服务器或分布式查询的应用程序，数据库管理员无需保留单独的 SQL 凭据集。 在这种情况下，开发人员必须将应用程序配置为使用集成身份验证：  
  
-   用户登录到客户端计算机，并对应用程序服务器进行身份验证。  
  
-   应用程序服务器先以其他数据库身份进行验证，然后再连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 先以数据库用户身份进行验证，然后再连接到另一个数据库 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])。  
  
配置集成身份验证后，凭据将传递给链接服务器。  
  
## <a name="integrated-authentication-and-sqlcmd"></a>集成身份验证和 sqlcmd
若要使用集成身份验证访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请使用 `sqlcmd` 的 `-E` 选项。 确保运行的帐户`sqlcmd`与默认 Kerberos 客户端主体相关联。

## <a name="integrated-authentication-and-bcp"></a>集成身份验证和 bcp
若要使用集成身份验证访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请使用 `bcp` 的 `-T` 选项。 确保运行的帐户`bcp`与默认 Kerberos 客户端主体相关联。 
  
它是使用错误`-T`与`-U`或`-P`选项。
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 注册的 SPN 的受支持语法

以下是 SPN 在连接字符串或连接属性中使用的语法：  

|语法|描述|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|使用 TCP 时访问接口生成的默认 SPN。 *port* 是 TCP 端口号。 *fqdn* 是一个完全限定域名。|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>使用 Active Directory 对 Linux 或 macOS 计算机进行身份验证

若要配置 Kerberos，在其中输入数据`krb5.conf`文件。 `krb5.conf` 处于`/etc/`但你可以引用另一个文件，例如使用语法`export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`。 以下是一个示例 `krb5.conf` 文件：  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
如果在 Linux 或 macOS 计算机配置为使用 Windows DHCP 服务器提供的 DNS 服务器使用动态主机配置协议 (DHCP) 来使用，则可以使用**dns_lookup_kdc = true**。 现在，可以使用 Kerberos 通过发出命令登录到你的域`kinit alias@YYYY.CORP.CONTOSO.COM`。 参数传递给`kinit`区分大小写并[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]配置为在域中的计算机必须具有该用户`alias@YYYY.CORP.CONTOSO.COM`添加为登录名。 现在，可以使用信任连接（连接字符串中的 Trusted_Connection=YES、bcp -T 或 sqlcmd -E）。  
  
必须关闭 Linux 或 macOS 计算机上的时间和 Kerberos 密钥分发中心 (KDC) 的时间。 确保系统时间已正确设置，例如通过使用网络时间协议 (NTP)。  

如果 Kerberos 身份验证失败，则 Linux 或 macOS 上的 ODBC 驱动程序不使用 NTLM 身份验证。  

有关 Linux 或 macOS 计算机与 Active Directory 进行身份验证的详细信息，请参阅[使用 Active Directory 对 Linux 客户端](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048)和[OS X 与 Active Directory集成的最佳做法](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). 有关配置 Kerberos 的详细信息，请参阅[MIT Kerberos 文档](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)。

## <a name="see-also"></a>另请参阅  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)

[使用 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
