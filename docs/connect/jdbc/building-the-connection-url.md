---
title: 生成连接 URL | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 889571da70eaf43878d4226751b2b031853f802f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922630"
---
# <a name="building-the-connection-url"></a>创建连接 URL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  连接 URL 的一般形式为：  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 其中：  
  
-   jdbc:sqlserver://（必需）称为子协议，且为常数  。  
  
-   serverName（可选）是要连接到的服务器的地址  。 它可以是 DNS 或 IP 地址，也可以是本地计算机地址 localhost 或 127.0.0.1。 如果未在连接 URL 中指定服务器名称，则必须在属性集中指定。  
  
-   instanceName（可选）是 serverName 上要连接到的实例  。 如果未指定，则会连接到默认实例。  
  
-   portNumber（可选）是 serverName 上要连接到的端口  。 默认值为 1433。 如果使用默认端口，则无需在 URL 中指定端口及其前面的“:”。  
  
    > [!NOTE]  
    >  若要获得最佳连接性能，应在连接到指定实例时设置 portNumber。 这将避免为了确定端口号而与服务器进行往返通讯。 如果同时使用 portNumber 和 instanceName，则会优先使用 portNumber，而忽略 instanceName。  
  
-   property（可选）是一个或多个选项连接属性  。 有关详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。 可指定该列表中的任何属性。 属性只能用分号（“;”）分隔，且不允许重复。  
  
> [!CAUTION]  
>  出于安全考虑，应避免根据用户输入的内容创建连接 URL。 只应在 URL 中指定服务器名称和驱动程序。 对于用户名和密码值，请使用连接属性集。 有关 JDBC 应用程序安全性的详细信息，请参阅[保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)。  
  
## <a name="connection-examples"></a>连接示例  
 使用用户名和密码连接到本地计算机上的默认数据库：  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  尽管前面的示例在连接字符串中使用了用户名和密码，但您应使用集成安全性，因为这样做更安全。 有关详细信息，请参阅本主题后面部分的[通过集成身份验证进行连接](#Connectingintegrated)一节。  
  
 以下连接字符串演示了如何使用集成身份验证和 Kerberos，从一个在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的任何操作系统上运行的应用程序连接到 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 数据库：  
  
```java
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 使用集成身份验证连接到本地计算机上的默认数据库：  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 连接到远程服务器上的指定数据库：  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 连接到远程服务器上的默认端口：  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 通过指定自定义应用程序名称进行连接：  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>命名的多个 SQL Server 实例  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许在每台服务器上安装多个数据库实例。 每个实例都由一个专用名称所标识。 若要连接到指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，可以使用指定实例的端口号（首选），也可将实例名指定为 JDBC URL 属性或 datasource 属性  。 如果未指定实例名属性或端口号属性，则会创建与默认实例的连接。 请看以下示例：  
  
 若要使用端口号，请执行下列操作：  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 若要使用 JDBC URL 属性，请执行下列操作：  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>转义连接 URL 中的值  
 由于包含特殊字符（如空格、分号和引号），所以必须转义连接 URL 值的某些部分。 如果这些字符包含在大括号中，则 JDBC 驱动程序将支持对其进行转义。 例如，{;} 将转义分号。  
  
 转义的值可以包含特殊字符（特别是“=”、“;”、“[]”和空格），但不能包含大括号。 应将必须进行转义且包含大括号的值添加到属性集中。  
  
> [!NOTE]  
>  大括号内的空白为原义字符，不能删除。  
  
##  <a name="connecting-with-integrated-authentication-on-windows"></a><a name="Connectingintegrated"></a> 在 Windows 上通过集成身份验证进行连接  
 JDBC 驱动程序支持通过 integratedSecurity 连接字符串属性在 Windows 操作系统上使用“类型 2”集成身份验证。 若要使用集成身份验证，请将 mssql-jdbc_auth-\<version>-\<arch>.dll 文件复制计算机中 Windows 系统路径下的 JDBC 驱动程序安装目录中。  
  
 mssql-jdbc_auth-\<version>-\<arch>.dll 文件的安装位置如下：  
  
 \<安装目录  >\sqljdbc_\<版本  >\\<语言  >\auth\  
  
 有关 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持的任何操作系统，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) 以了解 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 中新增的一个功能，该功能允许应用程序使用集成身份验证和类型 4 Kerberos 来连接数据库。  
  
> [!NOTE]  
>  如果运行的是 32 位的 Java 虚拟机 (JVM)，则使用 x86 文件夹中的 mssql-jdbc_auth-\<version>-\<arch>.dll 文件，即使操作系统是 x64 版本也不例外。 如果在 x64 处理器上运行 64 位 JVM，则使用 x64 文件夹中的 mssql-jdbc_auth-\<version>-\<arch>.dll 文件。  
  
 也可以设置 java.library.path 系统属性来指定 mssql-jdbc_auth-\<version>-\<arch>.dll 的目录。 例如，如果 JDBC 驱动程序安装在默认目录中，您可以在 Java 应用程序启动时使用以下虚拟机 (VM) 参数来指定 DLL 的位置：  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>通过 IPv6 地址进行连接  
 JDBC 驱动程序支持结合使用 IPv6 地址以及连接属性集合和 serverName 连接字符串属性。 连接字符串不支持在 IPv6 地址中使用初始 serverName 值，如 jdbc:sqlserver://serverName   。 使用 serverName 的名称而不是原始 IPv6 地址将适用于连接中的所有情况  。 以下实例提供了详细信息。  
  
 **使用 serverName 属性**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **使用属性集合**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
