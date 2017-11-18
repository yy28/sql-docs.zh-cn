---
title: "使用 SQLSRV 驱动程序流的形式检索字符数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 30d0b0884b258d494ffadcb3d44b76f197a445a5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序以流的形式检索字符数据
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

流选项仅适用于的 SQLSRV 驱动程序的形式检索数据[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，并在 PDO_SQLSRV 驱动程序中不可用。  
  
SQLSRV 驱动程序利用 PHP 流从服务器检索大量数据。 本主题中的示例演示如何以流的形式检索字符数据。  
  
## <a name="example"></a>示例  
以下示例从 AdventureWorks 数据库的 *Production.ProductReview* 表中检索行。 返回行的 *Comments* 字段以流的形式检索，并通过使用 PHP [fpassthru](http://go.microsoft.com/fwlink/?LinkId=217496) 函数进行显示。  
  
通过使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 和 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) （其中返回类型指定为字符流）来完成以流的形式检索数据操作。 通过使用常量指定返回类型**SQLSRV_PHPTYPE_STREAM**。 璝惠**sqlsrv**常量，请参阅[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
该示例假定已在本地计算机上安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
因为没有为前三个字段指定任何 PHP 返回类型，所以每个字段均按照其默认 PHP 类型进行返回。 有关默认 PHP 数据类型的信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。 有关如何指定 PHP 返回类型的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
## <a name="see-also"></a>另请参阅  
[检索数据](../../connect/php/retrieving-data.md)  
[使用 SQLSRV 驱动程序以流的形式检索数据](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)  
[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

