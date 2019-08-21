---
title: 使用 Azure Active Directory 身份验证进行连接 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028124"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍了如何开发 Java 应用程序以将 Azure Active Directory authentication 功能与用于 SQL Server 的 Microsoft JDBC 驱动程序配合使用。

可以使用 Azure Active Directory (AAD) 身份验证, 这种身份验证是一种使用 Azure Active Directory 中的标识连接到 Azure SQL 数据库 v12 的机制。 使用 Azure Active Directory 身份验证以集中管理数据库用户的标识且作为 SQL Server 身份验证的一种替代方法使用。 JDBC Driver 允许您在 JDBC 连接字符串中指定 Azure Active Directory 凭据以连接到 Azure SQL DB。 有关如何配置 Azure Active Directory 身份验证的信息, 请参阅[使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

用于在 SQL Server 的 Microsoft JDBC 驱动程序中支持 Azure Active Directory 身份验证的连接属性包括:
*   身份验证使用此属性以指示要用于连接的 SQL 身份验证方法  。 可能的值有： 
    * **ActiveDirectoryMSI**
        * 由于驱动程序版本**7.2**所支持`authentication=ActiveDirectoryMSI` , 可用于从启用 "标识" 支持的 azure 资源内部连接到 azure SQL 数据库/数据仓库。 另外, 还可以在 "连接/数据源" 属性以及此身份验证模式下指定**msiClientId** , 此身份验证模式必须包含用于获取用于建立**accessToken**的托管服务标识的客户端 ID连接。
    * **ActiveDirectoryIntegrated**
        * 由于驱动程序版本**6.0**所支持`authentication=ActiveDirectoryIntegrated` , 可用于使用集成身份验证连接到 Azure SQL 数据库/数据仓库。 若要使用此身份验证模式, 需要将本地 Active Directory 联合身份验证服务 (ADFS) 与云中的 Azure Active Directory 联合。 设置后, 可以通过将本机库 "sqljdbc_auth" 添加到 Windows 操作系统上的应用程序类路径, 或者为跨平台身份验证支持设置 Kerberos 票证来进行连接。 登录到已加入域的计算机时, 你将能够访问 Azure SQL DB/DW, 而不会提示输入凭据。
    * **ActiveDirectoryPassword**
        * 由于驱动程序版本**6.0**所支持`authentication=ActiveDirectoryPassword` , 可以使用 Azure AD 主体名称和密码来连接到 Azure SQL 数据库/数据仓库。
    * **SqlPassword**
        * 使用`authentication=SqlPassword` "用户名"/"用户" 和 "密码" 属性连接到 SQL Server。
    * **NotSpecified**
        * 如果`authentication=NotSpecified`不需要这些身份验证方法, 则使用或将其保留为默认值。

*   **accessToken**: 使用此连接属性可以使用访问令牌连接到 SQL 数据库。 只能使用 DriverManager 类中的 getConnection () 方法的 Properties 参数来设置 accessToken。 它不能在连接 URL 中使用。  

有关详细信息, 请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)页上的 "身份验证" 属性。  


## <a name="client-setup-requirements"></a>客户端安装要求
对于**ActiveDirectoryMSI** authentication, 以下组件必须安装在客户端计算机上:
* Java 8 或更高版本
* Microsoft JDBC Driver 7.2 (或更高版本) SQL Server
* 客户端环境必须是 Azure 资源, 并且必须启用 "标识" 功能支持。
* 一个包含的数据库用户, 该用户表示 Azure 资源的系统分配的托管标识或用户分配的托管标识, 或者您的 MSI 所属的某个组, 必须存在于目标数据库中, 并且必须具有 CONNECT 权限。

