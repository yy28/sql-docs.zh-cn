---
title: 使用 Kerberos 集成身份验证连接到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2215e9f6b6c8cd0e19c220d16ebc7a1520550a42
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026194"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>使用 Kerberos 集成身份验证连接到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 开始，应用程序可使用 authenticationScheme 连接属性指示它希望连接到使用类型 4 Kerberos 集成身份验证的数据库  。 有关连接属性的详细信息, 请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。 有关 Kerberos 的详细信息, 请参阅[Microsoft kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)。

对 Java Krb5LoginModule 使用集成身份验证时，可使用[类 Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html) 配置该模块  。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 针对 IBM Java VM 设置了以下属性：

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 针对所有其他 Java VM 设置了以下属性：

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Remarks

在之前  , 应用程序可以通过使用 integratedSecurity 连接属性并引用 sqljdbc_auth 来指定集成身份验证 (使用 Kerberos 或 NTLM, 具体取决于可用的) **。** [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]介绍如何[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。

从 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 开始，应用程序可使用 authenticationScheme 连接属性指示它希望通过纯 Java Kerberos 实现连接到使用 Kerberos 集成身份验证的数据库  ：

- 如果希望使用**Krb5LoginModule**进行集成身份验证, 则仍必须指定**integratedSecurity = true**连接属性。 然后, 您还可以指定**authenticationScheme = JavaKerberos**连接属性。

- 若要继续使用**sqljdbc_auth**的集成身份验证, 只需指定**integratedSecurity = true**连接属性 (也可以选择**authenticationScheme = NativeAuthentication**)。

- 如果指定**authenticationScheme = JavaKerberos** , 但不同时指定**integratedSecurity = true**, 则驱动程序将忽略**authenticationScheme**连接属性, 并将会发现用户名和密码连接字符串中的凭据。

使用数据源来创建连接时，可使用 setAuthenticationScheme 以编程方式设置身份验证方案，也可选择性地使用 setServerSpn 为 Kerberos 连接设置 SPN   。

新增了一个记录程序以支持 Kerberos 身份验证：com.microsoft.sqlserver.jdbc.internals.KerbAuthentication。 有关详细信息，请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)。

以下准则将有助于您配置 Kerberos：

