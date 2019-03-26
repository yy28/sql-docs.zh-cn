---
title: 空闲连接复原
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: a2361c8a2e8cbc709d50a9139678a08e2e850e2d
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305915"
---
# <a name="idle-connection-resiliency"></a>空闲连接复原
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[连接复原](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)是指，断开空闲连接可以重新建立连接，在某些限制条件的原则。 如果连接到 Microsoft SQL Server 失败，则连接复原允许客户端自动尝试重新建立连接。 连接复原能力是数据源; 的属性仅 SQL Server 2014 及更高版本和 Azure SQL 数据库支持连接复原能力。

连接复原能力实现与可以添加到连接字符串的两个连接关键字： **ConnectRetryCount**并**ConnectRetryInterval**。

|关键字|值|，则“默认”|描述|
|-|-|-|-|
|**ConnectRetryCount**| 0 到 255 （含） 之间的整数|1|尝试重新建立断开的连接之前放弃的最大次数。 默认情况下进行一次尝试以重新建立连接时中断。 值为 0 表示将尝试任何重新连接。|
|**ConnectRetryInterval**| 介于 1 和 60 （含） 之间的整数|1| 以秒为单位，两次尝试重新建立的连接之间的时间。 应用程序将尝试在检测到断开的连接后立即重新连接，然后等待**ConnectRetryInterval**秒，然后重试。 如果，则忽略此关键字**ConnectRetryCount**等于 0。

如果的乘积**ConnectRetryCount**乘以**ConnectRetryInterval**大于**LoginTimeout**，则客户端将停止尝试一次连接**LoginTimeout**达到; 否则，它将继续尝试重新连接之前**ConnectRetryCount**为止。

#### <a name="remarks"></a>Remarks

当连接处于空闲状态时，将应用连接复原能力。 故障发生时执行的事务，例如，不会触发重新连接尝试-它们将失败，因为预期的要。 以下情况下，名为不可恢复的会话状态，不会触发重新连接尝试：

* 临时表
* 全局和局部游标
* 事务上下文和会话级别事务锁
* 应用程序锁
* EXECUTE AS / 还原安全上下文
* OLE 自动化句柄
* 已准备好的 XML 句柄
* 跟踪标志

## <a name="example"></a>示例

下面的代码连接到数据库并执行查询。 连接中断通过中止会话，并且使用断开的连接尝试新的查询。 本示例使用 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 示例数据库。

在此示例中，我们可以中断连接之前指定缓冲的游标。 如果我们未指定缓冲的游标，将不重新建立连接因为会有活动的服务器端游标，因此连接将不会空闲时中断。 但是，在这种情况下，我们可以调用 sqlsrv_free_stmt() 中断要腾空游标的连接之前，将成功地重新建立连接。

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
预期的输出：
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>另请参阅
[Windows ODBC 驱动程序中的连接弹性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
