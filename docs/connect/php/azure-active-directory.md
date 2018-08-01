---
title: Azure Active Directory |Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 71e6b3b4556621b6bc8a8a4c7996cfdb47a12849
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979439"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) 是作为一种替代方法的核心用户 ID 管理技术[SQL Server 身份验证](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 允许连接到 Microsoft Azure SQL 数据库和 SQL 数据仓库具有联合身份在 Azure AD 中使用用户名和密码、 Windows 集成身份验证或 Azure AD 访问令牌;SQL Server 的 PHP 驱动程序提供对这些功能的部分支持。

若要使用 Azure AD，请使用**身份验证**关键字。 值的**身份验证**可能需要在下表中介绍。

|关键字|值|描述|
|-|-|-|
|**身份验证**|未设置 （默认值）|身份验证模式由其他关键字。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|直接对 SQL Server 实例 （这可能是 Azure 实例） 进行身份验证使用的用户名和密码。 必须为连接字符串，并使用传递的用户名和密码**UID**并**PWD**关键字。 |
||`ActiveDirectoryPassword`|使用 Azure Active Directory 标识使用用户名和密码进行身份验证。 必须为连接字符串，并使用传递的用户名和密码**UID**并**PWD**关键字。 |

**身份验证**关键字会影响连接安全设置。 如果它设置为在连接字符串中，则默认情况下**Encrypt**关键字设置为 true，因此，客户端将请求加密。 此外，服务器证书将验证而不考虑加密设置除非**TrustServerCertificate**设置为 true。 这是可分辨从旧和不太安全，登录方法，在其中的服务器证书尚未验证除非在连接字符串中明确请求加密。

在 Windows 上的 SQL Server 的 PHP 驱动程序使用 Azure AD 之前, 请确保已安装[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=41950)（不需要适用于 Linux 和 MacOS）。

#### <a name="limitations"></a>限制

在 Windows 中上, 基础 ODBC 驱动程序支持的一个更大的价值**身份验证**关键字， **ActiveDirectoryIntegrated**，但 PHP 驱动程序在任何平台上不支持此值，因此还不支持 Azure AD 基于令牌的身份验证。

## <a name="example"></a>示例

下面的示例演示如何使用连接**SqlPassword**并**ActiveDirectoryPassword**。

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

以下示例将执行与上述相同使用 PDO_SQLSRV 驱动程序。

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
[结合使用 Azure Active Directory 和 ODBC 驱动程序](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)
