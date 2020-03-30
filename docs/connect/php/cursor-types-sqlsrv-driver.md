---
title: 游标类型（SQLSRV 驱动程序）| Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac090ad8831397bf31c0911ab8a8db21486528db
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015111"
---
# <a name="cursor-types-sqlsrv-driver"></a>游标类型（SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

通过 SQLSRV 驱动程序，可以创建能够以任何顺序访问且具有行的结果集，具体取决于游标类型。  本主题将讨论客户端（缓冲）和服务器端（非缓冲）游标。  
  
## <a name="cursor-types"></a>游标类型  
使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 创建结果集时，可以指定游标的类型。 默认情况下使用只进游标，使用它可以从结果集的第一行开始一次移动一行，直到到达结果集的末尾。  
  
可以使用可滚动游标创建结果集，这样可以采用任意顺序访问结果集中的任意行。 下表列出了可以传递给 sqlsrv_query 或 sqlsrv_prepare 中的 Scrollable  选项的值。  
  
|选项|说明|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|使用此游标可以从结果集的第一行开始一次移动一行，直到到达结果集的末尾。<br /><br />这是默认的游标类型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 返回使用此游标类型创建的结果集的错误。<br /><br />forward  是 SQLSRV_CURSOR_FORWARD 的缩写形式。|  
|SQLSRV_CURSOR_STATIC|使用此游标可以采用任意顺序访问行，但不会反映数据库中的更改。<br /><br />static  是 SQLSRV_CURSOR_STATIC 的缩写形式。|  
|SQLSRV_CURSOR_DYNAMIC|使用此游标可以采用任意顺序访问行，并且会反映出数据库中的更改。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 返回使用此游标类型创建的结果集的错误。<br /><br />dynamic  是 SQLSRV_CURSOR_DYNAMIC 的缩写形式。|  
|SQLSRV_CURSOR_KEYSET|使用此游标可以采用任意顺序访问行。 然而，如果从表中删除某一行，键集游标不会更新行计数（将返回不含任何值的已删除行）。<br /><br />keyset  是 SQLSRV_CURSOR_KEYSET 的缩写形式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|使用此游标可以采用任意顺序访问行。 创建客户端游标查询。<br /><br />buffered  是 SQLSRV_CURSOR_CLIENT_BUFFERED 的缩写形式。|  
  
如果查询生成多个结果集，则 Scrollable  选项适用于所有结果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>在结果集中选择行  
创建结果集后，可以使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)、[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) 或 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) 来指定某一行。  
  
下表介绍了可以在 row  参数中指定的值。  
  
|参数|说明|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一行。 如果未为可滚动结果集指定 row  参数，则此值为默认值。|  
|SQLSRV_SCROLL_PRIOR|指定当前行之前的行。|  
|SQLSRV_SCROLL_FIRST|指定结果集中的第一行。|  
|SQLSRV_SCROLL_LAST|指定结果集中的最后一行。|  
|SQLSRV_SCROLL_ABSOLUTE|指定使用 offset  参数指定的行。|  
|SQLSRV_SCROLL_RELATIVE|指定从当前行使用 offset  参数指定的行。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>服务器端游标和 SQLSRV 驱动程序  
下面的示例显示了各种游标的效果。 在示例的第 33 行，你会看到指定不同游标的三个查询语句中的第一个。  其中有两个查询语句被注释掉。 每次运行该程序时，使用不同的游标类型来查看第 47 行上数据库更新的效果。  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>客户端游标和 SQLSRV 驱动程序  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版本中添加了客户端游标功能，使用此功能可以在内存中缓存整个结果集。 使用客户端游标执行查询后，提供行计数。  
  
客户端游标应用于中小型结果集。 对大型结果集使用服务器端游标。  
  
如果缓冲区的大小不足以容纳整个结果集，查询将返回 false。 可以将缓冲区大小增加到 PHP 内存限制。  
  
使用 SQLSRV 驱动程序，可以使用 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 的 ClientBufferMaxKBSize 设置来配置用于保存结果集的缓冲区大小。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) 返回 ClientBufferMaxKBSize 的值。 还可以使用 sqlsrv.ClientBufferMaxKBSize 在 php.ini 文件中设置最大缓冲区大小（例如，sqlsrv.ClientBufferMaxKBSize = 1024）。  
  
以下示例显示：  
  
-   使用客户端游标时，始终提供行计数。  
  
-   使用客户端游标和批处理语句。  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
下面的示例演示了使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和不同客户端缓冲区大小的客户端游标。
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
