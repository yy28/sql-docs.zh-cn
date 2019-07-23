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
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265180"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)(Azure AD) 是一个中心用户 ID 管理技术, 作为[SQL Server 身份验证](../../connect/php/how-to-connect-using-sql-server-authentication.md)的替代方法。 Azure AD 允许使用用户名和密码、Windows 集成身份验证或 Azure AD 访问令牌连接到 Azure AD 中的联合身份 Microsoft Azure SQL 数据库和 SQL 数据仓库。 SQL Server 的 PHP 驱动程序提供对这些功能的部分支持。

若要使用 Azure AD, 请使用**Authentication**或**AccessToken**关键字 (互斥), 如下表所示。 有关更多技术详细信息, 请参阅将[Azure Active Directory 与 ODBC 驱动程序结合使用](../../connect/odbc/using-azure-active-directory.md)。

|关键字|值|描述|
|-|-|-|
|**AccessToken**|未设置 (默认值)|由其他关键字确定的身份验证模式。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||一个字节字符串|从 OAuth JSON 响应中提取的 Azure AD 访问令牌。 连接字符串不能包含用户 ID、密码或 Authentication 关键字 (在 Linux 或 macOS 中需要 ODBC Driver 17 或更高版本)。 |
|**身份验证**|未设置 (默认值)|由其他关键字确定的身份验证模式。 有关详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|使用用户名和密码直接对 SQL Server 实例 (可能是 Azure 实例) 进行身份验证。 必须使用**UID**和**PWD**关键字将用户名和密码传递到连接字符串。 |
||`ActiveDirectoryPassword`|使用用户名和密码通过 Azure Active Directory 标识进行身份验证。 必须使用**UID**和**PWD**关键字将用户名和密码传递到连接字符串。 |
||`ActiveDirectoryMsi`|使用系统分配的托管标识或用户分配的托管标识进行身份验证 (需要 ODBC Driver 版本17.3.1.1 或更高版本)。 有关概述和教程, 请参阅[Azure 资源的托管标识是什么？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)。|

**Authentication**关键字影响连接安全设置。 如果在连接字符串中设置了, 则默认情况下将**encryption 关键字设置**为 true, 这意味着客户端将请求加密。 而且, 除非将**TrustServerCertificate**设置为 true (默认值为**false** ), 否则将验证服务器证书, 而不考虑加密设置。 此功能有别于旧的、不安全的登录方法, 在此方法中, 仅当在连接字符串中明确请求加密时, 才会验证服务器证书。

将 Azure AD 与 Windows 上 SQL Server 的 PHP 驱动程序一起使用时, 可能会要求你安装[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=41950)(对于 ODBC 17 +, 不是必需的)。

#### <a name="limitations"></a>限制

在 Windows 上, 基础 ODBC 驱动程序为**Authentication**关键字**ActiveDirectoryIntegrated**支持一个更多的值, 但 PHP 驱动程序不支持任何平台上的此值。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>示例-使用 SqlPassword 和 ActiveDirectoryPassword 进行连接

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>示例-使用 Azure 资源的托管标识进行连接

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>对 SQLSRV 驱动程序使用系统分配的托管标识

使用系统分配的托管标识进行连接时, 请不要使用 UID 或 PWD 选项。

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>将用户分配的托管标识用于 PDO_SQLSRV 驱动程序

用户分配的托管标识作为独立的 Azure 资源创建。 Azure 会在所使用的订阅所信任的 Azure AD 租户中创建标识。 创建标识后, 可以将标识分配给一个或多个 Azure 服务实例。 `Object ID`复制此标识的, 并将其设置为连接字符串中的用户名。 

因此, 当使用用户分配的托管标识进行连接时, 请提供对象 ID 作为用户名, 但要省略密码。

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

[Azure 资源的托管标识是什么？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
