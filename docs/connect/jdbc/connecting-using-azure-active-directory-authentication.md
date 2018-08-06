---
title: 使用 Azure Active Directory 身份验证连接 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d8f83d0f838304f6f541d1d88e56ce316b07d25
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278838"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证连接

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍如何开发 Java 应用程序以使用用于 SQL Server 的 Microsoft JDBC Driver 6.0 （或更高版本） 的 Azure Active Directory 身份验证功能。

可以使用 Azure Active Directory (AAD) 身份验证，这是连接到 Azure SQL 数据库 v12 的一种机制使用 Azure Active Directory 中的标识。 使用 Azure Active Directory 身份验证以集中管理数据库用户的标识且作为 SQL Server 身份验证的一种替代方法使用。 JDBC 驱动程序，可在要连接到 Azure SQL DB 的 JDBC 连接字符串中指定 Azure Active Directory 凭据。 有关如何配置 Azure Active Directory 身份验证信息，请访问[连接到 SQL 数据库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

若要支持 Azure Active Directory 身份验证，已添加两个新的连接属性：
*   **身份验证**： 使用此属性指示要用于连接的 SQL 身份验证方法。 可能的值为： **ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，以及默认**NotSpecified**.
    * 使用身份验证 = ActiveDirectoryIntegrated 连接到使用集成的 Windows 身份验证的 SQL 数据库。 若要使用此身份验证模式，需要进行联合身份验证的本地 Active Directory 联合身份验证服务 (ADFS) 与云中的 AAD。 这设置以及 Kerberos 票证后, 可访问 Azure SQL DB，而在加入域的计算机登录时提示输入凭据。 
    * 使用身份验证 = ActiveDirectoryPassword 连接到 SQL 数据库使用的 Azure AD 主体名称和密码。
    * 使用身份验证 = SqlPassword 连接到使用用户名/用户和密码属性在 SQL Server。
    * 使用身份验证 = NotSpecified 或保留为默认值，这些身份验证方法均不需要时。

*   **accessToken**： 此属性用于连接到 SQL 数据库使用的访问令牌。 仅可以在驱动程序管理器类中使用 getconnection （） 方法的属性参数设置 accessToken。 它不能在连接 URL 中使用。  

有关详细信息，请参阅身份验证属性[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)页。  


## <a name="client-setup-requirements"></a>客户端安装程序要求
请确保，在客户端计算机上安装以下组件：
* Java 7 或更高版本
*   Microsoft JDBC Driver 6.0 （或更高版本） 的 SQL Server
*   如果使用的访问权限基于令牌的身份验证模式，则需要[azure activedirectory-库-用于-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项，若要从本文运行示例。 有关详细信息，请参阅**使用访问令牌连接**部分。
*   如果使用 ActiveDirectoryPassword 身份验证模式，则需要[azure activedirectory-库-用于-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项。 有关详细信息，请参阅**使用 ActiveDirectoryPassword 身份验证模式进行连接**部分。
*   如果您使用 ActiveDirectoryIntegrated 模式，则需要 azure activedirectory-库-用于-java 和及其依赖项。 有关详细信息，请参阅**使用 ActiveDirectoryIntegrated 身份验证模式进行连接**部分。
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>使用 ActiveDirectoryIntegrated 身份验证模式进行连接
 使用版本 6.4，Microsoft JDBC 驱动程序添加了对多个平台 （Windows/Linux 和 Mac） 上使用 Kerberos 票证的 ActiveDirectoryIntegrated 身份验证支持。
有关详细信息，请参阅[在 Windows、 Linux 和 Mac 上的设置 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)的更多详细信息。 或者，在 Windows 中上, sqljdbc_auth.dll 可以还用于 ActiveDirectoryIntegrated 使用 JDBC 驱动程序进行身份验证。

> [!NOTE]
>  如果使用较旧版本的驱动程序，检查这[链接](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)使用此身份验证模式所需的相应依赖项。 

下面的示例演示如何使用身份验证 = ActiveDirectoryIntegrated 模式。 运行此示例联合使用 Azure Active Directory 域加入计算机上。 表示你的 Azure AD 主体，或一个组的包含的数据库用户，你属于、 必须存在于数据库，并且必须具有 CONNECT 权限。 

构建和运行该示例中，客户端计算机上之前 (上，你想要运行该示例)，下载[azure activedirectory-库-用于-java 库](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项，并将其包含在 Java 生成路径

将服务器/数据库名称替换你在以下行中的服务器/数据库名称为执行该示例之前：

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

该示例以使用 ActiveDirectoryIntegrated 身份验证模式：
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
客户端计算机上自动运行此示例使用 Kerberos 票证并没有密码是必需的。 如果建立连接，应看到以下消息：
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>在 Windows、 Linux 和 Mac 上设置 Kerberos 票证

需要设置链接到 Windows 域帐户的当前用户的 Kerberos 票证。 下面包含了关键步骤的摘要。

#### <a name="windows"></a>Windows
附带了 JDK `kinit`，可以用于获取 TGT 从密钥分发中心 (KDC) 域加入计算机与 Azure Active Directory 联合。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>步骤 1： 票证授予票证检索
- **在上运行**: Windows
- **操作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`从 KDC 获取 TGT，然后它将提示您输入您的域密码。
  - 使用`klist`若要查看可用的票证。 如果 kinit 成功，应看到来自 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票证。

> [!NOTE]
>  可能需要指定`.ini`文件具有`-Djava.security.krb5.conf`为应用程序到 KDC。

#### <a name="linux-and-mac"></a>Linux 和 Mac

##### <a name="requirements"></a>要求
访问 Windows 已加入域的计算机来查询在 Kerberos 域控制器。

##### <a name="step-1-find-kerberos-kdc"></a>步骤 1： 查找 Kerberos KDC
- **在上运行**: Windows 命令行
- **操作**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` （其中"DOMAIN.COMPANY.COM"映射到域的名称）
- **示例输出**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **若要提取的信息**DC 名称，在这种情况下 `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>步骤 2： 配置 KDC 中 krb5.conf
- **在上运行**: Linux/Mac
- **操作**： 编辑所选的编辑器中 /etc/krb5.conf。 配置下列密钥
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  然后保存 krb5.conf 文件并退出

> [!NOTE]
>  域必须在全大写形式。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>步骤 3： 测试票证授予票证检索
- **在上运行**: Linux/Mac
- **操作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`从 KDC 获取 TGT，然后它将提示您输入您的域密码。
  - 使用`klist`若要查看可用的票证。 如果 kinit 成功，应看到来自 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票证。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>使用 ActiveDirectoryPassword 身份验证模式进行连接
下面的示例演示如何使用身份验证 = ActiveDirectoryPassword 模式。

生成并运行该示例：
1.  客户端计算机上 (上，你想要运行该示例)，下载[azure activedirectory-库-用于-java 库](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项，并将其包含在 Java 生成路径
2.  找到以下代码行并服务器/数据库名称替换为你的服务器/数据库名称。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找到以下代码行和用户名称，替换为你想要为连接的 AAD 用户的名称。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

该示例以使用 ActiveDirectoryPassword 身份验证模式：
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
如果建立连接时，应作为输出中看到以下消息：
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的用户数据库必须存在和表示指定的包含的数据库用户 Azure AD 用户或组，指定 Azure AD 用户属于，必须存在于数据库，并且必须具有 CONNECT 权限 （除 Azure Active Directory服务器管理员或组）


## <a name="connecting-using-access-token"></a>使用访问令牌进行连接
应用程序/服务可以在 Azure Active Directory 中检索访问令牌，并使用它来连接到 SQL Azure 数据库。 请注意该 accessToken 只能在驱动程序管理器类中使用 getconnection （） 方法的属性参数进行设置。 它不能在连接字符串中使用。
 
下面的示例包含一个简单的 Java 应用程序连接到 Azure SQL 数据库访问基于令牌的身份验证。 然后再生成和运行示例，请执行以下步骤：
1.  在 Azure Active Directory 中创建的应用程序帐户，为你的服务。
    1. 登录 Azure 门户。
    2. 单击左侧导航栏中的 Azure Active Directory。
    3. 单击"应用注册"选项卡。
    4. 在抽屉中，单击"新建应用程序注册"。
    5. 输入 mytokentest 作为应用程序的友好名称，选择"Web 应用 /API"。
    6. 我们不需要登录 URL。 只需提供任何内容:"http://mytokentest"。
    7. 在底部单击"创建"。
    9. 仍然在 Azure 门户中，单击"设置"选项卡的应用程序，并打开"属性"选项卡。
    10. 找到"应用程序 ID"(也称为客户端 ID) 值并将其复制到某个位置，你稍后需要此配置应用程序 (例如，1846943b-ad04-4808-aa13-4702d908b5c1) 时。 请参阅以下快照。
    11. 在"密钥"部分下，通过填写名称字段，选择密钥的持续时间并保存配置 （不为空的值字段） 中创建一个密钥。 保存后，应为值字段自动填充，复制生成的值。 这是客户端密码。
    12. 在左侧面板上，单击 Azure Active Directory。 在"应用注册"下找到"终结点"选项卡。复制"OATH 2.0 令牌终结点"下的 URL，这是你 STS 的 URL。
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. 登录到 Azure SQL 服务器的用户数据库作为 Azure Active Directory 管理员以及为应用程序主体中使用 T-SQL 命令预配的包含的数据库用户。 有关详细信息，请参阅[连接到 SQL 数据库或 SQL 数据仓库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)有关如何创建 Azure Active Directory 管理员和包含的数据库用户的详细信息。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  客户端计算机上 (上，你想要运行该示例)，下载[azure activedirectory-库-用于-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)库及其依赖项，并将其包含的 Java 生成路径中。 请注意 azure activedirectory-库-用于-java 只需运行此特定示例。 该示例使用此库中的 Api 从 Azure AAD 中检索访问令牌。 如果已有一个访问令牌，则可以跳过此步骤。 请注意，还需要在以下示例中检索访问令牌中删除部分。

在以下示例中，将你的值替换为 STS URL、 客户端 ID、 客户端机密、 服务器和数据库名称。

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {

            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

如果连接成功，应作为输出中看到以下消息：
```java
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
