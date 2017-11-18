---
title: "使用 Azure Active Directory 身份验证进行连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83d5ad3bae131b58dd344c3f5f9bfc7f5d0c4f5a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接
本文提供有关如何开发 Java 应用程序以使用用于 SQL Server 的 Microsoft JDBC Driver 6.0 （或更高版本） 的 Azure Active Directory 身份验证功能的信息。

适用于 SQL Server 开始与 Microsoft JDBC Driver 6.0，你可以使用 Azure Active Direcoty (AAD) 身份验证这是连接到 Azure SQL 数据库 v12 的一种机制使用 Azure Active Directory 中的标识。 使用 Azure Active Directory 身份验证来集中管理标识的数据库用户和作为 SQL Server 身份验证的替代方法。 JDBC Driver 6.0 （或更高版本），可在要连接到 Azure SQL DB 的 JDBC 连接字符串中指定你的 Azure Active Directory 凭据。 有关如何配置 Azure Active Directory 身份验证信息，请访问[连接到 SQL 数据库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

添加了两个新的连接属性，以支持 Azure Active Directory 身份验证：
*   **身份验证**： 此属性用于指示要用于连接的 SQL 身份验证方法。 可能的值为： **ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**和默认**NotSpecified**.
    * 使用身份验证 = ActiveDirectoryIntegrated 连接到使用集成的 Windows 身份验证的 SQL 数据库。 若要使用此身份验证模式需要联合本地 Active Directory 联合身份验证服务 (ADFS) 与 Azure AD 在云中。 此功能后安装程序，可以访问 Azure SQL DB，而当加入域的计算机登录时提示输入 ceredentials。 
    * 使用身份验证 = ActiveDirectoryPassword 连接到 SQL 数据库使用 Azure AD 主体名称和密码。
    * 使用身份验证 = SqlPassword 连接到 SQL Server 使用用户名/用户和密码属性。
    * 使用身份验证 = NotSpecified 或将其保留为默认值，如果没有一个的这些身份验证方法需要。

*   **accessToken**： 使用此属性来连接到 SQL 数据库使用访问令牌。 仅可以在驱动程序管理器类使用 getConnection() 方法的属性参数设置 accessToken。 它不能在连接 URL。  

有关详细信息，请参阅上的身份验证属性[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)页。  


## <a name="client-setup-requirements"></a>客户端安装程序要求
请确保在客户端计算机上安装了以下组件：
* Java 7 或更高版本
*   6.2 （或更高版本） 的 Microsoft JDBC Driver for SQL Server
*   如果你使用的访问令牌的基于身份验证模式，你将需要[azure activedirectory-库-为-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)和其依赖项，以从这篇文章中运行这些示例。 请参阅**连接使用访问令牌**有关详细信息部分。
*   如果你正在使用 ActiveDirectoryPassword 身份验证模式将需要[azure activedirectory-库-为-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项。 请参阅**使用 ActiveDirectoryPassword 身份验证模式进行连接**有关详细信息部分。
*   如果使用 ActiveDirectoryIntegrated 模式，你将需要安装 Active Directory Authentication Library for SQL Server (ADALSQL。DLL) 和 sqljdbc_auth.dll。
    * ADALSQL。DLL 使应用程序向 Microsoft Azure SQL 数据库使用 Azure Active Directory 进行身份验证。 下载的 DLL[适用于 Microsoft SQL Server 的 Microsoft Active Directory 身份验证库](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * 有关 ADALSQL。DLL 两个的二进制版本 X86 和 X64 可供下载。 如果安装了错误的二进制版本或者缺少 DLL 时，该驱动程序将引发以下错误:"无法加载 adalsql.dll (身份验证 =...)。 错误代码： 0x2。"。 在此情况下下载 ADALSQL 正确版本。DLL。 
    * sqljdbc_auth.dll 是可用的驱动程序包中。 Sqljdbc_auth.dll 文件复制到装有 JDBC 驱动程序的计算机上的 Windows 系统路径上的目录。 也可以设置 java.libary.path 系统属性以指定 sqljdbc_auth.dll 的目录。 
    * 如果您在 x64 处理器上运行 64 位 JVM，则使用 x64 文件夹中的 sqljdbc_auth.dll 文件。 
    * 如果您运行 32 位的 Java 虚拟机 (JVM)，则使用 x86 文件夹中的 sqljdbc_auth.dll 文件，即使操作系统是 x64 版本也不例外。 
    * 例如，如果你使用的 32 位 JVM 和 JDBC 驱动程序安装在默认目录，你可以通过使用以下虚拟机 (VM) 参数启动 Java 应用程序时指定的 DLL 的位置：  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>使用 ActiveDirectoryIntegrated 身份验证模式进行连接
下面的示例演示如何使用身份验证 = ActiveDirectoryIntegrated 模式。 在加入域的计算机，与 Azure Active Directory 联合上运行此示例。 表示你的 Azure AD 主体，或某个组的包含的数据库用户，你属于数据库中必须存在，必须具有 CONNECT 权限。 
    
在执行该示例之前替换你的服务器/数据库名称，将以下行中的服务器/数据库名称：

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

该示例以使用 ActiveDirectoryIntegrated 身份验证模式：
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
加入到与 Azure Active Directory 联合的域的计算机上运行此示例将自动使用您的 Windows 凭据并且没有密码是必需的。 如果建立连接时，你将看到以下消息：
```
You have successfully logged on as: <your domain user name>
```

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>使用 ActiveDirectoryPassword 身份验证模式进行连接
下面的示例演示如何使用身份验证 = ActiveDirectoryPassword 模式。

生成并运行该示例：
1.  客户端计算机上 (上，你想要运行该示例)，下载[azure activedirectory-库-为-java 库](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项，并将它们包含的 Java 生成路径中
2.  找到以下代码行并将服务器/数据库名称替换为你的服务器/数据库名称。
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找到以下代码行并将用户名称替换为你想要作为连接的 Azure AD 用户的名称。
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

该示例以使用 ActiveDirectoryPassword 身份验证模式：
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
如果建立连接时，你将作为输出中看到以下消息：
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的用户数据库必须存在并且包含的数据库用户表示指定 Azure AD 用户或组，指定 Azure AD 用户所属的数据库中必须存在，并且必须具有 CONNECT 权限 （除 Azure Active Directory服务器管理员或组）


## <a name="connecting-using-access-token"></a>使用访问令牌进行连接
应用程序/服务可以在 Azure Active Directory 中检索访问令牌，并使用它连接到 SQL Azure 数据库。 请注意该 accessToken 只能在驱动程序管理器类使用 getConnection() 方法的属性参数进行设置。 它不能在连接字符串。
 
下面的示例包含一个简单的 Java 应用程序连接到 Azure SQL 数据库使用访问令牌基于身份验证。 在生成和运行示例之前, 执行以下步骤：
1.  为你的服务，在 Azure Active Directory 中创建的应用程序帐户。
    1. 登录到 Azure 管理门户
    2. 在左侧导航窗格中单击 Azure Active Directory
    3. 单击你要在其中注册示例应用程序的目录租户。 这必须是与你的数据库 （承载你的数据库的服务器） 相关联的相同目录。
    4. 单击应用程序选项卡。
    5. 在抽屉中，单击添加。
    6. 单击"添加我的组织正在开发的应用程序"。
    7. 输入 mytokentest 作为应用程序的友好名称，选择"Web 应用程序和/或 Web API"，然后单击下一步。
    8. 假设此应用程序为后台程序/服务并且不是 web 应用程序，它不具有登录 URL 或应用程序 ID URI。 对于这两个字段，输入 http://mytokentest
    9. 仍然在 Azure 门户中，单击你的应用程序的配置选项卡
    10. 找到客户端 ID 值并将其复制到某个位置，你将需要此更高版本 （即配置你的应用程序时 a4bbfe26-dbaa-4fec-8ef5-223d229f647d)。 请参阅下面的快照。
    11. 在"密钥"部分中，选择密钥的持续时间，保存配置，并复制以供将来使用的密钥。 这是客户端机密。
    12. 在底部，单击"查看终结点"，并复制"OAUTH 2.0 授权终结点"下的 URL 以供将来使用。 这是 STS URL。


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. 登录到你的 Azure SQL 服务器的用户数据库作为 Azure Active Directory 管理员以及使用适用于你的应用程序主体 T-SQL 命令设置包含的数据库用户。 请参阅[连接到 SQL 数据库或 SQL 数据仓库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)有关如何创建 Azure Active Directory 管理员和包含的数据库用户的详细信息。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  客户端计算机上 (上，你想要运行该示例)，下载[azure activedirectory-库-为-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)库及其依赖项，并将它们包含的 Java 生成路径中。 请注意 azure activedirectory-库-为-java 只需运行此特定示例，因为它使用通过此库 Api 从 Azure AD 检索访问令牌。 如果你没有访问令牌，则可以跳过此步骤。 请注意，将需要在以下示例中检索访问令牌中删除部分。

在下面的示例中，STS 的 URL，客户端 ID、 客户端机密、 服务器和数据库名称与你的值的替换。

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

如果成功连接，则将作为输出中看到以下消息：
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 

