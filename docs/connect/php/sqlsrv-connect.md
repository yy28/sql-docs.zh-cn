---
title: "sqlsrv_connect |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
caps.latest.revision: 67
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e9491e2b0721f7c7a2ca6b5ed37c52135a4c760
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

创建一个连接资源，并打开该连接。 默认情况下，使用 Windows 身份验证尝试连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parameters  
*$serverName*：指定建立连接的服务器名称的字符串。 实例名称（例如“myServer\instanceName”）或端口号（例如“myServer, 1521”）可以包括为此字符串的一部分。 有关可用于此参数的选项的完整介绍，请参阅 [结合使用连接字符串关键字与 SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkId=105504)的 ODBC 驱动程序连接字符串关键字部分中的 Server 关键字。  
  
从 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 3.0 开始，你还可以指定带有 `"(localdb)\instancename"`的 LocalDB 实例。 有关详细信息，请参阅 [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。  
  
同样从 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 3.0 开始，你还可以指定要连接到 AlwaysOn 可用性组的虚拟网络名称。 有关对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]支持的详细信息，请参阅 [PHP Driver for SQL Server 对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。  
  
*$connectionInfo* [可选]: 关联**数组**包含连接属性 (例如，**数组**("Database"= >"AdventureWorks"))。 有关数组的受支持密钥的列表，请参阅 [Connection Options](../../connect/php/connection-options.md) 。  
  
## <a name="return-value"></a>返回值  
PHP 连接资源。 如果无法成功创建和打开连接，则返回 **false** 。  
  
## <a name="remarks"></a>注释  
如果在可选的 *$connectionInfo* 参数中没有指定 *UID* 和 *PWD* 的值，将尝试使用 Windows 身份验证进行此连接。 有关连接到服务器的详细信息，请参阅 [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) 和 [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)。  
  
## <a name="example"></a>示例  
以下示例使用 Windows 身份验证创建和打开连接。 该示例假定本地计算机上已安装了 SQL Server 和 [AdventureWorks](http://www.codeplex.com/SqlServerSamples) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[Connecting to the Server](../../connect/php/connecting-to-the-server.md)  
[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

