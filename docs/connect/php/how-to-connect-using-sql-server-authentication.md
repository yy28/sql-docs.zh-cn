---
title: "如何： 使用 SQL Server 身份验证进行连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d4305d3b6dd25f3a06cda56db8e69fcd5d09972
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-using-sql-server-authentication"></a>如何：使用 SQL Server 身份验证进行连接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

当连接到 SQL Server 时， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支持使用 SQL Server 身份验证。  
  
应仅在 Windows 身份验证不可用时才使用 SQL Server 身份验证。 有关使用 Windows 身份验证进行连接的信息，请参阅 [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md)。  
  
使用 SQL Server 身份验证连接到 SQL Server 时，必须考虑以下几点：  
  
-   必须在服务器上启用 SQL Server 混合模式身份验证。  
  
-   用户 ID 和密码 (*UID*和*PWD* SQLSRV 驱动程序中的连接属性) 尝试建立连接时，必须设置。 用户 ID 和密码必须映射到有效的 SQL Server 用户和密码。  
  
> [!NOTE]  
> 包含右大括号 (}) 的密码必须使用另一个右大括号进行转义。 例如，如果 SQL Server 密码为“pass}word”，则 *PWD* 连接属性的值必须设置为“pass}}word”。  
  
在使用 SQL Server 身份验证连接到 SQL Server 时，应采取以下预防措施：  
  
-   保护（加密）通过网络从 Web 服务器传递到数据库的凭据。 从 SQL Server 2005 开始，默认对凭据进行加密。 为了提高安全性，请将“Encrypt”连接属性设置为“启用”，以便对发送至服务器的所有数据进行加密。  
  
> [!NOTE]  
> 将“Encrypt”连接属性设置为“启用”可能会导致性能降低，因为数据加密可能是一项计算量较大的操作。  
  
-   不要在 PHP 脚本的纯文本中包含 *UID* 和 *PWD* 连接属性的值。 这些值应存储在具有相应受限权限的特定于应用程序的目录中。  
  
-   避免使用 *sa* 帐户。 将应用程序映射到拥有所需权限的数据库用户，并使用强密码。  
  
> [!NOTE]  
> 在建立连接时，可以设置除用户 ID 和密码之外的连接属性。 有关受支持的连接属性的完整列表，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="example"></a>示例  
以下示例使用 SQLSRV 驱动程序和 SQL Server 身份验证来连接到 SQL Server 的本地实例。 所需的值*UID*和*PWD*连接属性会从应用程序特定的文本文件， *uid.txt*和*pwd.txt*中*C:\AppData*目录。 建立连接后，将查询服务器以验证用户登录名。  
  
该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从浏览器运行该示例时，所有输出都将写入该浏览器。  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
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
此示例使用 PDO_SQLSRV 驱动程序来演示如何使用 SQL Server 身份验证进行连接。  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
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
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[关于文档中的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
[SUSER_SNAME (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=106382)  
[如何创建 SQL Server 登录名](http://go.microsoft.com/fwlink/?LinkId=106325)  
[如何创建数据库用户](http://go.microsoft.com/fwlink/?LinkId=106327)  
[管理用户、角色和登录名](http://go.microsoft.com/fwlink/?LinkId=106329)  
[用户架构分离](http://go.microsoft.com/fwlink/?LinkId=106330)  
[Grant 对象权限 (TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=106332)  
  

