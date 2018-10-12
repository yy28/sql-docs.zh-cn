---
title: 使用 Azure Active Directory 与 ODBC 驱动程序 |适用于 SQL Server 的 Microsoft 文档
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7486e97fb0efe9fffa9fe6eb49ee75cc6d75bfce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634993"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>结合使用 Azure Active Directory 和 ODBC 驱动程序
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>用途

Microsoft ODBC Driver for SQL Server 使用版本 13.1 或更高版本允许 ODBC 应用程序连接到 SQL Azure 的实例使用 Azure Active Directory 中的联合身份标识，使用用户名/密码、 Azure Active Directory 访问令牌或 Windows集成身份验证 (_Windows 驱动程序_)。 ODBC 驱动程序版本 13.1，令牌身份验证的 Azure Active Directory 访问权限_仅 Windows_。 ODBC 驱动程序版本 17 和上面跨所有平台 （Windows、 Linux 和 Mac） 支持此身份验证。 为 Windows，如果在 ODBC 驱动程序版本 17.1 中引入的新 Azure Active Directory 交互式身份验证使用的登录 ID。 所有这些都是通过使用新 DSN 和连接字符串关键字和连接属性完成。

> [!NOTE]
> 在 Linux 和 macOS 上 ODBC 驱动程序不支持 Active Directory 联合身份验证服务。 如果使用 Azure Active Directory 用户名/密码身份验证从 Linux 或 macOS 客户端和 Active Directory 配置包括联合身份验证服务，可能会失败身份验证。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新的和/或修改后的 DSN 和连接字符串关键字

`Authentication`关键字可用于使用 DSN 或连接字符串进行连接时控制身份验证模式。 在连接字符串中设置的值覆盖，在 DSN 中，如果提供。 _预先属性值_的`Authentication`设置为从连接字符串和 DSN 值计算的值。

|名称|值|默认|描述|
|-|-|-|-|
|`Authentication`|（未设置），（空字符串）、 `SqlPassword`， `ActiveDirectoryPassword`， `ActiveDirectoryIntegrated`， `ActiveDirectoryInteractive`|(未设置)|控制身份验证模式。<table><tr><th>ReplTest1<th>描述<tr><td>(未设置)<td>身份验证模式由其他关键字 （现有旧的连接选项。）<tr><td>(空字符串)<td>连接字符串为“{0}”重写和取消设置`Authentication`值在 DSN 中的设置。<tr><td>`SqlPassword`<td>直接进行身份验证使用的用户名和密码的 SQL Server 实例。<tr><td>`ActiveDirectoryPassword`<td>使用 Azure Active Directory 标识使用用户名和密码进行身份验证。<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 驱动程序_。 使用 Azure Active Directory 标识使用集成身份验证进行身份验证。<tr><td>`ActiveDirectoryInteractive`<td>_Windows 驱动程序_。 使用 Azure Active Directory 标识使用交互式身份验证进行身份验证。</table>|
|`Encrypt`|(未设置)、`Yes``No`|（请参见说明）|控制连接的加密。 如果预属性值`Authentication`设置不是_无_，默认值是`Yes`。 否则默认值为 `No`。 加密的预属性值是`Yes`的值设置为如果`Yes`的 DSN 或连接字符串中。|

## <a name="new-andor-modified-connection-attributes"></a>新的和/或修改连接属性

以下预连接属性已引入或修改，以支持 Azure Active Directory 身份验证的连接。 当连接属性都有相应的连接字符串或 DSN 关键字，并且设置时，连接属性优先。

