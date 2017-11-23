---
title: "使用集成身份验证 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 162b94d551ea8625b6b22fafec61e19038dc2051
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="using-integrated-authentication"></a>使用集成身份验证
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用 Kerberos 的 Linux 和 macOS 支持连接在集成的身份验证。 它支持 MIT Kerberos 密钥分发中心 (KDC)，并适用于通用安全服务应用程序程序接口 (GSSAPI) 和 Kerberos v5 库。
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>使用集成身份验证连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]从 ODBC 应用程序  

你可以通过指定启用 Kerberos 集成身份验证**Trusted_Connection = yes**的连接字符串中**SQLDriverConnect**或**SQLConnect**。 例如：  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
当使用 DSN 连接，你还可以添加**Trusted_Connection = yes**到中的 DSN 条目`odbc.ini`。
  
`-E`选项`sqlcmd`和`-T`选项`bcp`还可用于指定集成身份验证; 请参阅[使用连接**sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)和[使用连接**bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md)有关详细信息。

确保要连接到其中的客户端主体[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]已使用 Kerberos KDC 身份验证。
  
**ServerSPN** 和 **FailoverPartnerSPN** 不受支持。  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>作为服务运行到部署的 Linux 或 macOS ODBC 驱动程序的应用程序设计

系统管理员可以部署应用程序以使用 Kerberos 身份验证连接到的服务运行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
你首先需要配置 Kerberos 客户端上，然后确保应用程序可以使用默认主体的 Kerberos 凭据。

请确保使用`kinit`或 PAM （可插入身份验证模块） 来获取并在连接使用，通过以下方法之一，此主体缓存 TGT:  
  
-   运行`kinit`，并传入的主体名称和密码。  
  
-   运行`kinit`、 传入的主体名称并包含所创建的主体的密钥的 keytab 文件的位置`ktutil`。  
  
-   请确保登录到系统已进行使用 Kerberos PAM （可插入身份验证模块）。

应用程序运行时作为一种服务，因为 Kerberos 凭据过期设计使然，续订凭据后，以确保连续的服务可用性。 ODBC 驱动程序不续订凭据重试。请确保有`cron`作业或定期运行以续订其到期前的凭据的脚本。 若要避免为每个续订需要密码，你可以使用 keytab 文件。  
  
[“Kerberos 配置和使用”](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 提供有关 Linux 上的 Kerberize 服务的详细信息。
  
## <a name="tracking-access-to-a-database"></a>跟踪对数据库的访问

当使用系统帐户来访问，则数据库管理员可以创建对数据库的访问的审核痕迹[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用集成身份验证。  
  
登录到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用系统帐户和模拟安全上下文的 linux 操作系统上没有任何功能。 因此，需要更多信息来确定用户。
  
审核中的活动[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]代表不同于系统帐户的用户，应用程序必须使用[!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**。  
  
若要提高应用程序性能，应用程序可以将连接池与集成身份验证和审核结合使用。 但是，组合连接池时，集成的身份验证和审核产生安全风险因为 unixODBC 驱动程序管理器允许不同的用户可以重复使用已入池的连接。 有关详细信息，请参阅 [ODBC 连接池](http://www.unixodbc.org/doc/conn_pool.html)。  

在重复使用之前, 应用程序必须通过重置已入池的连接执行`sp_reset_connection`。  

## <a name="using-active-directory-to-manage-user-identities"></a>使用 Active Directory 管理用户身份

应用程序系统管理员不需要管理单独的登录凭据集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 可以针对集成身份验证将 Active Directory 配置为密钥发行中心 (KDC)。 请参阅[Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx)有关详细信息。

## <a name="using-linked-server-and-distributed-queries"></a>使用链接服务器和分布式查询

开发人员可以部署可使用链接服务器或分布式查询的应用程序，数据库管理员无需保留单独的 SQL 凭据集。 在此情况下，开发人员必须配置应用程序使用集成身份验证：  
  
-   用户登录到客户端计算机，并对应用程序服务器进行身份验证。  
  
-   应用程序服务器作为不同的数据库进行身份验证和连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]作为另一个数据库数据库用户进行身份验证 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
配置集成身份验证后，凭据将传递给链接服务器。  
  
## <a name="integrated-authentication-and-sqlcmd"></a>集成身份验证和 sqlcmd
访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用集成身份验证，使用`-E`选项`sqlcmd`。 确保运行的帐户`sqlcmd`与默认 Kerberos 客户端主体相关联。

## <a name="integrated-authentication-and-bcp"></a>集成身份验证和 bcp
访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用集成身份验证，使用`-T`选项`bcp`。 确保运行的帐户`bcp`与默认 Kerberos 客户端主体相关联。 
  
它是使用错误`-T`与`-U`或`-P`选项。
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>支持的语法通过注册的 SPN[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

Spn 在连接字符串或连接属性中使用的语法如下所示：  

|语法|说明|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|使用 TCP 时访问接口生成的默认 SPN。 *port* 为 TCP 端口号。 *fqdn* 是一个完全限定域名。|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Linux 或 macOS 计算机与 Active Directory 进行身份验证

若要配置 Kerberos，在其中输入数据`krb5.conf`文件。 `krb5.conf`处于`/etc/`但你可以引用另一个文件，例如使用语法`export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`。 以下是一个示例`krb5.conf`文件：  
  
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
  
如果你在 Linux 或 macOS 计算机配置为使用与提供的 DNS 服务器的 Windows DHCP 服务器动态主机配置协议 (DHCP) 来使用，则可以使用**dns_lookup_kdc = true**。 现在，你可以使用 Kerberos 来发出命令登录到你的域`kinit alias@YYYY.CORP.CONTOSO.COM`。 参数传递给`kinit`是区分大小写和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]配置为在域中的计算机必须具有该用户`alias@YYYY.CORP.CONTOSO.COM`添加为登录名。 现在，你可以使用受信任的连接 (**Trusted_Connection = YES**在连接字符串中， **bcp-T**，或**sqlcmd-E**)。  
  
Linux 或 macOS 计算机上的时间和时间 Kerberos 密钥分发中心 (KDC) 必须关闭。 确保您的系统时间已正确设置了，例如通过使用网络时间协议 (NTP)。  

如果 Kerberos 身份验证失败，在 Linux 或 macOS 上的 ODBC 驱动程序不使用 NTLM 身份验证。  

有关对 Linux 或 macOS 计算机与 Active Directory 进行身份验证的详细信息，请参阅[与 Active Directory 进行身份验证 Linux 客户端](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048)和[与 Active Directory集成OSX的最佳实践](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). 有关配置 Kerberos 的详细信息，请参阅[麻省理工学院的 Kerberos 文档](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)。

## <a name="see-also"></a>另请参阅  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)

[使用 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
