---
title: 在 ODBC 驱动程序中使用 Azure Active Directory |SQL Server 的 Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e60c376e0bced63241674b82d05700281a06ad3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008496"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>结合使用 Azure Active Directory 和 ODBC 驱动程序
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>用途

版本13.1 或更高版本的 Microsoft ODBC Driver for SQL Server 允许 ODBC 应用程序使用用户名/密码、Azure Active Directory 访问令牌、Azure Active SQL Azure 的 Azure Active Directory 中的联合身份连接到实例目录托管服务标识或 Windows 集成身份验证 (_仅适用于 windows 驱动程序_)。 对于 ODBC 驱动程序版本 13.1, Azure Active Directory 访问令牌身份验证仅适用于_Windows_。 ODBC 驱动程序版本17和更高版本支持在所有平台 (Windows、Linux 和 Mac) 上进行此身份验证。 Windows 的 ODBC 驱动程序版本17.1 中引入了一个新的 Azure Active Directory 具有登录 ID 的交互式身份验证。 为系统分配的标识和用户分配的标识在 ODBC 驱动程序版本17.3.1.1 中添加了一个新的 Azure Active Directory 托管服务标识身份验证方法。 所有这些都是通过使用新的 DSN 和连接字符串关键字和连接属性来实现的。

> [!NOTE]
> Linux 和 macOS 上的 ODBC 驱动程序不支持 Active Directory 联合身份验证服务。 如果你使用的是 Linux 或 macOS 客户端 Azure Active Directory 用户名/密码身份验证, 并且 Active Directory 配置包括联合服务, 则身份验证可能会失败。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新的和/或修改的 DSN 和连接字符串关键字

使用`Authentication` DSN 或连接字符串连接来控制身份验证模式时, 可以使用关键字。 在连接字符串中设置的值将覆盖 DSN 中的值 (如果已提供)。 `Authentication`设置的_预属性值_是从连接字符串和 DSN 值计算得出的值。

|“属性”|值|，则“默认”|描述|
|-|-|-|-|
|`Authentication`|(未设置)、(空字符串)、 `SqlPassword` `ActiveDirectoryIntegrated`、 `ActiveDirectoryPassword` `ActiveDirectoryInteractive`、、、`ActiveDirectoryMsi` |(未设置)|控制身份验证模式。<table><tr><th>ReplTest1<th>描述<tr><td>(未设置)<td>由其他关键字确定的身份验证模式 (现有旧连接选项。)<tr><td>(空字符串)<td>连接字符串名称重写和`Authentication`取消设置 DSN 中设置的值。<tr><td>`SqlPassword`<td>使用用户名和密码直接对 SQL Server 实例进行身份验证。<tr><td>`ActiveDirectoryPassword`<td>使用用户名和密码通过 Azure Active Directory 标识进行身份验证。<tr><td>`ActiveDirectoryIntegrated`<td>_仅限 Windows 驱动程序_。 使用集成身份验证通过 Azure Active Directory 标识进行身份验证。<tr><td>`ActiveDirectoryInteractive`<td>_仅限 Windows 驱动程序_。 使用交互式身份验证通过 Azure Active Directory 标识进行身份验证。<tr><td>`ActiveDirectoryMsi`<td>使用托管服务标识身份验证 Azure Active Directory 标识进行身份验证。 对于用户分配的标识，UID 设置为用户标识的对象 ID。</table>|
|`Encrypt`|(未设置)、`Yes``No`|(请参阅说明)|控制连接的加密。 如果 DSN 或连接字符串中`Authentication`设置的预属性值不是 "_无_", 则默认值为。 `Yes` 否则默认值为 `No`。 如果特性`SQL_COPT_SS_AUTHENTICATION`覆盖的预属性`Authentication`值, 请在 DSN 或连接字符串或连接属性中显式设置加密的值。 如果在 DSN 或连接字符串中将`Yes`值设置为, `Yes`则加密的预属性值为。|

## <a name="new-andor-modified-connection-attributes"></a>新的和/或修改的连接属性

以下连接前连接属性已引入或修改, 以支持 Azure Active Directory 身份验证。 当连接属性具有相应的连接字符串或 DSN 关键字并且进行了设置时, 将优先使用连接属性。

