---
title: 如何：使用 Windows 身份验证进行连接
description: 了解通过 Drivers for PHP for SQL Server 使用 Windows 集成身份验证进行连接的含义。
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4915343cf9ed7ebf730ac11360f10271c59e92c3
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634831"
---
# <a name="how-to-connect-using-windows-authentication"></a>如何：使用 Windows 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

默认情况下， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 Windows 身份验证连接 SQL Server。 请务必注意，在大多数情况下，这通常意味着使用 Web 服务器的进程标识或线程标识（如果 Web 服务器正在使用模拟）来连接服务器，而不是最终用户的标识。  
  
使用 Windows 身份验证连接 SQL Server 时，必须要考虑以下几点：  
  
-   运行 Web 服务器的进程（或线程）所依据的凭据必须映射到有效的 SQL Server 登录才能建立连接。  
  
-   如果 SQL Server 和 Web 服务器位于不同的计算机上，则必须配置 SQL Server 才能启用远程连接。  
  
> [!NOTE]  
> 建立连接时可以设置连接属性，如 *Database* 和 *ConnectionPooling* 。 有关受支持的连接属性的完整列表，请参阅 [Connection Options](connection-options.md)。  
  
只要可能存在以下原因，都应使用 Windows 身份验证来连接 SQL Server：  
  
-   没有任何凭据在身份验证期间通过网络传递；用户名和密码未嵌入在数据库连接字符串中。 这意味着恶意用户或攻击者无法通过监视网络或查看配置文件内部的连接字符串来获取凭据。  
  
-   用户要进行集中式帐户管理；强制执行多次无效登录请求后的安全策略，如密码有效期、最短密码长度和帐户锁定。  
  
如果 Windows 身份验证不可行，请参阅[如何：使用 SQL Server 身份验证进行连接](how-to-connect-using-sql-server-authentication.md)。  
  
## <a name="example"></a>示例  
通过使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 SQLSRV 驱动程序，以下示例将使用 Windows 身份验证连接到 SQL Server 的本地实例。 建立连接后，服务器将查询正在访问数据库的用户登录名。  
  
该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 当从浏览器运行该示例时，所有输出都将写入该浏览器。  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
下面的示例使用 PDO_SQLSRV 驱动程序来完成与上一示例相同的任务。  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQL Server 身份验证进行连接](how-to-connect-using-sql-server-authentication.md)

[Microsoft Drivers for PHP for SQL Server 编程指南](programming-guide-for-php-sql-driver.md)

[文档中相关的代码示例](about-code-examples-in-the-documentation.md)

[如何：创建 SQL Server 登录名](../../relational-databases/security/authentication-access/create-a-login.md)

[如何：创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)

[管理用户、角色和登录帐户](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[用户架构分离](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[授予对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
