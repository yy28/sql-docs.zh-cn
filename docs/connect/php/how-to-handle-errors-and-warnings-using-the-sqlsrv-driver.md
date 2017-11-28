---
title: "如何： 处理错误和警告使用 SQLSRV 驱动程序 |Microsoft 文档"
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
helpviewer_keywords: errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 02aa17ddd031d351510f600f60dcd99b42a5d6e5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序处理错误和警告
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

默认情况下，SQLSRV 驱动程序会将警告视为错误；对生成错误或警告的 **sqlsrv** 函数的调用将返回 **false**。 本主题演示如何关闭此默认行为以及如何分别处理警告与错误。  
  
> [!NOTE]  
> 有一些例外情况，即将警告视为错误的默认行为。 对应于 SQLSTATE 值 01000、01001、01003 和 01S02 的警告决不会被视为错误。  
  
## <a name="example"></a>示例  
下面的代码示例使用两个用户定义函数， **DisplayErrors**和**DisplayWarnings**，目的是处理错误和警告。 该示例演示如何通过执行以下操作分别处理警告和错误：  
  
1.  关闭将警告视为错误的默认行为。  
  
2.  创建可更新员工的休假小时数并将剩余休假小时数作为输出参数返回的存储过程。 当某一员工的可用休假小时数小于零时，该存储的过程将显示一条警告。  
  
3.  通过调用每个员工的存储过程更新多个员工的休假小时数，并显示与出现的任何警告和错误相对应的消息。  
  
4.  显示每个员工的剩余休假小时数。  
  
请注意，在首次调用**sqlsrv**函数 ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md))，警告视为错误。 因为警告添加到了错误集合中，因此不需要分别检查警告和错误。 但是，在后续调用 **sqlsrv** 函数过程中，不会将警告视为错误，因此必须准确地检查警告和错误。  
  
另请注意，该示例代码在每次调用 **sqlsrv** 函数之后检查错误。 这是建议做法。  
  
此示例假定本地计算机上已安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。 当针对新安装的 AdventureWorks 数据库运行该示例时，它将产生三条警告和两个错误。 前两条警告是连接到数据库时就会发出的标准警告。 之所以出现第三条警告是因为员工的可用休假小时数更新为小于零的值。 发生错误的原因是员工的可用休假小时数更新为小于 40 小时的值，这与表中的约束条件冲突。  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to substract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQLSRV 驱动程序配置错误和警告处理](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
