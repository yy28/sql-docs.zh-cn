---
title: 如何：使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e89f3df43a8a3f5327c86c792cc3425e75aede50
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此功能已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的版本 1.1 中添加，并且仅在针对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]使用 SQLSRV 驱动程序时才有效。 将 ReturnDatesAsStrings 连接选项与 PDO_SQLSRV 驱动程序结合使用时会出错。  
  
可以通过在连接字符串中指定一个选项来以字符串的形式检索日期和时间类型（datetime**、date**、time**、datetime2** 和 datetimeoffset**）。  
  
### <a name="to-retrieve-date-and-time-types-as-strings"></a>以字符串的形式检索日期和时间类型  
  
-   使用以下连接选项：  
  
    ```  
    'ReturnDatesAsStrings'=>true  
    ```  
  
    默认值是 **False**，这意味着 **datetime**、 **Date**、 **Time**、 **DateTime2**和 **DateTimeOffset** 类型将返回为 PHP **Datetime** 类型。  
  
## <a name="example"></a>示例  
以下示例演示的语法可用于指定要以字符串的形式检索日期和时间类型。  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例演示当检索字符串时，通过指定 UTF-8 可以字符串的形式检索日期，即使连接是使用 `"ReturnDatesAsStrings" => false` 建立的也是如此。  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));  
  
if( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例演示如何通过在连接字符串中指定 UTF-8 和 `"ReturnDatesAsStrings" => true` 来以字符串的形式检索日期。  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8' );  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例演示如何以 PHP 类型的形式检索日期。 `'ReturnDatesAsStrings'=> false` 处于打开状态。  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$date_string = date_format( $date, 'jS, F Y' );  
echo "Date = $date_string\n";  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[检索数据](../../connect/php/retrieving-data.md)  
  
