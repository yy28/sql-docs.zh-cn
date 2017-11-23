---
title: "使用 ODBC 驱动程序的 Azure Active Directory |Microsoft 文档"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: afdd399a8efcbb67915eab1978796b812e8a6558
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>使用 ODBC 驱动程序的 Azure Active Directory
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>用途

ODBC Driver 13.1 for SQL Server 允许 ODBC 应用程序连接到 SQL Azure 实例使用 Azure Active Directory 中的联合的身份，使用用户名/密码、 Azure Active Directory 访问令牌 （仅 Windows 驱动） 或 Windows 集成身份验证 （仅 Windows 驱动程序）。 通过使用新 DSN 和连接字符串关键字，以及连接属性完成该操作。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新的和/或修改 DSN 和连接字符串关键字

`Authentication`关键字可用时使用 DSN 或连接字符串连接来控制身份验证模式。 连接字符串中设置的值，在中重写 DSN，如果提供。 _预属性值_的`Authentication`设置为从连接字符串和 DSN 值计算的值。

|Name|值|默认|Description|
|-|-|-|-|
|`Authentication`|（未设置），（空字符串）， `SqlPassword`， `ActiveDirectoryPassword`，`ActiveDirectoryIntegrated`|(未设置)|控制身份验证模式。<table><tr><th>值<th>Description<tr><td>(未设置)<td>身份验证模式由其他关键字 （现有旧连接选项。）<tr><td>(空字符串)<td>（仅在连接字符串中。）重写和取消设置`Authentication`值在 DSN 中的设置。<tr><td>`SqlPassword`<td>直接进行身份验证使用的用户名和密码的 SQL Server 实例。<tr><td>`ActiveDirectoryPassword`<td>使用 Azure Active Directory 标识使用用户名和密码进行身份验证。<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 驱动程序_。 通过使用集成身份验证的 Azure Active Directory 标识进行身份验证。</table>|
|`Encrypt`|（未设置）， `Yes`，`No`|（请参阅说明）|控制连接的加密。 如果预属性值的`Authentication`未设置，则_无_，默认值是`Yes`。 否则，默认值是`No`。 加密的预属性值是`Yes`如果值设置为`Yes`的 DSN 或连接字符串中。|

## <a name="new-andor-modified-connection-attributes"></a>新的和/或修改连接属性

以下预连接的连接属性具有已引入或修改，可支持 Azure Active Directory 身份验证。 当连接属性具有相应的连接字符串或 DSN 关键字，并且设置时，连接属性优先。

