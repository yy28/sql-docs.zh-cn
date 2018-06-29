---
title: sqlsrv_prepare |Microsoft 文档
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_prepare
apitype: NA
helpviewer_keywords:
- executing queries
- API Reference, sqlsrv_prepare
- sqlsrv_prepare
ms.assetid: 8c74c697-3296-4f5d-8fb9-e361f53f19a6
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3b376d9fb4333489bf841f04cfb2d429803c6f3
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309676"
---
# <a name="sqlsrvprepare"></a>sqlsrv_prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

创建与指定连接相关联的语句资源。 此函数对于执行多个查询非常有用。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_prepare(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parameters  
*$conn*：与创建的语句相关联的连接资源。  
  
*$tsql*： 对应于已创建语句的 TRANSACT-SQL 表达式。  
  
*$params* [可选]:**数组**的对应参数化查询中的参数的值。 该阵列的每个元素可以是以下项之一：
  
-   文字值。  
  
-   对 PHP 变量的引用。  
  
-   具有以下结构的 **阵列** ：  
  
    ```  
    array(&$value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    > [!NOTE]  
    > 作为查询参数传递的变量应通过引用传递，而不是通过值传递。 例如，传递 `&$myVariable` 而不是 `$myVariable`。 执行具有按值参数的查询时，将引发 PHP 警告。  
  
    下表将介绍这些阵列元素：  
  
    |元素|Description|  
    |-----------|---------------|  
    |*$value*|文字值或对 PHP 变量的引用。|  
    |*$direction*[可选]|以下项之一**SQLSRV_PARAM_\*** 常量用于指示参数方向： **SQLSRV_PARAM_IN**， **SQLSRV_PARAM_OUT**， **SQLSRV_PARAM_INOUT**。 默认值是**SQLSRV_PARAM_IN**。<br /><br />有关 PHP 常量的详细信息，请参阅[常量&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[OPTIONAL]|A **SQLSRV_PHPTYPE_\*** 指定 PHP 数据类型的返回值的常量。|  
    |*$sqlType*[OPTIONAL]|A **SQLSRV_SQLTYPE_\*** 常量，用于指定输入值的 SQL Server 数据类型。|  
  
*$options* [可选]: 用于设置查询属性的关联数组。 下表列出了支持的键和相应值：  
  
|Key|支持的值|Description|  
|-------|--------------------|---------------|  
|QueryTimeout|正整数值。|设置查询超时（以秒为单位）。 默认情况下，该驱动程序将无限期等待结果。|  
|SendStreamParamsAtExec|**true** 或 **false**<br /><br />默认值为 **true**。|配置要发送所有流在执行数据的驱动程序 (**true**)，或将流数据发送消息块 (**false**)。 默认情况下，该值设置为 **true**。 有关详细信息，请参阅 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可滚动|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|有关这些值的详细信息，请参阅 [指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>返回值  
语句资源。 如果无法创建语句资源，将返回 **false** 。  
  
## <a name="remarks"></a>Remarks  
当你准备一个将变量用作参数的语句时，这些变量将绑定到该语句。 这意味着，如果更新变量的值，下次执行该语句时，它将使用更新的参数值运行。  
  
组合**sqlsrv_prepare**和**sqlsrv_execute**离职语句准备和语句执行中的为两个函数调用，并且可以用于执行参数化的查询。 如果要对每次执行使用不同的参数值来多次执行语句，该函数是理想之选。  
  
有关写入和读取大量信息的备用策略，请参阅[SQL 语句的批处理](../../odbc/reference/develop-app/batches-of-sql-statements.md)和[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
有关详细信息，请参阅 [如何：使用 SQLSRV 驱动程序检索输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>示例  
以下示例将准备和执行语句。 语句执行后 (请参阅[sqlsrv_execute](../../connect/php/sqlsrv-execute.md))，更新中的字段*Sales.SalesOrderDetail* AdventureWorks 数据库表。 该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ?   
         WHERE SalesOrderDetailID = ?";  
  
/* Assign parameter values. */  
$param1 = 5;  
$param2 = 10;  
$params = array(&$param1, &$param2);  
  
/* Prepare the statement. */  
if ($stmt = sqlsrv_prepare($conn, $tsql, $params)) {
    echo "Statement prepared.\n";  
} else {  
    echo "Statement could not be prepared.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement. */  
if (sqlsrv_execute($stmt)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Statement could not be executed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例演示如何准备语句，然后使用不同的参数值重新执行它。 该示例将更新 AdventureWorks 数据库中的 *Sales.SalesOrderDetail* 表格的 *OrderQty* 列。 发生更新后，将查询数据库以验证更新是否已成功。 该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  
  
/* Define the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail  
         SET OrderQty = ?  
         WHERE SalesOrderDetailID = ?";  
  
/* Initialize parameters and prepare the statement. Variables $qty  
and $id are bound to the statement, $stmt1. */  
$qty = 0; $id = 0;  
$stmt1 = sqlsrv_prepare($conn, $tsql, array(&$qty, &$id));  
if ($stmt1) {  
    echo "Statement 1 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the SalesOrderDetailID and OrderQty information. This array  
maps the order ID to order quantity in key=>value pairs. */  
$orders = array(1=>10, 2=>20, 3=>30);  
  
/* Execute the statement for each order. */  
foreach ($orders as $id => $qty) {  
    // Because $id and $qty are bound to $stmt1, their updated  
    // values are used with each execution of the statement.   
    if (sqlsrv_execute($stmt1) === false) {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
echo "Orders updated.\n";  
  
/* Free $stmt1 resources.  This allows $id and $qty to be bound to a different statement.*/  
sqlsrv_free_stmt($stmt1);  
  
/* Now verify that the results were successfully written by selecting   
the newly inserted rows. */  
$tsql = "SELECT OrderQty   
         FROM Sales.SalesOrderDetail   
         WHERE SalesOrderDetailID = ?";  
  
/* Prepare the statement. Variable $id is bound to $stmt2. */  
$stmt2 = sqlsrv_prepare($conn, $tsql, array(&$id));  
if ($stmt2) {  
    echo "Statement 2 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement for each order. */  
foreach (array_keys($orders) as $id)  
{  
    /* Because $id is bound to $stmt2, its updated value   
    is used with each execution of the statement. */  
    if (sqlsrv_execute($stmt2)) {  
        sqlsrv_fetch($stmt2);  
        $quantity = sqlsrv_get_field($stmt2, 0);  
        echo "Order $id is for $quantity units.\n";  
    } else {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
  
/* Free $stmt2 and connection resources. */  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> 建议绑定到的值时，使用字符串作为输入[decimal 或 numeric 列](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)以确保精度和准确性，如 PHP 具有有限的精度[浮点数](http://php.net/manual/en/language.types.float.php)。 这同样适用于 bigint 列，尤其是在有效值的范围之外时[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="example"></a>示例  
此代码示例演示如何将绑定十进制值作为输入参数。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[如何：执行参数化查询](../../connect/php/how-to-perform-parameterized-queries.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)

[如何：以流的形式发送数据](../../connect/php/how-to-send-data-as-a-stream.md)

[使用方向参数](../../connect/php/using-directional-parameters.md)

[检索数据](../../connect/php/retrieving-data.md)

[更新数据（Microsoft Drivers for PHP for SQL Server）](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

