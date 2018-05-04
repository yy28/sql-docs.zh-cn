---
title: 空闲连接复原
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: ba55069430198661a4454269afd12db6c21bd24d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="idle-connection-resiliency"></a>空闲连接复原
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[连接复原](https://msdn.microsoft.com/library/dn632678.aspx)是，断开的空闲连接可以重新建立，某些约束内的原则。 如果与 Microsoft SQL Server 的连接失败，则连接复原允许客户端自动尝试重新建立连接。 连接复原能力是数据源; 的属性仅 SQL Server 2014 及更高版本和 Azure SQL 数据库支持连接复原。

连接复原实现与可以添加到连接字符串的两个连接关键字： **ConnectRetryCount**和**ConnectRetryInterval**。

|关键字|值|默认|Description|
|-|-|-|-|
|**ConnectRetryCount**| 介于 0 和 255 （含） 之间的整数|1|尝试重新建立放弃之前断开的连接的最大次数。 默认情况下，进行一次尝试以重新建立连接时中断。 值为 0 表示将尝试没有重新连接。|
|**ConnectRetryInterval**| 介于 1 和 60 （含） 之间的整数|1| 以秒为单位，以重新建立连接尝试之间的时间。 应用程序将尝试检测到断开的连接后立即重新连接，并会然后等到**ConnectRetryInterval**秒，然后重试。 如果此关键字将被忽略**ConnectRetryCount**等于 0。

如果的产品**ConnectRetryCount**乘以**ConnectRetryInterval**大于**LoginTimeout**，则客户端将停止尝试进行一次连接**LoginTimeout**为止; 否则，它将继续尝试重新连接直到**ConnectRetryCount**为止。

#### <a name="remarks"></a>注释

在连接处于空闲状态时，连接复原适用。 执行事务，例如，不会触发重新连接尝试 – 时发生的失败则会失败否则按预期的那样。 下列情况下，名为不可恢复的会话状态，不会触发重新连接尝试次数：

* 临时表
* 全局和局部游标
* 事务上下文和会话级别事务锁
* 应用程序锁
* EXECUTE AS / 还原安全上下文
* OLE 自动化句柄
* 已准备好的 XML 句柄
* 跟踪标志

## <a name="example"></a>示例

下面的代码连接到数据库并执行查询。 连接将中断通过终止会话，然后使用断开的连接尝试新的查询。 此示例使用[AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx)示例数据库。

在此示例中，我们在断开连接之前指定的缓冲的游标。 如果我们未指定的缓冲的游标，将不重新建立连接因为将有活动的服务器端游标，因此将不会对连接空闲时中断。 但是，在这种情况下，我们可以调用 sqlsrv_free_stmt() 中断腾空游标，该连接之前，将已成功重新建立连接。

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
[Windows ODBC 驱动程序中的连接弹性](https://docs.microsoft.com/en-us/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)