|Attribute|类型|值|默认|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_RESET`|(未设置)|请参阅说明`Authentication`上面的关键字。 `SQL_AU_NONE`若要显式重写一组提供`Authentication`DSN 和/或连接字符串中的值时`SQL_AU_RESET`取消设置该属性，如果它已设置，从而允许要优先的 DSN 或连接字符串值。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|指向`ACCESSTOKEN`或 NULL|NULL|_Windows 驱动程序_。 如果非 null，指定 azure Ad 访问令牌来使用。 它是指定访问令牌中的错误以及`UID`， `PWD`， `Trusted_Connection`，或`Authentication`连接字符串关键字或其等效的属性。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|（请参阅说明）|控制连接的加密。 `SQL_EN_OFF`和`SQL_EN_ON`禁用并启用加密，分别。 如果预属性值的`Authentication`未设置，则_无_或`SQL_COPT_SS_ACCESS_TOKEN`设置，和`Encrypt`默认值中的 DSN 或连接字符串未指定`SQL_EN_ON`。 否则，默认值是`SQL_EN_OFF`。 此属性控制的生效值[是否加密将用于连接。](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|不支持与 Azure Active Directory，因为无法通过 ODBC 连接来实现对 AAD 主体的密码更改。 <br><br>SQL Server 2005 中引入了 SQL Server 身份验证的密码过期。 `SQL_COPT_SS_OLDPWD`属性已添加以允许客户端连接提供旧和新密码。 设置此属性时，访问接口对于第一次连接或后续连接将不使用连接池，因为连接字符串将包含现在已更改的“旧密码”。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_弃用_; 使用`SQL_COPT_SS_AUTHENTICATION`设置为`SQL_AU_AD_INTEGRATED`相反。 <br><br>强制使用 Windows 身份验证 (Kerberos 在 Linux 和 macOS 上) 的登录服务器访问验证。 当使用 Windows 身份验证时，该驱动程序将忽略作为的一部分提供的用户标识符和密码值`SQLConnect`， `SQLDriverConnect`，或`SQLBrowseConnect`处理。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory （仅 Windows 驱动程序） 的用户界面添加

DSN 安装程序和驱动程序的连接 Ui 得到增强，使用与 Azure AD 的身份验证所必需的其他选项。

### <a name="creating-and-editing-dsns-in-the-ui"></a>创建和编辑在 UI 中的 Dsn

则可使用新的 Azure AD 身份验证选项时创建或编辑现有 DSN 使用驱动程序的安装程序 UI:

`Authentication=ActiveDirectoryIntegrated`有关对 SQL Azure 的 Azure Active Directory 集成身份验证

![CreateNewDSN3.png](windows/CreateNewDSN3.png)

`Authentication=ActiveDirectoryPassword`到 SQL Azure 的 Azure Active Directory 用户名/密码身份验证

![CreateNewDSN4.png](windows/CreateNewDSN4.png)

`Authentication=SqlPassword`到 SQL Server 的用户名/密码身份验证 （Azure 或其他方式）

![CreateNewDSN.png](windows/CreateNewDSN.png)

`Trusted_Connection=Yes`对于 Windows 旧 SSPI 集成身份验证

![CreateNewDSN2.png](windows/CreateNewDSN2.png)

四个选项对应于`Trusted_Connection=Yes`(现有旧版 Windows 仅 SSPI 集成的身份验证) 和`Authentication=` `ActiveDirectoryIntegrated`， `SqlPassword`，和`ActiveDirectoryPassword`分别。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示符 （仅 Windows 驱动程序）

提示对话框中时，它请求完成连接所需的信息显示 SQLDriverConnect 包含 Azure AD 身份验证的两个新选项：

![SQLServerLogin.png](windows/SQLServerLogin.png)

这些选项对应于相同的四个在 DSN 安装程序 UI 上面。

### <a name="example-connection-strings"></a>连接字符串示例
1. SQL Server 身份验证 – 旧语法。 未验证服务器证书，并且仅当服务器强制执行它使用加密。 用户名/密码将传入的连接字符串。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 身份验证 – 新的语法。 客户端请求加密 (默认值的`Encrypt`是`true`) 和服务器证书获取已验证，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 用户名/密码将传入的连接字符串。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 集成 Windows 身份验证 (Kerberos 在 Linux 和 macOS 上) 使用 SSPI （到 SQL Server 或 SQL IaaS） – 当前语法。 服务器证书未通过验证，除非使用加密。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 驱动程序_。)集成 Windows 身份验证使用 SSPI （如果目标数据库在 SQL Server 或 SQL IaaS） – 新的语法。 客户端请求加密 (默认值的`Encrypt`是`true`) 和服务器证书获取已验证，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 用户名/密码身份验证 （如果目标数据库位于 Azure SQL DB 中）。 获取验证服务器证书，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 用户名/密码将传入的连接字符串。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 驱动程序_。)使用 ADAL，这就需要兑换 AAD 颁发访问令牌的 Windows 帐户凭据，假设目标数据库在 Azure SQL 数据库中集成的 Windows 身份验证。 获取验证服务器证书，而不考虑加密设置 (除非`TrustServerCertificate`设置为`true`)。 
`server=Server;database=Database; Authentication=ActiveDirectoryIntegrated;`

> [!NOTE] 
>- 当新的 Active Directory 选项使用 Windows ODBC 驱动程序，确保[适用于 SQL Server 的 Active Directory 身份验证库](http://go.microsoft.com/fwlink/?LinkID=513072)已安装。 Linux 和 macOS 驱动程序不需要对使用 Azure Active Directory 进行身份验证的任何附加依赖项。
>- 若要使用的 SQL Server 帐户用户名和密码进行连接，您现在可以使用新`SqlPassword`选项，它建议专门为 SQL Azure 中，因为此选项，可以更安全的连接默认值。
>- 若要使用的 Azure Active Directory 帐户用户名和密码进行连接，指定`Authentication=ActiveDirectoryPassword`连接字符串中与`UID`和`PWD`关键字，使用用户名和密码分别。
>- 若要使用 Windows 集成或 Active Directory 集成 （仅 Windows 驱动程序） 的身份验证进行连接，指定`Authentication=ActiveDirectoryIntegrated`连接字符串中。 该驱动程序将自动选择正确的身份验证模式。 `UID`和`PWD`不能指定。

## <a name="authenticating-with-an-access-token-windows-driver-only"></a>使用访问令牌 （仅 Windows 驱动程序） 进行身份验证

`SQL_COPT_SS_ACCESS_TOKEN`预连接属性允许从 Azure AD 进行身份验证而不是用户名和密码，获取访问令牌的使用，还绕过了协商和获取驱动程序的访问令牌。 若要使用访问令牌，设置`SQL_COPT_SS_ACCESS_TOKEN`连接属性的指针到`ACCESSTOKEN`结构：

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN`是包含一个 4 字节的长度可变结构_长度_跟_长度_窗体的访问令牌的不透明数据的字节。 由于 SQL Server 处理访问令牌的方式，其中一个获取通过[OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios)必须展开 JSON 响应，以便每个字节后跟 0 填充字节，类似于包含仅包含 ASCII 字符的 ucs-2 字符串; 但是，该标记是一个不透明值，以字节为单位，所指定的长度不得包含任何 null 终止符。 由于其相当大的长度和格式约束，此方法的身份验证才以编程方式通过可用`SQL_COPT_SS_ACCESS_TOKEN`coonnection 属性; 没有相应的 DSN 或连接字符串关键字。 连接字符串不能包含`UID`， `PWD`， `Authentication`，或`Trusted_Connection`关键字。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 身份验证的示例代码

下面的示例演示连接到 SQL Server 所需的代码使用 Azure Active Directory 与连接关键字。 请注意，没有无需更改应用程序代码，然后重试。连接字符串或如果使用，DSN 是使用 AAD 进行身份验证所需的唯一修改：
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下面的示例演示了使用 Azure Active Directory 进行访问令牌身份验证连接到 SQL Server 所需的代码。 在这种情况下，有必要，修改应用程序代码以处理的访问令牌并将关联的连接属性设置。
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

## <a name="see-also"></a>另请参阅
[支持使用 Azure AD 身份验证的 Azure SQL DB 的基于令牌的身份验证](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

