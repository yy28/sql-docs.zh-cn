---
title: Azure Active Directory |Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62522802"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) 是作为一种替代方法的核心用户 ID 管理技术[SQL Server 身份验证](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 允许连接到 Microsoft Azure SQL 数据库和 SQL 数据仓库具有联合身份在 Azure AD 中使用用户名和密码、 Windows 集成身份验证或 Azure AD 访问令牌。 SQL Server 的 PHP 驱动程序提供对这些功能的部分支持。

若要使用 Azure AD，请使用**身份验证**或**AccessToken**关键字 （它们是互相排斥） 下, 表中所示。 有关更多技术详细信息，请参阅[使用 Azure Active Directory 与 ODBC 驱动程序](../../connect/odbc/using-azure-active-directory.md)。

|关键字|值|描述|
|-|-|-|
|**AccessToken**|未设置 （默认值）|身份验证模式由其他关键字。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||一个字节的字符串|Azure AD 访问令牌的 OAuth JSON 响应中提取。 连接字符串必须包含用户 ID、 密码或身份验证关键字 (需要 ODBC 驱动程序版本 17 或更高版本在 Linux 或 macOS 中)。 |
|**身份验证**|未设置 （默认值）|身份验证模式由其他关键字。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|直接对 SQL Server 实例 （这可能是 Azure 实例） 进行身份验证使用的用户名和密码。 必须为连接字符串，并使用传递的用户名和密码**UID**并**PWD**关键字。 |
||`ActiveDirectoryPassword`|使用 Azure Active Directory 标识使用用户名和密码进行身份验证。 必须为连接字符串，并使用传递的用户名和密码**UID**并**PWD**关键字。 |
||`ActiveDirectoryMsi`|使用系统分配的托管的标识或用户分配的托管的标识进行身份验证 (需要 ODBC 驱动程序版本 17.3.1.1 或更高版本)。 有关概述和教程，请参阅[什么是 Azure 资源的管理的标识？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)。|

**身份验证**关键字会影响连接安全设置。 如果它设置为在连接字符串中，则默认情况下**Encrypt**关键字设置为 true，这意味着，客户端将请求加密。 此外，服务器证书将验证而不考虑加密设置除非**TrustServerCertificate**设置为 true (**false**默认情况下)。 此功能有别于旧，不太安全的登录方法，仅当在连接字符串中专门请求加密，服务器证书进行验证。

当 Windows 上的 SQL Server 的 PHP 驱动程序使用 Azure AD，你可能需要安装[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=41950)（不需要 ODBC 17 +）。

#### <a name="limitations"></a>限制

在 Windows 中上, 基础 ODBC 驱动程序支持的一个更大的价值**身份验证**关键字， **ActiveDirectoryIntegrated**，但是 PHP 驱动程序在任何平台上不支持此值。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>示例-使用 SqlPassword 和 ActiveDirectoryPassword 连接

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>示例-使用 PDO_SQLSRV 驱动程序进行连接

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>示例-使用 Azure AD 访问令牌进行连接

### <a name="sqlsrv-driver"></a>SQLSRV 驱动程序

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 驱动程序

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>示例-使用 Azure 资源管理的标识进行连接

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>系统分配的托管的标识使用 SQLSRV 驱动程序

当使用系统分配连接管理标识时，则不要使用的 UID 或 PWD 选项。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>使用 PDO_SQLSRV 驱动程序的用户分配托管的标识

用户分配的托管的标识将创建为独立的 Azure 资源。 Azure 中使用的订阅信任的 Azure AD 租户中创建一个标识。 创建的标识后，可以将标识分配给一个或多个 Azure 服务实例。 复制`Object ID`此标识和组的用户为其命名连接字符串中。 

因此，当使用用户分配连接管理标识，提供与用户名同名的对象 ID，但省略了密码。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>另请参阅
[结合使用 Azure Active Directory 和 ODBC 驱动程序](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[什么是 Azure 资源的管理的标识？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
