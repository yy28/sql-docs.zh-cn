---
title: sqlsrv_fetch_array | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb76c3498be69a9a29525bbe96a26b94ba954af2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802280"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以数字索引的阵列、关联阵列或这两者的形式检索下一行数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>Parameters  
*$stmt*：对应于已执行语句的语句资源。  
  
$fetchType [可选]：预定义常量  。 此参数可以采用下表中列出的值之一：  
  
|ReplTest1|描述|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|下一行数据将以数值阵列的形式返回。|  
|SQLSRV_FETCH_ASSOC|下一行数据将以关联阵列的形式返回。 阵列键是结果集中的列名称。|  
|SQLSRV_FETCH_BOTH|下一行数据将以数值阵列和关联阵列的形式返回。 这是默认值。|  
  
row [可选]：版本 1.1 中已添加  。 以下值之一，用于指定要在使用可滚动游标的结果集中访问的行。 （已指定 row 时，必须显式指定 fetchtype，即使指定默认值也是如此。）    
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
有关这些值的详细信息，请参阅 [指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。 已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 1.1 中添加了对可滚动游标的支持。  
  
offset [可选]：结合使用 SQLSRV_SCROLL_ABSOLUTE 和 SQLSRV_SCROLL_RELATIVE 以指定要检索的行  。 结果集中的第一个记录为 0。  
  
## <a name="return-value"></a>返回值  
如果检索数据行，将返回 **array** 。 如果没有更多要检索的行，将返回 **NULL** 。 如果出现错误，将返回 **False** 。  
  
根据 *$fetchType* 参数的值，返回的 **阵列** 可以是数字索引的 **阵列**、关联 **阵列**或这两者。 默认情况下，将返回带有数值键和关联键的 **array** 。 返回阵列中值的数据类型将是默认 PHP 数据类型。 有关默认 PHP 数据类型的信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
## <a name="remarks"></a>Remarks  
如果返回没有名称的列，阵列元素的关联键将为空字符串 ("")。 例如，考虑可将某个值插入数据库表并检索服务器生成的主键的 Transact-SQL 语句：  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
如果此语句的 `SELECT SCOPE_IDENTITY()` 部分返回的结果集以关联阵列的形式进行检索，则返回值的键将是空字符串 ("")，因为返回的列没有名称。 若要避免出现上述情形，可以以数值阵列的形式检索该结果，或在 Transact-SQL 语句中为返回的列指定一个名称。 以下方法可用于在 Transact-SQL 中指定一个列名：  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
如果结果集包含多个不带名称的列，则最后一个未命名列的值将分配到空字符串 ("") 键。  
  
## <a name="example"></a>示例  
以下示例将每一行结果集检索为一个关联 **阵列**。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
以下示例将每一行结果集检索为一个数字索引的阵列。  
  
该示例将从产品（具有指定日期且库存量 (StockQty) 小于指定值）的 AdventureWorks 数据库的 Purchasing.PurchaseOrderDetail 表中检索产品信息   。  
  
该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
sqlsrv_fetch_array 函数将始终根据[默认 PHP 数据类型](../../connect/php/default-php-data-types.md)返回数据  。 有关如何指定 PHP 数据类型的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
如果检索没有名称的字段，阵列元素的关联键将为空字符串 ("")。 有关详细信息，请参阅 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)。  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[检索数据](../../connect/php/retrieving-data.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)

[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
