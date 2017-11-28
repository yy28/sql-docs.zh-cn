---
title: "如何： 检索使用 SQLSRV 驱动程序的 I/O 参数 |Microsoft 文档"
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
ms.assetid: 9a7c5f60-67f9-4968-a3a8-c256ee481da2
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76423ca2d960951ecdc7a58181393eed792ab756
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver"></a>How to: Retrieve Input and Output Parameters Using the SQLSRV Driver
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题演示如何使用 SQLSRV 驱动程序调用其中一个参数已定义为输入/输出参数的存储过程，以及如何检索结果。 请注意，在检索输出参数或输入/输出参数时，必须在可以访问返回的参数值前使用存储过程返回的所有结果。  
  
> [!NOTE]  
> 已初始化或更新为 **null**、 **DateTime**的变量或流类型无法用作输出参数。  
  
## <a name="example"></a>示例  
下面的示例将调用一个从指定员工的可用休假小时数减去已用休假小时数的存储过程。 表示已用休假小时数的变量 *$vacationHrs*将作为输入参数传递给该存储过程。 在更新可用休假小时数之后，该存储过程将使用同一参数返回剩余的休假小时数。  
  
> [!NOTE]  
> 将 *$vacationHrs* 初始化为 4 可将返回的 PHPTYPE 设置为整数。 若要确保数据类型的完整性，应先初始化输入/输出参数并随后调用存储过程，或者应指定所需的 PHPTYPE。 有关指定 PHPTYPE 的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
存储的过程返回两个结果，因为[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)后执行存储的过程以使输出参数的值可用必须调用。 在调用**sqlsrv_next_result**， *$vacationHrs*包含存储过程返回的输出参数的值。  
  
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
$tsql_dropSP = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = "CREATE PROCEDURE SubtractVacationHours  
                        @EmployeeID int,  
                        @VacationHrs smallint OUTPUT  
                  AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHrs  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHrs = (SELECT VacationHours  
                                      FROM HumanResources.Employee  
                                      WHERE EmployeeID = @EmployeeID)";  
  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call SubtractVacationHours( ?, ?)}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an INOUT  
parameter. Initializing $vacationHrs to 8 sets the returned PHPTYPE to  
integer. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
  
$employeeId = 4;  
$vacationHrs = 8;  
$params = array(   
                 array($employeeId, SQLSRV_PARAM_IN),  
                 array($vacationHrs, SQLSRV_PARAM_INOUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $vacationHrs. */  
sqlsrv_next_result($stmt3);  
echo "Remaining vacation hours: ".$vacationHrs;  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQLSRV 驱动程序指定参数方向](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)  
[如何：使用 SQLSRV 驱动程序检索输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)  
[检索数据](../../connect/php/retrieving-data.md)  
  
