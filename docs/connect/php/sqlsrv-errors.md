---
title: sqlsrv_errors | Microsoft Docs
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
ms.topic: conceptual
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bd38f2d165f1b6e4ebea1bfa9b18c1aa23cd75c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

返回扩展错误和/或最后一个有关的警告信息**sqlsrv**执行操作。  
  
**Sqlsrv_errors**函数可以通过其中一个在下面的 Parameters 节中指定的参数值调用返回错误和/或警告信息。  
  
默认情况下，对任何 **sqlsrv** 函数的调用所生成的警告将会视为错误；如果警告发生在调用 **sqlsrv** 函数时，则该函数会返回 false。 但是，对应于 SQLSTATE 值 01000、01001、01003 和 01S02 的警告决不视为错误。  
  
以下代码行会关闭上述行为；对 **sqlsrv** 函数的调用所生成的警告不会导致函数返回 false：  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
以下代码行恢复默认行为；警告（有例外，如上所述）将会视为错误。  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
而不考虑设置，警告只能检索通过调用**sqlsrv_errors**使用**SQLSRV_ERR_ALL**或**SQLSRV_ERR_WARNINGS**参数值 （请参阅Parameters 节下面有关详细信息）。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>Parameters  
*$errorsAndOrWarnings*[可选]: 预定义的常量。 此参数可以采用下表中所列的值之一：  
  
|“值”|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|将返回在上次调用 **sqlsrv** 函数时生成的错误和警告。|  
|SQLSRV_ERR_ERRORS|将返回上次调用 **sqlsrv** 函数时生成的错误。|  
|SQLSRV_ERR_WARNINGS|将返回上次调用 **sqlsrv** 函数时生成的警告。|  
  
如果未提供任何参数值，则将返回上次调用 **sqlsrv** 函数时生成的错误和警告。  
  
## <a name="return-value"></a>返回值  
数组的 **array** 或 **null**。 每个**数组**在返回**数组**包含三个键-值对。 下表列出了每个键及其描述：  
  
|Key|Description|  
|-------|---------------|  
|SQLSTATE|对于来源于 ODBC 驱动程序的错误，为 ODBC 返回的 SQLSTATE。 了解适用于 ODBC 的 SQLSTATE 值时，请参阅[ODBC 错误代码](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。<br /><br />对于来源于 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的错误，为 IMSSP 的 SQLSTATE。<br /><br />对于来源于 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的警告，为 01SSP 的 SQLSTATE。|  
|代码|对于来源于 SQL Server 的错误，为本机 SQL Server 错误代码。<br /><br />对于来源于 ODBC 驱动程序的错误，为 ODBC 返回的错误代码。<br /><br />对于来源于 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的错误，为 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 错误代码。 有关详细信息，请参阅 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)。|  
|message|错误的说明。|  
  
数组值还可以使用数值键 0、1 和 2 访问。 如果未发生任何错误或警告，将返回 **null** 。  
  
## <a name="example"></a>示例  
以下示例显示在失败的语句执行期间发生的错误。 (该语句将失败，因为**InvalidColumName**不是指定表中的有效列名。)该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
