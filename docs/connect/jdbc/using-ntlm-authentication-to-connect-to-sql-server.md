---
title: 使用 NTLM 身份验证连接到 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 2fab4794544ada07e0bf5e690da35b72ad6b7421
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026104"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>使用 NTLM 身份验证连接到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

允许应用程序使用 authenticationScheme 连接属性来指示它需要使用 NTLM v2 身份验证连接到数据库。  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 

以下属性还用于 NTLM 身份验证:

- **域 =** 域名可有可无
- **用户 = 用户名**
- **密码 = 密码**
- **integratedSecurity = true**

除**域**之外的其他属性是必需的, 如果使用**NTLM** authenticationScheme 属性时, 驱动程序将引发错误。 

有关连接属性的详细信息, 请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。 有关 Microsoft NTLM 身份验证协议的详细信息, 请参阅[MICROSOFT ntlm](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm)。

## <a name="remarks"></a>Remarks

请参阅[网络安全: LAN Manager 身份验证级别](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level), 了解用于控制 NTLM 身份验证行为的 SQL server 设置。 

## <a name="logging"></a>日志记录

新增了一个记录程序以支持 NTLM 身份验证：com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication。 有关详细信息，请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)。

## <a name="datasource"></a>DataSource

使用数据源创建连接时, 可使用**setAuthenticationScheme**、 **setDomain**和 (可选) **SETSERVERSPN**以编程方式设置 NTLM 属性。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>服务主体名称

服务主体名称 (SPN) 是客户端用来唯一标识服务实例的名称。

可以使用 serverSpn 连接属性指定 SPN 或让驱动程序生成它（默认）  。 此属性采用“MSSQLSvc/fqdn:port\@REALM”的形式，其中 fqdn 是完全限定的域名，port 是端口号，REALM 是 SQL Server 的领域（采用大写形式）。 此属性的领域部分是可选的, 因为默认领域与服务器的领域相同。

例如, 你的 SPN 可能如下所示: "MSSQLSvc/: 1433"

有关服务主体名称 (SPN) 的详细信息，请参阅：

- [客户端连接中的服务主体名称 (SPN) 支持](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> serverSpn 连接属性仅受 Microsoft JDBC Driver 4.2 及更高版本支持。

> 在6.2 版本的 JDBC driver 之前, 需要显式设置**serverSpn**。 从6.2 版的发行版中, 默认情况下, 驱动程序将能够生成**serverSpn** , 但也可以显式使用**serverSpn** 。

## <a name="security-risks"></a>安全风险

NTLM 协议是一种具有各种漏洞的旧身份验证协议, 这会带来安全风险。 它基于一个相对弱的加密方案, 容易受到各种攻击。 它已替换为 Kerberos, 这是一种更安全的安全建议。 NTLM 身份验证仅应在安全的受信任环境中使用, 或在不能使用 Kerberos 的情况下使用。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]仅支持 NTLM v2, 这对原始 v1 协议具有一些安全改进。 还建议使用 It'ss 来启用扩展保护, 或者使用 SSL 加密来提高安全性。 

有关如何启用扩展保护和的详细信息, 请参阅:

- [使用扩展保护连接到数据库引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

有关连接 SSL 加密的详细信息, 请参阅:

- [使用 SSL 加密进行连接](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 在7.4 版本中, 不  支持启用扩展保护和加密。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
