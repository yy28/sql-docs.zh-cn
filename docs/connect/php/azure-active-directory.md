---
title: "Azure Active Directory |Microsoft 文档"
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01d921ebee152924b905fa7a9de8c6d46f41ca64
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (Azure AD) 是一种作为的替代方法进行操作的核心用户 ID 管理技术[SQL Server 身份验证](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 允许连接到 Microsoft Azure SQL 数据库和 SQL 数据仓库与联合身份在 Azure AD 中使用用户名和密码、 Windows 集成身份验证或 Azure AD 访问令牌;SQL Server PHP 驱动程序提供部分支持这些功能。

若要使用 Azure AD，使用**身份验证**关键字。 值的**身份验证**可能需要在解释了下表中。

|关键字|值|Description|
|-|-|-|
|**身份验证**|未设置 （默认值）|身份验证模式由其他关键字。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|向 SQL Server 实例 （这可能是 Azure 实例） 直接进行身份验证使用的用户名和密码。 用户名和密码必须传递到连接字符串使用**UID**和**PWD**关键字。 |
||`ActiveDirectoryPassword`|使用 Azure Active Directory 标识使用用户名和密码进行身份验证。 用户名和密码必须传递到连接字符串使用**UID**和**PWD**关键字。 |

**身份验证**关键字会影响连接安全设置。 如果在连接字符串中，则默认情况下设置**Encrypt**关键字设置为 true，因此客户端将请求加密。 此外，服务器证书将验证而不考虑加密设置除非**TrustServerCertificate**设置为 true。 这被区分从旧，和更少的安全，login 方法，在其中的服务器证书尚未验证除非在连接字符串中专门请求加密的。

在 Windows 上的 SQL Server PHP 驱动程序在使用 Azure AD 之前，确保已安装[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=41950)（并非适用于 Linux 和 MacOS 所必需）。

#### <a name="limitations"></a>限制

在 Windows 上，基础的 ODBC 驱动程序支持的一个更大的价值**身份验证**关键字， **ActiveDirectoryIntegrated**，但 PHP 驱动程序在任何平台上不支持此值，因此还不支持基于令牌的 Azure AD 的身份验证。

## <a name="example"></a>示例

下面的示例演示如何使用连接**SqlPassword**和**ActiveDirectoryPassword**。

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

以下示例执行上面与相同 PDO_SQLSRV 驱动程序。

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>另请参阅  
[使用 ODBC 驱动程序的 Azure Active Directory](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)

