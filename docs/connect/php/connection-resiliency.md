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
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265167"
---
# <a name="idle-connection-resiliency"></a>空闲连接复原
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[连接复原](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)是指可以在某些约束内重新建立中断的空闲连接的原则。 如果与 Microsoft SQL Server 的连接失败, 则连接复原允许客户端自动尝试重新建立连接。 连接复原是数据源的属性;仅 SQL Server 2014 及更高版本以及 Azure SQL 数据库支持连接复原。

连接复原是通过可添加到连接字符串的两个连接关键字实现的: **ConnectRetryCount**和**ConnectRetryInterval**。

|关键字|值|，则“默认”|描述|
|-|-|-|-|
|**ConnectRetryCount**| 介于 0 和 255 之间（含限值）的整数|1|在放弃之前, 尝试重新建立断开连接的最大次数。 默认情况下, 一次尝试在中断时重新建立连接。 值0表示不会尝试重新连接。|
|**ConnectRetryInterval**| 介于 1 和 60 之间（含限值）的整数|1| 尝试重新建立连接所用的时间 (以秒为单位)。 应用程序将在检测到中断的连接时立即尝试重新连接, 然后等待**ConnectRetryInterval**秒, 然后重试。 如果**ConnectRetryCount**等于 0, 则忽略此关键字。

如果**ConnectRetryCount**的乘积乘以**ConnectRetryInterval**大于**LoginTimeout**, 则在达到**LoginTimeout**后, 客户端将停止尝试连接;否则, 在达到**ConnectRetryCount**之前, 它将继续尝试重新连接。

#### <a name="remarks"></a>Remarks

连接处于空闲状态时, 将应用连接复原。 例如, 在执行事务时发生的故障将不会触发重新连接尝试-它们将失败, 否则应该会失败。 以下情况 (称为不可恢复的会话状态) 将不会触发重新连接尝试:

* 临时表
* 全局和局部游标
* 事务上下文和会话级事务锁
* 应用程序锁
* EXECUTE AS/REVERT 安全上下文
* OLE 自动化处理
* 已准备的 XML 句柄
* 跟踪标志

## <a name="example"></a>示例

以下代码连接到数据库并执行查询。 通过终止会话来中断连接, 并使用断开的连接尝试新的查询。 本示例使用 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 示例数据库。

在此示例中, 我们将在中断连接之前指定一个缓冲的游标。 如果未指定缓冲游标, 连接将不会重新建立, 因为这会产生活动的服务器端游标, 从而导致连接在中断时不会处于空闲状态。 但是, 在这种情况下, 我们可以在中断连接以 vacate 游标之前调用 sqlsrv_free_stmt (), 并成功重新建立连接。

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
预期输出:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>另请参阅
[Windows ODBC 驱动程序中的连接弹性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
