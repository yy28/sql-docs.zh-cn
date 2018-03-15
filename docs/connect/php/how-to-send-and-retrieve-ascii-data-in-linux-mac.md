---
title: "如何： 发送和检索在 Linux 和 macOS (SQL) 的 ASCII 数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/16/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.workload: On Demand
ms.openlocfilehash: 5fbd86bb120a64d509b6349a589308eda9c26bf8
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>如何： 发送和检索在 Linux 和 macOS ASCII 数据 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文假定已生成或安装 Linux 或 macOS 系统中的 ASCII (非 UTF 8) 区域设置。 

若要发送或检索到服务器的 ASCII 字符集：  

1.  如果所需的区域设置不是你系统的环境中的默认值，请确保你调用`setlocale(LC_ALL, $locale)`之前建立第一个连接。 PHP setlocale() 函数更改仅在当前脚本的区域设置，如果调用进行第一次连接后，可能会被忽略。
 
2.  当使用 SQLSRV 驱动程序，你可能指定`'CharacterSet' => SQLSRV_ENC_CHAR`为连接选项，但此步骤是可选因为它是默认编码。

3.  在使用 PDO_SQLSRV 驱动程序时，有两种方法。 首先，当建立的连接，设置`PDO::SQLSRV_ATTR_ENCODING`到`PDO::SQLSRV_ENCODING_SYSTEM`(有关设置连接选项的示例，请参阅[:: __construct](../../connect/php/pdo-construct.md))。 成功连接之后，或者，添加以下行 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
当你指定的编码的连接资源 （在 SQLSRV) 或连接对象 (PDO_SQLSRV) 时，驱动程序假定其他连接选项字符串使用编码的相同。 也可以假定服务器名称和查询字符串使用相同的字符集。  
  
默认编码 PDO_SQLSRV 驱动程序与不同的是 SQLSRV 驱动程序是 utf-8 (PDO::SQLSRV_ENCODING_UTF8)。 有关这些常量的详细信息，请参阅[常量&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 
  
## <a name="example"></a>示例  
下面的示例演示如何发送和检索使用用于 SQL Server PHP 驱动程序通过建立的连接之前指定特定的区域设置的 ASCII 数据。 在各种 Linux 平台的区域设置可能以不同方式命名从 macOS 中的同一区域设置。 例如，美国 iso-8859-1 (拉丁文 1) 区域设置是`en_US.ISO-8859-1`在 Linux 时在 macOS 名称是`en_US.ISO8859-1`。
  
这些示例假定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的服务器上安装。 从浏览器运行示例时，所有输出都写入浏览器。  
  
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
[使用 utf-8 数据](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[更新数据&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)  
  
