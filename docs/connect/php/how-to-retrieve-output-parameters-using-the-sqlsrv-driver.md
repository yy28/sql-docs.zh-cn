---
title: "如何： 检索输出参数使用 SQLSRV 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7aadbe6a38e8d91c31a76ddd85dc7f5ab6fbc556
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序检索输出参数
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题演示如何调用一个参数已在其中定义为输出参数的存储过程。 请注意，在检索输出参数或输入/输出参数时，必须在可以访问返回的参数值前使用存储过程返回的所有结果。  
  
> [!NOTE]  
> 已初始化或更新为 **null**、 **DateTime**的变量或流类型无法用作输出参数。  
  
在流类型（例如 SQLSRV_SQLTYPE_VARCHAR('max')）用作输出参数时，将会发生数据截断。 不支持将流类型用作输出参数。 对于非流类型，数据截断会在未指定输出参数长度或输出参数的指定长度不够大时发生。  
  
## <a name="example"></a>示例  
以下示例调用可返回某个指定员工的从年初至今的销售的存储过程。 PHP 变量 *$lastName* 是输入参数，而 *$salesYTD* 是输出参数。  
  
> [!NOTE]  
> 将 *$salesYTD* 初始化为 0.0 会将返回的 PHPTYPE 设置为 **浮点型**。 为确保数据类型完整性，应在调用存储过程之前初始化输出参数，或应指定所需的 PHPTYPE。 有关指定 PHPTYPE 的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
由于存储过程仅返回一个结果，所以在执行存储过程后 *$salesYTD* 会立即包含输出参数的返回值。  
  
> [!NOTE]  
> 建议使用规范语法来调用存储过程。 有关规范语法的详细信息，请参阅 [调用存储过程](http://go.microsoft.com/fwlink/?linkid=119517)。  
  
该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array($salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQLSRV 驱动程序指定参数方向](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)  
[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
[检索数据](../../connect/php/retrieving-data.md)  
  