|Attribute|类型|值|默认|描述|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`、`SQL_AU_PASSWORD`、`SQL_AU_AD_INTEGRATED`、`SQL_AU_AD_PASSWORD`、`SQL_AU_AD_INTERACTIVE`、`SQL_AU_RESET`|(未设置)|请参阅说明`Authentication`关键字更高版本。 `SQL_AU_NONE` 若要显式重写一组提供`Authentication`值在 DSN 和/或连接字符串中，虽然`SQL_AU_RESET`取消设置该属性，如果它已设置，从而允许为具有更高优先级的 DSN 或连接字符串值。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|指向`ACCESSTOKEN`或为 NULL|NULL|如果非 null，指定 azure Ad 访问令牌来使用。 它是指定的访问令牌，也`UID`， `PWD`， `Trusted_Connection`，或`Authentication`连接字符串关键字或其等效的属性。 <br> **注意：** ODBC 驱动程序版本 13.1 才支持此上_Windows_。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`、`SQL_EN_ON`|（请参见说明）|控制连接的加密。 `SQL_EN_OFF` 和`SQL_EN_ON`禁用和启用加密，分别。 如果预属性值`Authentication`设置不是_无_或`SQL_COPT_SS_ACCESS_TOKEN`设置，并`Encrypt`未指定的 DSN 或连接字符串中的默认值是`SQL_EN_ON`。 否则默认值为 `SQL_EN_OFF`。 此属性控制的有效值[是否将使用加密连接。](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|不支持与 Azure Active Directory，因为无法通过 ODBC 连接完成对 AAD 主体的密码更改。 <br><br>在 SQL Server 2005 中引入了 SQL Server 身份验证密码过期功能。 `SQL_COPT_SS_OLDPWD`添加了属性，以允许客户端提供连接旧和新密码。 设置此属性时，访问接口对于第一次连接或后续连接将不使用连接池，因为连接字符串将包含现在已更改的“旧密码”。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`、`SQL_IS_ON`|`SQL_IS_OFF`|_已弃用_; 使用`SQL_COPT_SS_AUTHENTICATION`设置为`SQL_AU_AD_INTEGRATED`相反。 <br><br>强制使用 Windows 身份验证 (Kerberos Linux 和 macOS 上) 的服务器登录名访问验证。 使用 Windows 身份验证时，该驱动程序将忽略作为的一部分提供的用户标识符和密码值`SQLConnect`， `SQLDriverConnect`，或`SQLBrowseConnect`处理。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory（仅 Windows 驱动程序）的 UI 新增功能

DSN 设置和连接 Ui 的驱动程序已得到增强和其他选项使用与 Azure AD 身份验证所必需的。

### <a name="creating-and-editing-dsns-in-the-ui"></a>创建和编辑 UI 中的 Dsn

此外，可以使用新的 Azure AD 身份验证选项时创建或编辑现有 DSN 使用驱动程序的安装程序 UI:

`Authentication=ActiveDirectoryIntegrated` SQL Azure 到 Azure Active Directory 集成身份验证

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` SQL Azure 到 Azure Active Directory 用户名/密码身份验证

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` 用于针对 SQL Azure 的 Azure Active Directory 交互式身份验证

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` 到 SQL Server 的用户名/密码身份验证 （Azure 或其他方式）

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` 对于 Windows 旧 SSPI 集成身份验证

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

五个选项对应于`Trusted_Connection=Yes`(现有旧 Windows SSPI 仅集成的身份验证) 和`Authentication=` `ActiveDirectoryIntegrated`， `SqlPassword`， `ActiveDirectoryPassword`，并`ActiveDirectoryInteractive`分别。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示符 （仅 Windows 驱动程序）

SQLDriverConnect 请求以完成连接所需的信息时显示提示对话框包含三个 Azure AD 身份验证的新选项：

![ServerLogin.png](windows/ServerLogin.png)

这些选项对应于相同的五个 DSN 设置 UI 更高版本中可用。

### <a name="example-connection-strings"></a>连接字符串示例
1. SQL Server 身份验证 – 旧语法。 不验证服务器证书，并且仅当服务器强制实施它使用加密。 在连接字符串中传递用户名/密码。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 身份验证 – 新的语法。 客户端请求加密 (默认值`Encrypt`是`true`) 和服务器证书获取已验证，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 在连接字符串中传递用户名/密码。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 集成 Windows 身份验证 (Kerberos Linux 和 macOS 上) 使用 SSPI （到 SQL Server 或 SQL IaaS） – 当前的语法。 不验证服务器证书，除非使用加密。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 驱动程序_。)集成 Windows 身份验证使用 SSPI （如果目标数据库位于 SQL Server 或 SQL IaaS） – 新语法。 客户端请求加密 (默认值`Encrypt`是`true`) 和服务器证书获取已验证，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 用户名/密码身份验证 （如果目标数据库是在 Azure SQL 数据库）。 获取验证服务器证书，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 在连接字符串中传递用户名/密码。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 驱动程序_。)集成 Windows 身份验证使用 ADAL，需要在兑换 AAD 颁发访问令牌的 Windows 帐户凭据，假设目标数据库为 Azure SQL 数据库中。 获取验证服务器证书，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows 驱动程序_。)AAD 交互式身份验证使用 Azure 多重身份验证技术建立了连接。 在此模式下，通过提供的登录 ID，Windows Azure 身份验证对话框时触发，允许用户输入密码以完成连接。 用户名传递连接字符串中。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- 在新的 Active Directory 选项使用 Windows ODBC 驱动程序，确保[SQL Server 的 Active Directory 身份验证库](http://go.microsoft.com/fwlink/?LinkID=513072)已安装。 当使用 Linux 和 macOS 的驱动程序，确保`libcurl`已安装。 有关驱动程序版本 17.2 及更高版本，这不是显式依赖关系由于不需要其他身份验证方法或 ODBC 操作。
>- 若要使用的 SQL Server 帐户的用户名和密码进行连接，您现在可以使用新`SqlPassword`选项，因为此选项将启用更安全的连接默认设置为 SQL Azure 建议。
>- 若要使用的 Azure Active Directory 帐户的用户名和密码进行连接，指定`Authentication=ActiveDirectoryPassword`连接字符串中并`UID`和`PWD`关键字，使用用户名和密码分别。
>- 若要使用 Windows 集成或 Active Directory 集成 （仅 Windows 驱动程序） 的身份验证进行连接，请指定`Authentication=ActiveDirectoryIntegrated`连接字符串中。 该驱动程序将自动选择正确的身份验证模式。 `UID` 和`PWD`不能指定。
>- 使用 Active Directory Interactive （仅 Windows 驱动程序） 的身份验证进行连接`UID`必须指定。

## <a name="authenticating-with-an-access-token"></a>使用访问令牌进行身份验证

`SQL_COPT_SS_ACCESS_TOKEN`预连接属性允许从 Azure AD 进行身份验证而不是用户名和密码，获取访问令牌使用和也绕过协商和获取访问令牌的驱动程序。 若要使用的访问令牌，将`SQL_COPT_SS_ACCESS_TOKEN`连接属性设置为一个指向`ACCESSTOKEN`结构：

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN`是一种长度可变的结构由组成的 4 字节_长度_跟_长度_的窗体的访问令牌的不透明数据的字节。 由于 SQL Server 如何处理访问令牌，一个通过获取[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)必须展开 JSON 响应，以便每个字节后跟 0 填充字节，类似于包含仅包含 ASCII 字符的 ucs-2 字符串; 但是，该令牌是一个不透明值和指定，以字节为单位，长度不能包含任何 null 终止符。 由于其相当大的长度和格式约束，此身份验证方法是仅可通过以编程方式`SQL_COPT_SS_ACCESS_TOKEN`连接属性，则没有相应的 DSN 或连接字符串关键字。 连接字符串必须包含`UID`， `PWD`， `Authentication`，或`Trusted_Connection`关键字。

> [!NOTE]
> ODBC 驱动程序版本 13.1 上仅支持此身份验证_Windows_。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 身份验证示例代码

下面的示例显示了连接到 SQL Server 所需的代码使用 Azure Active Directory 与连接关键字。 请注意，无需更改应用程序代码，然后重试。连接字符串或如果使用，DSN 是唯一使用 AAD 进行身份验证所需的修改：
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下面的示例显示了连接到 SQL Server 所需的代码使用访问令牌的身份验证使用 Azure Active Directory。 在这种情况下，有必要修改应用程序代码以处理访问令牌并将关联的连接属性设置。
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
下面是一个与 Azure Active Directory 交互式身份验证一起使用的连接字符串示例。 请注意它不包含 PWD 字段，因为将使用 Windows Azure 身份验证屏幕输入的密码。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>另请参阅
[使用 Azure AD 身份验证的 Azure SQL DB 的基于令牌的身份验证支持](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

