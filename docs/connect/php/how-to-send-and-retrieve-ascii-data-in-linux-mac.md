---
title: 如何：在 Linux 和 macOS 中发送和检索 ASCII 数据 (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68251907"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>如何：在 Linux 和 macOS 中发送和检索 ASCII 数据 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文假定已在 Linux 或 macOS 系统中生成或安装 ASCII（非 UTF-8）区域设置。 

向服务器发送或检索 ASCII 字符集：  

1.  如果所需的区域设置不是系统环境中的默认区域设置，请务必在进行第一次连接之前先调用 `setlocale(LC_ALL, $locale)`。 PHP setlocale() 函数仅更改当前脚本的区域设置，如果在进行第一次连接后调用，它可能会被忽略。
 
2.  使用 SQLSRV 驱动程序时，可以将 `'CharacterSet' => SQLSRV_ENC_CHAR` 指定为连接选项，但此步骤是可选的，因为它是默认编码。

3.  在使用 PDO_SQLSRV 驱动程序时，有两种方法。 首先，在建立连接时，将 `PDO::SQLSRV_ATTR_ENCODING` 设置为 `PDO::SQLSRV_ENCODING_SYSTEM`（有关设置连接选项的示例，请参阅 [PDO::__construct](../../connect/php/pdo-construct.md)）。 或者，在成功连接后，添加以下行：`$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
（在 SQLSRV 中）指定连接资源或连接对象 (PDO_SQLSRV) 的编码时，驱动程序假定其他连接选项字符串使用相同的编码。 也可以假定服务器名称和查询字符串使用相同的字符集。  
  
PDO_SQLSRV 驱动程序的默认编码为 UTF-8 (PDO::SQLSRV_ENCODING_UTF8)，这与 SQLSRV 驱动程序不同。 有关这些常量的详细信息，请参阅[常量 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 
  
## <a name="example"></a>示例  
下面的示例演示如何通过在建立连接之前指定特定的区域设置，使用 SQL Server PHP 驱动程序来发送和检索 ASCII 数据。 各种 Linux 平台中的区域设置与 macOS 中的同一区域设置可能具有不同的命名方式。 例如，在 Linux 中，US ISO-8859-1 (Latin 1) 区域设置为 `en_US.ISO-8859-1`，而在 macOS 中名为 `en_US.ISO8859-1`。
  
这些示例假定已在服务器上安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 当从浏览器运行该示例时，所有输出都将写入该浏览器。  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>另请参阅  
[检索数据](../../connect/php/retrieving-data.md)  
[使用 UTF-8 数据](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[更新数据（Microsoft SQL Server PHP 驱动程序）](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)  
  