1. 在 Windows 注册表中将**AllowTgtSessionKey**设置为1。 有关详细信息，请参阅 [Windows Server 2003 中的 Kerberos 协议注册表项和 KDC 配置项](https://support.microsoft.com/kb/837361)。
2. 请确保 Kerberos 配置（UNIX 环境中的 krb5.conf）指向您的环境中正确的领域和 KDC。
3. 通过使用 kinit 或登录到域来初始化 TGT 缓存。
4. 当在 Windows Vista 或 Windows 7 操作系统上运行使用 authenticationScheme=JavaKerberos 的应用程序时，应使用标准用户帐户  。 但是，如果在管理员帐户下运行应用程序，则该程序必须以管理员特权运行。

> [!NOTE]  
> serverSpn 连接属性仅受 Microsoft JDBC Driver 4.2 及更高版本支持。

## <a name="service-principal-names"></a>服务主体名称

服务主体名称 (SPN) 是客户端用来唯一标识服务实例的名称。

可以使用 serverSpn 连接属性指定 SPN 或只需让驱动程序生成它（默认）  。 此属性采用“MSSQLSvc/fqdn:port\@REALM”的形式，其中 fqdn 是完全限定的域名，port 是端口号，REALM 是 SQL Server 的 Kerberos 领域（采用大写形式）。 如果 Kerberos 配置的默认领域与该 Server 的领域相同且不默认包含在内，则此属性的领域部分可选。 如果想要支持跨领域身份验证方案，其中 Kerberos 配置中的默认领域与服务器的领域不同，则必须使用 serverSpn 属性设置 SPN。

例如, 你的 SPN 可能如下所示: "MSSQLSvc/ZZZZ: 1433\@"。CORP.CONTOSO.COM "

有关服务主体名称 (SPN) 的详细信息，请参阅：

- [如何在 SQL Server 中使用 Kerberos 身份验证](https://support.microsoft.com/kb/319723)

- [对 SQL Server 使用 Kerberos](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> 在6.2 版本的 JDBC driver 之前, 若要正确使用跨领域 Kerberos, 则需要显式设置**serverSpn**。
>
> 在6.2 版中, 驱动程序将能够在默认情况下生成**serverSpn** , 即使使用跨领域 Kerberos 也是如此。 尽管也可以显式使用**serverSpn** 。

## <a name="creating-a-login-module-configuration-file"></a>创建登录模块配置文件

您也可选择指定 Kerberos 配置文件。 如果未指定配置文件，则以下设置有效：

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

如果您决定创建登录模块配置文件，则该文件必须遵循以下格式：

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

登录配置文件包含一个或多个条目，每个条目分别指定应用于某个特定应用程序或多个应用程序的基础身份验证技术。 例如，

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

因此，每个登录模块配置文件条目均包含一个名称，该名称后跟一个或多个特定于 LoginModule 的条目，其中每个特定于 LoginModule 的条目以分号结尾，并且整个特定于 LoginModule 的条目组都包含在大括号中。 每个配置文件条目均以分号结尾。

除了允许驱动程序使用登录配置模块文件中指定的设置获取 Kerberos 凭据之外，驱动程序还可使用现有凭据。 如果应用程序需要使用多个用户凭据来创建连接，则这非常有用。

在尝试使用指定登录模块登录之前，如果现有凭据可用，则驱动程序将尝试使用它们。 因此，在使用 `Subject.doAs` 方法在特定上下文中执行代码时，可通过传递到 `Subject.doAs` 调用的凭据创建连接。

有关详细信息，请参阅 [JAAS 登录配置文件](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)和[类 Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)。

从 Microsoft JDBC Driver 6.2 开始, 可以选择使用连接属性`jaasConfigurationName`传递登录模块配置文件的名称, 这允许每个连接都有自己的登录配置。

## <a name="creating-a-kerberos-configuration-file"></a>创建 Kerberos 配置文件

有关 Kerberos 配置文件的详细信息，请参阅 [Kerberos 需求](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)。

这是一个示例域配置文件，其中 YYYY 和 ZZZZ 是域名。

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>启用域配置文件和登录模块配置文件

您可以使用 -Djava.security.krb5.conf 启用域配置文件。 您可以启用具有 **-Djava**的登录模块配置文件。

例如, 可以使用以下命令启动应用程序:

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>验证能否通过 Kerberos 访问 SQL Server

在 SQL Server Management Studio 中运行以下查询：

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

请确保您具有运行此查询的必要权限。

## <a name="constrained-delegation"></a>约束委派

从 Microsoft JDBC Driver 6.2 开始, 驱动程序支持 Kerberos 约束委派。 委托的凭据可以作为 jgss. GSSCredential 对象传入, 驱动程序使用这些凭据来建立连接。

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>使用主体名称和密码的 Kerberos 连接

从 Microsoft JDBC Driver 6.2 开始, 驱动程序可以使用连接字符串中传递的主体名称和密码建立 Kerberos 连接。

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

如果用户属于 krb5.conf 文件中设置的 default_realm, 则 username 属性不需要领域。 当`userName`与`password` `integratedSecurity=true;`和属性`authenticationScheme=JavaKerberos;`一起设置和时, 将通过将 "用户名" 值作为 Kerberos 主体以及提供的密码建立连接。

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>在同一域中的 Unix 计算机上使用 Kerberos 身份验证

本指南假设已有一个有效的 Kerberos 设置。 在使用 Kerberos 身份验证的 Windows 计算机上运行以下代码, 以验证上述是否为 true。 如果成功, 代码会将 "身份验证方案: KERBEROS" 打印到控制台。 不需要任何其他运行时标志、依赖关系或驱动程序设置。 可以在 Linux 上运行相同的代码块来验证连接是否成功。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. 域将客户端计算机加入到与服务器相同的域中。
2. 可有可无设置默认的 Kerberos 票证位置。 通过设置`KRB5CCNAME`环境变量, 可以很方便地完成此操作。
3. 通过生成新的 Kerberos 票证, 或在默认的 Kerberos 票证位置中放置现有 Kerberos 票证。 若要生成票证, 只需使用终端并通过`kinit USER@DOMAIN.AD` "用户" 和 "域" 来初始化票证。AD "是主体和域。 例如 `kinit SQL_SERVER_USER03@MICROSOFT.COM`。 票证将在默认票证位置或`KRB5CCNAME`路径 (如果已设置) 中生成。
4. 终端会提示输入密码, 请输入密码。
5. 通过`klist`验证票证中的凭据, 并确认凭据是要用于身份验证的凭据。
6. 运行上述示例代码并确认 Kerberos 身份验证成功。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
