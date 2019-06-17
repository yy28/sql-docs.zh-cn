---
title: 如何： 指定 PHP 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 596c7b648d0d6812859fc688657dfba4f7567b1e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799665"
---
# <a name="how-to-specify-php-data-types"></a>如何：指定 PHP 数据类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

如果使用 PDO_SQLSRV 驱动程序，当使用 PDOStatement::bindColumn 和 PDOStatement::bindParam 从服务器中检索数据时，可以指定 PHP 数据类型。 有关详细信息，请参阅 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 和 [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) 。  
  
以下步骤概括了如何在使用 SQLSRV 驱动程序从服务器中检索数据时指定 PHP 数据类型：  
  
1.  使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 组合，设置并执行 Transact-SQL 查询。  
  
2.  通过 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)使数据行可供读取。  
  
3.  结合使用 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 与所需的 PHP 数据类型（指定为可选的第三个参数）从返回行中检索字段数据。 如果未指定可选的第三个参数，将根据默认 PHP 类型返回数据。 有关默认 PHP 返回类型的信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
    有关用于指定 PHP 数据类型的常量的信息，请参阅[常量（icrosoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md) 的 PHPTYPE 部分。  
  
## <a name="example"></a>示例  
以下示例从 AdventureWorks 数据库的 *Production.ProductReview* 表中检索行。 在每个返回行中，  ReviewDate 字段以字符串形式进行检索，Comments  字段以流形式进行检索。 通过使用 PHP [fpassthru](https://php.net/manual/en/function.fpassthru.php) 函数显示流数据。  
  
该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
在该示例中，以字符串形式检索第二个字段 (ReviewDate  ) 会保留精确到毫秒的 SQL Server DATETIME 数据类型。 默认情况下，将 SQL Server DATETIME 数据类型作为 PHP DateTime 对象进行检索，但无法精确到毫秒。  
  
出于演示目的，以流形式检索第四个字段 (Comments  )。 默认情况下，将 SQL Server 数据类型 nvarchar(3850) 作为字符串进行检索，大多数情况下都可接受此方式。  
  
> [!NOTE]  
> [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) 函数提供了在执行查询之前获取字段信息（包括类型信息）的方法。  
  
## <a name="see-also"></a>另请参阅  
[检索数据](../../connect/php/retrieving-data.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)

[如何：使用 SQLSRV 驱动程序检索输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[如何：使用 SQLSRV 驱动程序检索输入和输出参数](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
