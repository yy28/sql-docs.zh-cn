---
title: "游标类型 （SQLSRV 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92fa89c2f477b867930d1b53da7e6fa318a3d39d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-types-sqlsrv-driver"></a>游标类型 （SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 驱动程序，可以创建具有您可以以任何顺序排列，具体取决于游标类型访问的行的结果集。  本主题将讨论客户端 （缓冲式） 和服务器端 （缓冲） 游标。  
  
## <a name="cursor-types"></a>游标类型  
当你创建具有的结果集[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)，你可以指定的游标类型。 默认情况下，将使用只进游标，它可让你从结果集直到到达结果集的末尾的第一行开始一次移动一个行。  
  
你可以创建具有可滚动游标，可用于访问结果集，按任何顺序中的任意行的结果集。 下表列出的值，可传递给**可滚动**sqlsrv_query 或 sqlsrv_prepare 中的选项。  
  
|选项|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|使你可以移动一行的第一行结果集直到到达结果集的末尾处开始一次。<br /><br />这是默认游标类型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)返回结果集使用此游标类型创建一个错误。<br /><br />**转发**是 SQLSRV_CURSOR_FORWARD 的缩写的形式。|  
|SQLSRV_CURSOR_STATIC|允许你采用任意顺序访问行，但不是会反映数据库中的更改。<br /><br />**静态**是 SQLSRV_CURSOR_STATIC 的缩写的形式。|  
|SQLSRV_CURSOR_DYNAMIC|允许你采用任意顺序访问行并将反映数据库中的更改。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)返回结果集使用此游标类型创建一个错误。<br /><br />**动态**是 SQLSRV_CURSOR_DYNAMIC 的缩写的形式。|  
|SQLSRV_CURSOR_KEYSET|允许你访问行按任何顺序。 但是，键集游标不更新的行计数，如果从 （不含任何值返回已删除的行） 的表中删除行。<br /><br />**键集**是 SQLSRV_CURSOR_KEYSET 的缩写的形式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|允许你访问行按任何顺序。 创建客户端游标查询。<br /><br />**缓冲**是 SQLSRV_CURSOR_CLIENT_BUFFERED 的缩写的形式。|  
  
如果查询生成多个结果集，**可滚动**选项适用于所有结果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>在结果集中选择行  
创建一个结果集后，你可以使用[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)， [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)，或[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)要指定行。  
  
下表描述你可以在指定的值*行*参数。  
  
|参数|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一步的行。 这是默认值，如果不指定*行*参数为可滚动的结果集。|  
|SQLSRV_SCROLL_PRIOR|指定之前的当前行的行。|  
|SQLSRV_SCROLL_FIRST|指定结果集中的第一行。|  
|SQLSRV_SCROLL_LAST|指定结果集中的最后一行。|  
|SQLSRV_SCROLL_ABSOLUTE|指定使用指定的行*偏移量*参数。|  
|SQLSRV_SCROLL_RELATIVE|指定使用指定的行*偏移量*参数从当前行。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>服务器端游标和 SQLSRV 驱动程序  
下面的示例演示各种游标的效果。 在行 33 示例中，你将看到第一个三个指定不同的游标的查询语句。  两个查询语句已被注释。 每次运行该程序，使用不同的游标类型行 47 上查看的数据库更新的效果。  
  
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
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>客户端游标，SQLSRV 驱动程序  
客户端游标是一项功能的版本 3.0 中添加[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，使你能够整个结果集在内存中高速缓存。 使用客户端游标时执行查询后，行计数是可用。  
  
对于小型到中型的结果集，应使用客户端游标。 对于大型结果集使用服务器端游标。  
  
查询将返回 false 缓冲区是否不大到能够容纳整个结果集。 你可以增加最大 PHP 内存限制为缓冲区大小。  
  
使用 SQLSRV 驱动程序，你可以配置用于保留结果集的 ClientBufferMaxKBSize 设置的缓冲区的大小[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)返回 ClientBufferMaxKBSize 的值。 此外可以在 php.ini 文件中使用 sqlsrv 设置最大缓冲区大小。ClientBufferMaxKBSize (例如，sqlsrv。ClientBufferMaxKBSize = 1024年)。  
  
下面的示例演示：  
  
-   行计数时始终使用客户端游标。  
  
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
  
下面的示例演示客户端游标使用[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。  
  
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
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable"=>SQLSRV_CURSOR_CLIENT_BUFFERED));  
  
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
  