对于其他身份验证模式, 以下组件必须安装在客户端计算机上:
* Java 7 或更高版本
* Microsoft JDBC Driver 6.0 (或更高版本) SQL Server
* 如果你使用的是基于访问令牌的身份验证模式, 则需要使用[azure activedirectory 库的 java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其依赖项来运行本文中的示例。 有关详细信息, 请参阅**使用访问令牌进行连接**一节。
* 如果使用的是**ActiveDirectoryPassword** authentication 模式, 则需要用于 java 及其依赖项的[azure activedirectory 库](https://github.com/AzureAD/azure-activedirectory-library-for-java)。 有关详细信息, 请参阅**使用 ActiveDirectoryPassword authentication 模式进行连接**一节。
* 如果你使用的是**ActiveDirectoryIntegrated**模式, 则需要用于 java 及其依赖项的 azure activedirectory 库。 有关详细信息, 请参阅**使用 ActiveDirectoryIntegrated Authentication 模式进行连接**一节。

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>使用 ActiveDirectoryMSI 身份验证模式进行连接
下面的示例展示了如何使用 `authentication=ActiveDirectoryMSI` 模式。 从 Azure 资源、e、g、Azure 虚拟机、应用服务或与 Azure Active Directory 联合的 Function App 中运行此示例。

执行示例之前, 请将服务器/数据库名称替换为以下行中的服务器/数据库名称:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

使用 ActiveDirectoryMSI 身份验证模式的示例:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

在 Azure 虚拟机上运行此示例时, 将从_系统分配的托管_标识或_用户分配的托管标识_(如果指定了**msiClientId** ) 中提取访问令牌, 并使用获取的访问权限建立连接令牌. 如果建立了连接, 则应看到以下消息:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>使用 ActiveDirectoryIntegrated 身份验证模式进行连接
使用版本 6.4, Microsoft JDBC Driver 添加了对在多个平台 (Windows、Linux 和 macOS) 上使用 Kerberos 票证进行 ActiveDirectoryIntegrated Authentication 的支持。
有关详细信息, 请参阅[在 Windows、Linux 和 Mac 上设置 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)了解更多详细信息。 或者, 在 Windows 上, sqljdbc_auth 也可用于通过 JDBC 驱动程序进行 ActiveDirectoryIntegrated 身份验证。

> [!NOTE]
>  如果你使用的是较旧版本的驱动程序, 请在此[链接](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)中查看使用此身份验证模式所需的相应依赖项。 

下面的示例展示了如何使用 `authentication=ActiveDirectoryIntegrated` 模式。 在与 Azure Active Directory 联合的已加入域的计算机上运行此示例。 表示 Azure AD 主体的包含数据库用户或所属的某个组必须存在于数据库中, 并且必须具有 CONNECT 权限。 

在生成并运行该示例之前, 请在客户端计算机上 (要在其上运行此示例), 下载[适用于 azure 的 azure activedirectory](https://github.com/AzureAD/azure-activedirectory-library-for-java)库及其依赖项, 并将它们包含在 java 生成路径中

执行示例之前, 请将服务器/数据库名称替换为以下行中的服务器/数据库名称:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

使用 ActiveDirectoryIntegrated 身份验证模式的示例:
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

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

在客户端计算机上运行此示例将自动使用您的 Kerberos 票证, 无需密码。 如果建立了连接, 则应看到以下消息:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>在 Windows、Linux 和 Mac 上设置 Kerberos 票证

需要设置一个 Kerberos 票证, 将当前用户链接到 Windows 域帐户。 下面包含关键步骤的摘要。

#### <a name="windows"></a>Windows
JDK 附带了`kinit`, 可用于从与 Azure Active Directory 联合的已加入域的计算机上密钥发行中心 (KDC) 获取 TGT。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>步骤 1: 票证授予票证检索
- **运行于**: Windows
- **操作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`从 KDC 获取 TGT, 然后它会提示你输入域密码。
  - 使用`klist`查看可用的票证。 如果 kinit 成功, 应会看到 krbtgt/DOMAIN. .COM @ DOMAIN.COMPANY.COM 中的票证。

> [!NOTE]
>  你可能需要为应用程序`.ini`指定一个`-Djava.security.krb5.conf`文件, 以便查找 KDC。

#### <a name="linux-and-mac"></a>Linux 和 Mac

##### <a name="requirements"></a>要求
访问 Windows 域加入计算机，以查询 Kerberos 域控制器。

##### <a name="step-1-find-kerberos-kdc"></a>步骤 1: 查找 Kerberos KDC
- 运行于Windows 命令行 
- **操作**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (其中 "DOMAIN.COMPANY.COM" 映射到你的域的名称)
- **示例输出**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **要提取的信息**DC 名称, 在本例中为`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>步骤 2: 在 krb5.conf 中配置 KDC
- **运行于**: Linux/Mac
- **操作**: 在所选编辑器中编辑/etc/krb5.conf。 配置下列密钥
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
>  域必须全部大写。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>第 3 步：测试票证授予票证检索
- **运行于**: Linux/Mac
- **操作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`从 KDC 获取 TGT, 然后它会提示你输入域密码。
  - 使用`klist`查看可用的票证。 如果 kinit 成功, 应会看到 krbtgt/DOMAIN. .COM @ DOMAIN.COMPANY.COM 中的票证。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>使用 ActiveDirectoryPassword 身份验证模式进行连接
下面的示例展示了如何使用 `authentication=ActiveDirectoryPassword` 模式。

生成并运行该示例之前:
1.  在客户端计算机上 (要在其上运行此示例), 下载适用于[azure 的 azure activedirectory](https://github.com/AzureAD/azure-activedirectory-library-for-java)库及其依赖项, 并将它们包含在 java 生成路径中
2.  找到以下代码行, 并将服务器/数据库名称替换为你的服务器/数据库名称。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找到以下代码行, 并将用户名替换为要连接的 AAD 用户的名称。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

使用 ActiveDirectoryPassword 身份验证模式的示例:
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
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
如果建立了连接, 则应看到以下消息作为输出:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 必须存在包含的用户数据库, 并且包含的数据库用户 (表示指定的 Azure AD 用户或某个组、指定的 Azure AD 用户所属) 必须存在于数据库中, 并且必须具有 CONNECT 权限 (Azure Active Directory 除外服务器管理员或组)

## <a name="connecting-using-access-token"></a>使用访问令牌进行连接
应用程序/服务可以从 Azure Active Directory 检索访问令牌, 并使用它连接到 Azure SQL 数据库/数据仓库。

> [!NOTE] 
> 只能使用 DriverManager 类中的 getConnection () 方法的 Properties 参数来设置**accessToken** 。 不能在连接字符串中使用它。

以下示例包含一个简单的 Java 应用程序, 该应用程序使用基于访问令牌的身份验证连接到 Azure SQL 数据库/数据仓库。 在生成并运行该示例之前, 请执行以下步骤:
1.  在服务的 Azure Active Directory 中创建应用程序帐户。
    1. 登录 Azure 门户。
    2. 单击左侧导航栏中的 "Azure Active Directory"。
    3. 单击 "应用注册" 选项卡。
    4. 在抽屉中, 单击 "新建应用程序注册"。
    5. 输入 mytokentest 作为应用程序的友好名称, 然后选择 "Web 应用/API"。
    6. 我们不需要登录 URL。 只需提供任何内容: "https://mytokentest" 。
    7. 单击底部的 "创建"。
    9. 在 Azure 门户中, 单击应用程序的 "设置" 选项卡, 然后打开 "属性" 选项卡。
    10. 找到 "应用程序 ID" (也称为 "客户端 ID") 值并将其复制, 稍后在配置应用程序时需要此值 (例如, 1846943b-ad04-4808-aa13-4702d908b5c1)。 请参阅以下快照。
    11. 在 "键" 部分下, 通过填写 "名称" 字段, 选择密钥的持续时间, 并保存配置 (将 "值" 字段留空) 来创建一个密钥。 保存后, 应自动填充值字段, 复制生成的值。 这是客户端密码。
    12. 单击左侧面板上的 "Azure Active Directory"。 在 "应用注册" 下, 找到 "终结点" 选项卡。复制 "OATH 2.0 令牌终结点" 下的 URL, 这是 STS URL。
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. 以 Azure Active Directory 管理员身份登录到 Azure SQL Server 的用户数据库, 并使用 T-sql 命令为你的应用程序主体预配包含的数据库用户。 有关详细信息, 请参阅[使用 Azure Active Directory 身份验证连接到 Sql 数据库或 Sql 数据仓库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。有关如何创建 Azure Active Directory 管理员和包含的数据库用户的详细信息, 请参阅连接到 sql 数据库或 Sql 数据仓库。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  在客户端计算机 (在其上, 你要运行此示例) 中, 下载[适用于 azure 的 azure activedirectory](https://github.com/AzureAD/azure-activedirectory-library-for-java)库及其依赖项, 并将它们包含在 java 生成路径中。 请注意, 只有在运行此特定示例时, 才需要用于 java 的 azure activedirectory 库。 该示例使用此库中的 Api 从 Azure AAD 检索访问令牌。 如果已有访问令牌, 则可以跳过此步骤。 请注意, 还需要删除示例中检索访问令牌的部分。

在下面的示例中, 将 STS URL、客户端 ID、客户端密钥、服务器和数据库名称替换为你的值。

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

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

如果连接成功, 则会看到以下消息作为输出:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
