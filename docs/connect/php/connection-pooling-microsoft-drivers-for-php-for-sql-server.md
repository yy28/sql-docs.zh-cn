---
title: 连接池 (Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02db1d891f02dce9912d4cdcf78ca0166eab9c32
ms.sourcegitcommit: ef7f2540ba731cc6a648005f2773d759df5c6405
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39415476"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>连接池 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

有关 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中的连接池，需要注意以下要点：  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 ODBC 连接池。  
  
-   默认情况下，连接池在 Windows 中处于启用状态。 在 Linux 和 macOS 中，连接建立池连接仅当启用连接池用于 ODBC (请参阅[启用/禁用连接池](#enablingdisabling-connection-pooling))。 如果启用连接池，连接到服务器的驱动程序将尝试使用已入池的连接，然后它会创建一个新。 如果在池中未找到等效连接，将创建新的连接，并将其添加到该池中。 该驱动程序将基于连接字符串的比较结果确定连接是否等效。  
  
-   当使用池中的某个连接时，会重置该连接状态。  
  
-   关闭连接会将该连接返回到池。  
  
若要详细了解连接池，请参阅[驱动程序管理器连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="enablingdisabling-connection-pooling"></a>启用/禁用连接池
### <a name="windows"></a>Windows
可以将连接字符串中的 ConnectionPooling 属性值设置为 false 或 0，强制驱动程序新建连接，而不是在连接池中查找等效连接。  
  
如果在连接字符串中省略了 ConnectionPooling 属性，或将此属性值设置为 true 或 1，那么仅当连接池中没有等效连接时，驱动程序才会新建连接。  
  
有关其他连接属性的信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
### <a name="linux-and-macos"></a>Linux 和 macOS
*ConnectionPooling*属性不能用于启用/禁用连接池。 

连接池可以启用/禁用通过编辑 odbcinst.ini 配置文件。 以使更改生效，应重新加载该驱动程序。

设置`Pooling`到`Yes`和一个正`CPTimeout`odbcinst.ini 文件中的值，将启用连接池。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
至少，odbcinst.ini 文件应类似于此示例中：

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

设置`Pooling`到`No`odbcinst.ini 文件会强制驱动程序来创建新的连接。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Remarks
- 在 Linux 或 macOS 中，所有连接将建立都池连接如果 odbcinst.ini 文件中启用了池。 这意味着 ConnectionPooling 连接选项不起作用。 若要禁用了连接池，将设置池 = No odbcinst.ini 文件中的并重新加载驱动程序。
  - unixODBC < = 2.3.4 （Linux 和 macOS） 可能不会返回正确的诊断信息，例如错误消息、 警告和信息性消息
  - 出于此原因，SQLSRV 和 PDO_SQLSRV 驱动程序可能无法正确地提取以字符串形式的长数据 （如 xml、 二进制)。 可以作为一种解决方法的流的形式提取的长整型数据。 SQLSRV，请参阅下面的示例。

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>另请参阅  
[如何：使用 Windows 身份验证进行连接](../../connect/php/how-to-connect-using-windows-authentication.md)

[如何：使用 SQL Server 身份验证进行连接](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