|Attribute|类型|值|，则“默认”|描述|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`、`SQL_AU_PASSWORD`、`SQL_AU_AD_INTEGRATED`、`SQL_AU_AD_PASSWORD`、`SQL_AU_AD_INTERACTIVE`、`SQL_AU_AD_MSI`、`SQL_AU_RESET`|(未设置)|请参阅上述`Authentication`关键字说明。 `SQL_AU_NONE`提供此参数是为了显式重写 DSN `Authentication`和/或连接字符串中的设置值, 同时`SQL_AU_RESET`在设置取消设置属性时, 允许 DSN 或连接字符串值优先使用。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|指向或`ACCESSTOKEN` NULL 的指针|NULL|如果非 null, 则指定要使用的 AzureAD 访问令牌。 `UID`指定访问令牌以及`PWD` `Trusted_Connection`、、、或`Authentication`连接字符串关键字或其等效属性是错误的。 <br> **注意:** ODBC 驱动程序版本13.1 仅支持_Windows_上的此版本。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`、`SQL_EN_ON`|(请参阅说明)|控制连接的加密。 `SQL_EN_OFF`并`SQL_EN_ON`分别禁用和启用加密。 如果`Authentication`设置的预属性值不是 "_无_" 或`SQL_COPT_SS_ACCESS_TOKEN` "已设置", 并且`Encrypt`没有在 DSN 或连接字符串中指定, 则默认值为`SQL_EN_ON`。 否则默认值为 `SQL_EN_OFF`。 如果连接属性`SQL_COPT_SS_AUTHENTICATION`设置为 "不是_无_", 则`SQL_COPT_SS_ENCRYPT`在 DSN 或连接字符串中未指定时, 显式设置为所需的值。 `Encrypt` 此属性的有效值控制[是否将加密用于连接。](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Azure Active Directory 不支持, 因为无法通过 ODBC 连接来完成对 AAD 主体的密码更改。 <br><br>在 SQL Server 2005 中引入了 SQL Server 身份验证密码过期功能。 添加`SQL_COPT_SS_OLDPWD`了属性, 以允许客户端同时为连接提供旧密码和新密码。 设置此属性时，访问接口对于第一次连接或后续连接将不使用连接池，因为连接字符串将包含现在已更改的“旧密码”。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`、`SQL_IS_ON`|`SQL_IS_OFF`|_弃用_;改用`SQL_COPT_SS_AUTHENTICATION`设置为`SQL_AU_AD_INTEGRATED` 。 <br><br>强制使用 Windows 身份验证 (Linux 和 macOS 上的 Kerberos) 进行服务器登录访问验证。 使用 Windows 身份验证时, 驱动程序将忽略作为、 `SQLConnect` `SQLDriverConnect`或`SQLBrowseConnect`处理的一部分提供的用户标识符和密码值。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory（仅 Windows 驱动程序）的 UI 新增功能

驱动程序的 DSN 设置和连接 Ui 已使用 Azure AD 的身份验证所需的其他选项进行了增强。

### <a name="creating-and-editing-dsns-in-the-ui"></a>在 UI 中创建和编辑 Dsn

使用驱动程序的安装程序 UI 创建或编辑现有 DSN 时, 可以使用新的 Azure AD 身份验证选项:

`Authentication=ActiveDirectoryIntegrated` 用于向 SQL Azure 执行 Azure Active Directory 集成身份验证

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`对于 Azure Active Directory 用户名/密码身份验证 SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` 用于针对 SQL Azure 的 Azure Active Directory 交互式身份验证

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`要 SQL Server 的用户名/密码身份验证 (Azure 或其他)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`对于 Windows 旧 SSPI 集成身份验证

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

这五个选项分别`Trusted_Connection=Yes`对应于 (现有旧版 Windows SSPI 集成身份验证`ActiveDirectoryPassword` `SqlPassword` `Authentication=` `ActiveDirectoryIntegrated`)、、、和`ActiveDirectoryInteractive`。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示 (仅 Windows 驱动程序)

SQLDriverConnect 在请求完成连接所需的信息时显示的提示对话框包含三个用于 Azure AD 身份验证的新选项:

![ServerLogin.png](windows/ServerLogin.png)

这些选项对应于上面 DSN 安装程序 UI 中的五个可用选项。

### <a name="example-connection-strings"></a>连接字符串示例
1. SQL Server Authentication-旧语法。 服务器证书未经过验证, 并且仅当服务器强制执行加密时才使用它。 用户名/密码在连接字符串中传递。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 身份验证-新语法。 客户端请求加密 (的默认`Encrypt`值为`true`), 并验证服务器证书, 而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 用户名/密码在连接字符串中传递。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Windows 集成身份验证 (Linux 和 macOS 上的 Kerberos 和 SQL Server)-当前语法。 除非使用加密, 否则不会验证服务器证书。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_仅适用于 Windows 驱动程序_。)使用 SSPI 集成的 Windows 身份验证 (如果目标数据库位于 SQL Server 或 SQL IaaS 中)-新语法。 客户端请求加密 (的默认`Encrypt`值为`true`), 并验证服务器证书, 而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 用户名/密码身份验证 (如果目标数据库在 Azure SQL DB 中)。 无论加密设置如何, 都会验证服务器证书 (除非`TrustServerCertificate`设置为`true`)。 用户名/密码在连接字符串中传递。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_仅适用于 Windows 驱动程序_。)使用 ADAL 进行集成的 Windows 身份验证, 它涉及兑换的 Windows 帐户凭据, 适用于 AAD 颁发的访问令牌, 假定目标数据库在 Azure SQL 数据库中。 无论加密设置如何, 都会验证服务器证书 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_仅适用于 Windows 驱动程序_。)AAD 交互身份验证使用 Azure 多重身份验证技术来设置连接。 在此模式下, 通过提供登录 ID, 将触发 Windows Azure 身份验证对话框, 并允许用户输入密码来完成连接。 用户名在连接字符串中传递。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. AAD 托管服务标识 Authentication 使用系统分配的身份验证或用户分配的标识进行身份验证, 以设置连接。 对于用户分配的标识，UID 设置为用户标识的对象 ID。<br>
对于系统分配的标识，<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
对于用户分配的标识, 对象 ID 等于 myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- 将新 Active Directory 选项与 Windows ODBC 驱动程序一起使用时, 请确保已安装[SQL Server 的 Active Directory 身份验证库](https://go.microsoft.com/fwlink/?LinkID=513072)。 使用 Linux 和 macOS 驱动程序时, 请确保`libcurl`已安装。 对于驱动程序版本17.2 及更高版本, 这不是显式依赖项, 因为其他身份验证方法或 ODBC 操作不需要该依赖项。
>- 若要使用 SQL Server 帐户用户名和密码进行连接, 你现在可以使用 " `SqlPassword`新建" 选项, 因为此选项可启用更安全的连接默认值, 因此尤其适用于 SQL Azure。
>- 若要使用 Azure Active Directory 帐户的用户名和密码进行连接`Authentication=ActiveDirectoryPassword` , 请分别使用用户名和`UID`密码`PWD`在连接字符串中指定和和关键字。
>- 若要使用 Windows 集成或 Active Directory 集成 (仅 windows 驱动程序) 身份验证`Authentication=ActiveDirectoryIntegrated`进行连接, 请在连接字符串中指定。 驱动程序将自动选择正确的身份验证模式。 `UID`不得`PWD`指定和。
>- 若要使用 Active Directory Interactive (仅 Windows 驱动程序) 身份`UID`验证进行连接, 则必须指定。

## <a name="authenticating-with-an-access-token"></a>使用访问令牌进行身份验证

通过`SQL_COPT_SS_ACCESS_TOKEN`预连接属性, 可以使用从 Azure AD 获取的访问令牌来进行身份验证, 而不是使用用户名和密码, 也不会绕过驱动程序协商和获取访问令牌。 若要使用访问令牌, 请将`SQL_COPT_SS_ACCESS_TOKEN`连接属性设置为指向`ACCESSTOKEN`结构的指针:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

是一个可变长度的结构, 它由4字节_长度_后跟构成访问令牌的不透明数据的长度字节组成。  `ACCESSTOKEN` 由于 SQL Server 如何处理访问令牌, 因此必须展开通过[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 响应获取的令牌, 以便每个字节后跟0个填充字节, 类似于仅包含 ASCII 字符的 UCS-2 字符串;但是, 标记是一个不透明的值, 并且指定的长度 (以字节为单位) 不得包含任何 null 终止符。 由于其长度和格式限制, 此身份验证方法仅以编程方式通过`SQL_COPT_SS_ACCESS_TOKEN`连接属性提供; 没有相应的 DSN 或连接字符串关键字。 连接字符串不能`UID`包含、 `PWD`、 `Authentication`或`Trusted_Connection`关键字。

> [!NOTE]
> ODBC 驱动程序版本13.1 仅支持_Windows_上的此身份验证。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 身份验证示例代码

下面的示例演示了使用 Azure Active Directory 与连接关键字连接到 SQL Server 所需的代码。 请注意, 不需要更改应用程序代码本身;使用 AAD 进行身份验证所需的唯一修改是连接字符串或 DSN (如果使用)。
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下面的示例演示了使用 Azure Active Directory 与访问令牌身份验证连接到 SQL Server 所需的代码。 在这种情况下, 需要修改应用程序代码以处理访问令牌并设置关联的连接属性。
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
下面是一个用于 Azure Active Directory 交互式身份验证的连接字符串示例。 请注意, 它不包含 PWD 字段, 因为将使用 Windows Azure 身份验证屏幕输入密码。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
下面是一个示例连接字符串, 用于 Azure Active Directory 托管服务标识身份验证。 请注意，对于用户分配的标识，UID 设置为用户标识的对象 ID。
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>另请参阅
[使用 Azure AD auth 的 Azure SQL DB 的基于令牌的身份验证支持](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

