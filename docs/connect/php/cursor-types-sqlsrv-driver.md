---
title: 游标类型 （SQLSRV 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: deffdb98790baa64eaa1983fee6839a65289d0d4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37990159"
---
# <a name="cursor-types-sqlsrv-driver"></a>游标类型（SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

通过 SQLSRV 驱动程序，可以创建能够以任何顺序访问且具有行的结果集，具体取决于游标类型。  本主题将讨论客户端 （缓冲） 以及服务器端 （缓冲） 游标。  
  
## <a name="cursor-types"></a>游标类型  
当你创建的结果集[sqlsrv_query](../../connect/php/sqlsrv-query.md)或使用[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)，可以指定的游标类型。 默认情况下，使用只进游标，它可让你从第一行的结果集直到到达结果集的末尾处开始一次移动一个行。  
  
可以创建的结果集可滚动游标，可用于访问结果集中，按任意顺序中的任意行。 下表列出了值，可传递给**可滚动**sqlsrv_query 或 sqlsrv_prepare 中的选项。  
  
|选项|描述|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|可以从第一行的结果集直到到达结果集的末尾处开始一次移动一个行。<br /><br />这是默认游标类型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)对此游标类型创建结果集返回一个错误。<br /><br />**前滚**是 SQLSRV_CURSOR_FORWARD 的缩写的形式。|  
|SQLSRV_CURSOR_STATIC|可让你采用任何顺序访问行，但不是会反映数据库中的更改。<br /><br />**静态**是 SQLSRV_CURSOR_STATIC 的缩写的形式。|  
|SQLSRV_CURSOR_DYNAMIC|可让你采用任何顺序访问行并将反映数据库中的更改。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)对此游标类型创建结果集返回一个错误。<br /><br />**动态**是 SQLSRV_CURSOR_DYNAMIC 的缩写的形式。|  
|SQLSRV_CURSOR_KEYSET|可让你访问任何顺序中的行。 然而，如果从表中删除某一行，键集游标不会更新行计数（将返回不含任何值的已删除行）。<br /><br />**由键集**是 SQLSRV_CURSOR_KEYSET 的缩写的形式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|可让你访问任何顺序中的行。 创建客户端游标查询。<br /><br />**缓冲**是 SQLSRV_CURSOR_CLIENT_BUFFERED 的缩写的形式。|  
  
如果查询生成多个结果集，**可滚动**选项适用于所有结果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>在结果集中选择行  
创建结果集后，可以使用[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)， [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)，或[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)以指定的行。  
  
下表描述了可以在指定的值*行*参数。  
  
|参数|描述|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一步的行。 这是默认值，如果未指定*行*对于可滚动结果集的参数。|  
|SQLSRV_SCROLL_PRIOR|指定在当前行前面的行。|  
|SQLSRV_SCROLL_FIRST|指定结果集中的第一行。|  
|SQLSRV_SCROLL_LAST|指定在结果集中的最后一行。|  
|SQLSRV_SCROLL_ABSOLUTE|指定使用指定的一行*偏移量*参数。|  
|SQLSRV_SCROLL_RELATIVE|指定使用指定的一行*偏移量*参数从当前行。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>服务器端游标和 SQLSRV 驱动程序  
下面的示例显示了各种游标的效果。 在该示例的第 33 行中，会看到三个指定不同的游标的查询语句的第一个。  两个查询语句被注释掉。 每次运行该程序使用不同的游标类型才能生效第 47 行上的数据库更新。  
  
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
客户端游标是一项功能的版本 3.0 中添加[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，可用于缓存整个结果集在内存中。 使用客户端游标时执行查询后，可以提供行计数。  
  
对于小型到中型的结果集，应使用客户端游标。 对于大型结果集使用服务器端游标。  
  
查询将返回 false，如果缓冲区足以容纳整个结果集。 可以增加缓冲区大小最大为 PHP 内存限制。  
  
使用 SQLSRV 驱动程序，可以配置用于保留结果集的 ClientBufferMaxKBSize 设置的缓冲区的大小[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)返回 ClientBufferMaxKBSize 的值。 此外可以在 php.ini 文件中使用 sqlsrv 设置最大缓冲区大小。ClientBufferMaxKBSize (例如，sqlsrv。ClientBufferMaxKBSize = 1024年)。  
  
下面的示例演示：  
  
-   行计数始终都可以进行客户端游标。  
  
-   客户端游标和批处理语句的使用。  
  
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
  
