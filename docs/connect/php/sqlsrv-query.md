---
title: sqlsrv_query |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19d7f4d6562f64061f01bf0ff7a73fcd03a4f63c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606247"
---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

准备并执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parameters  
*$conn*：与已准备的语句相关联的连接资源。  
  
$tsql：对应于已准备的语句的 Transact-SQL 表达式。  
  
$params [可选]：对应于参数化查询中参数的值的阵列。 该阵列的每个元素可以是以下项之一：
  
-   文字值。  
  
-   PHP 变量。  
  
-   具有以下结构的 **阵列** ：  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    下表提供对阵列的每个元素的描述：  
  
    |元素|描述|  
    |-----------|---------------|  
    |*$value*|参数值、PHP 变量或通过引用传递的 PHP 变量。|  
    |*$direction*[可选]|用于指示参数方向的以下 SQLSRV_PARAM_ 常量之一：SQLSRV_PARAM_IN、SQLSRV_PARAM_OUT、SQLSRV_PARAM_INOUT**\***。 默认值为 SQLSRV_PARAM_IN。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[可选]|SQLSRV_PHPTYPE_\* 常量，用于指定返回的值的 PHP 数据类型。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$sqlType*[可选]|SQLSRV_SQLTYPE_\* 常量，用于指定输入值的 SQL Server 数据类型。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
  
$options [可选]：关联阵列，用于设置查询属性。 支持的键如下：  
  
|Key|支持的值|描述|  
|-------|--------------------|---------------|  
|QueryTimeout|正整数值。|设置查询超时（以秒为单位）。 默认情况下，驱动程序无限期等待结果。|  
|SendStreamParamsAtExec|**true** 或 **false**<br /><br />默认值为 **true**。|将驱动程序配置为在执行时发送所有流数据 (true)，或配置为在区块中发送流数据 (false)。 默认情况下，该值设置为 **true**。 有关详细信息，请参阅 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可滚动|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|有关这些值的详细信息，请参阅 [指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>返回值  
语句资源。 如果无法创建和/或执行语句，将返回 false。  
  
## <a name="remarks"></a>Remarks  
sqlsrv_query 函数非常适合一次性查询，并且应该是执行查询的默认选项，除非出现特殊情况。 此函数提供了一个简化的方法，以便使用最少的代码来执行查询。 sqlsrv_query 函数可用于语句准备和语句执行，还可用于执行参数化查询。  
  
有关详细信息，请参阅 [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>示例  
在下面的示例中，向 AdventureWorks 数据库的 *Sales.SalesOrderDetail* 表格中插入单个行。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
> [!NOTE]  
> 尽管下面的示例使用 INSERT 语句来演示将 sqlsrv_query 用于执行一次性语句，但是上述概念适用于所有 Transact-SQL 语句。  
  
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
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>示例  
下面的示例将更新 AdventureWorks 数据库的 Sales.SalesOrderDetail 表格中的字段。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> 建议使用字符串作为输入，绑定到的值时[decimal 或 numeric 的列](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)若要确保的精确度和准确度，如 PHP 具有有限的精度[浮点数](https://php.net/manual/en/language.types.float.php)。 这同样适用于到 bigint 列，尤其是有效值的范围之外[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

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
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="example"></a>示例
此代码示例演示如何创建的表[sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)类型，并提取插入的数据。

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$options = array("Database"=>$dbName, "UID"=>$uid, "PWD"=>$pwd);
$conn = sqlsrv_connect($server, $options);
if($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

$tableName = 'testTable';
$query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $query);

if(sqlsrv_fetch($stmt) === false) {
    die(print_r(sqlsrv_errors(), true));
}

$col1 = sqlsrv_get_field($stmt, 0);
echo "First field:  $col1 \n";

$col2 = sqlsrv_get_field($stmt, 1);
echo "Second field:  $col2 \n";

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```

将预期的输出：

```
First field:  1
Second field:  test_data
```

## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  

[如何：执行参数化查询](../../connect/php/how-to-perform-parameterized-queries.md)  

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  

[如何：以流的形式发送数据](../../connect/php/how-to-send-data-as-a-stream.md)  

[使用方向参数](../../connect/php/using-directional-parameters.md)  

  
