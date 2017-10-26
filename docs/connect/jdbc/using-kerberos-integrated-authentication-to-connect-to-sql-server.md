---
title: "使用 Kerberos 集成身份验证连接到 SQL Server |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f26a429563aaf5c079c45b064b4723cb19cada90
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>使用 Kerberos 集成身份验证连接 SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  从[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，应用程序可以使用**authenticationScheme**连接属性以指示它想要连接到数据库使用的类型 4 Kerberos 集成身份验证。 请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)有关连接属性的详细信息。 有关 Kerberos 的详细信息，请参阅[Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)。  
  
 与 Java 结合使用集成身份验证时**Krb5LoginModule**，你可以配置模块使用[类 Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)。  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] IBM Java 虚拟机将设置以下属性：  
  
-   **useDefaultCcache = true**  
  
-   **moduleBanner = false**  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]对于所有其他 Java Vm 将设置以下属性：  
  
-   **useTicketCache = true**  
  
-   **doNotPrompt = true**  
  
## <a name="remarks"></a>注释  
 之前[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，应用程序可以指定集成身份验证 （使用 Kerberos 或 NTLM，具体取决于在其上可用） 使用**integratedSecurity**连接属性和通过引用**sqljdbc_auth.dll**中所述，[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
 从[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，应用程序可以使用**authenticationScheme**连接属性以指示它想要连接到使用 Kerberos 数据库集成使用纯 Java Kerberos 的身份验证实现：  
  
-   如果您希望集成身份验证使用**Krb5LoginModule**，仍必须指定**integratedSecurity = true**连接属性。 然后，将还指定**authenticationScheme = JavaKerberos**连接属性。  
  
-   若要继续使用集成身份验证用于**sqljdbc_auth.dll**，只需指定**integratedSecurity = true**连接属性 (及 （可选） **authenticationScheme =NativeAuthentication**)。  
  
-   如果指定**authenticationScheme = JavaKerberos**但不是同时指定**integratedSecurity = true**，驱动程序将忽略**authenticationScheme**连接属性，并且其将期望在连接字符串中找到用户名称和密码凭据。  
  
 在使用中的数据源创建连接时，可以以编程方式设置的身份验证方案使用 setAuthenticationScheme 并 （可选） 设置为 Kerberos 连接使用的 SPN **setServerSpn**。  
  
 新增了一个记录程序以支持 Kerberos 身份验证：com.microsoft.sqlserver.jdbc.internals.KerbAuthentication。 有关详细信息，请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)。  
  
 以下准则将有助于您配置 Kerberos：  
  
1.  设置**AllowTgtSessionKey**为在 Windows 注册表中的 1。 有关详细信息，请参阅[Kerberos 协议注册表项，并且在 Windows Server 2003 的 KDC 配置密钥](http://support.microsoft.com/kb/837361)。  
  
2.  请确保 Kerberos 配置（UNIX 环境中的 krb5.conf）指向您的环境中正确的领域和 KDC。  
  
3.  通过使用 kinit 或登录到域来初始化 TGT 缓存。  
  
4.  当使用的应用程序时**authenticationScheme = JavaKerberos** Windows Vista 或 Windows 7 上运行的操作系统，则应使用标准用户帐户。 但如果以管理员帐户运行应用程序，则必须使用管理员特权运行该应用程序。  
  
> [!NOTE]  
>  通过 Microsoft JDBC 驱动程序 4.2 和更高版本才支持 serverSpn 连接属性。  
  
## <a name="service-principal-names"></a>服务主体名称  
 服务主体名称 (SPN) 是客户端用来唯一标识服务实例的名称。  
  
 你可以指定 SPN 使用**serverSpn**连接属性，或只需将生成为你 （默认值） 的驱动程序。  此属性采用的格式:"MSSQLSvc/fqdn:port@REALM"其中 fqdn 是完全限定的域名，端口为端口号，领域是中大写字母的 SQL Server 的 Kerberos 领域。  如果你的 Kerberos 配置的默认领域与服务器的领域相同，并且默认情况下不包含该领域，则此属性的领域部分是可选的。  如果想要支持跨领域身份验证方案，其中 Kerberos 配置中的默认领域与服务器的领域不同，则必须使用 serverSpn 属性设置 SPN。  
  
 例如，你 SPN 可能如下所示:"MSSQLSvc/some-server.zzz.corp.contoso.com:1433@ZZZZ.CORP.CONTOSO.COM"  
  
 有关服务主体名称 (SPN) 的详细信息，请参阅：  
  
-   [如何在 SQL Server 中使用 Kerberos 身份验证](http://support.microsoft.com/kb/319723)  
  
-   [使用 SQL Server 的 Kerberos](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> 6.2.0 发布的 JDBC 驱动程序，对适当使用跨领域 Kerberos 之前你需要显式设置**serverSpn**。
>
> 截至 6.2.0 版本中，该驱动程序将能够生成**serverSpn**默认情况下，即使是在使用跨领域 Kerberos。 尽管用户可以使用**serverSpn**显式过。 
  
## <a name="creating-a-login-module-configuration-file"></a>创建登录模块配置文件  
 您也可选择指定 Kerberos 配置文件。 如果未指定配置文件，则以下设置有效：  
  
 Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule 所需 useTicketCache = true;  
  
 IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule 所需 useDefaultCcache = true;  
  
 如果您决定创建登录模块配置文件，则该文件必须遵循以下格式：  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 登录配置文件包含一个或多个条目，每个条目分别指定应用于某个特定应用程序或多个应用程序的基础身份验证技术。 例如：  
  
```  
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 因此，每个登录模块配置文件条目均包含一个名称，该名称后跟一个或多个特定于 LoginModule 的条目，其中每个特定于 LoginModule 的条目以分号结尾，并且整个特定于 LoginModule 的条目组都包含在大括号中。 每个配置文件条目均以分号结尾。  
  
 除了允许驱动程序使用登录配置模块文件中指定的设置获取 Kerberos 凭据之外，驱动程序还可使用现有凭据。 这在您的应用程序需要使用多个用户的凭据创建连接时非常有用。  
  
 在尝试使用指定登录模块登录之前，如果现有凭据可用，则驱动程序将尝试使用它们。 因此，使用 Subject.doAs 方法在特定上下文下执行代码时，将使用传递给 Subject.doAs 调用的凭据创建连接。  
  
 有关详细信息，请参阅[JAAS 登录配置文件](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)和[类 Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)。  

 从 Microsoft JDBC 驱动程序 6.2 开始，（可选） 可以使用连接属性 jaasConfigurationName 传递登录模块配置文件的名称，这可使具有其自己的登录名配置每个连接。
 
## <a name="creating-a-kerberos-configuration-file"></a>创建 Kerberos 配置文件  
 有关 Kerberos 配置文件的详细信息，请参阅[Kerberos 要求](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)。  
  
 下面是一个示例域配置文件，其中 YYYY 和 ZZZZ 是您网站的域名称。  
  
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
 您可以使用 -Djava.security.krb5.conf 启用域配置文件。 你可以启用一个登录名模块配置文件**-Djava.security.auth.login.config**。  
  
 例如，启动应用程序时，您可使用以下命令行：  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>验证可通过 Kerberos 访问 SQL Server  
 在 SQL Server Management Studio 中运行以下查询：  
  
 **从 sys.dm_exec_connections 选择 auth_scheme 其中 session_id = @@spid**  
  
 请确保您具有运行此查询的必要权限。  

## <a name="constrained-delegation"></a>约束的委派
从 Microsoft JDBC 驱动程序 6.2 开始，该驱动程序支持的 Kerberos 约束委派。 委派的凭据可以作为 org.ietf.jgss.GSSCredential 对象传递中，这些凭据由驱动程序，以建立连接。 

```
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>使用主体名称和密码的 Kerberos 连接
从 Microsoft JDBC 驱动程序 6.2 开始，驱动程序可以在连接字符串中建立连接使用的主体名称和密码传递的 Kerberos。 
```
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
如果用户属于在 krb5.conf 文件中设置 default_realm，username 属性不需要领域。 当`userName`和`password`设置连同`integratedSecurity=true;`和`authenticationScheme=JavaKerberos;`属性，该连接使用建立的用户名的值作为 Kerberos 主体沿与提供的密码。
 
## <a name="see-also"></a>另请参阅  
 [连接到 SQL Server 使用 JDBC 驱动程序](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

