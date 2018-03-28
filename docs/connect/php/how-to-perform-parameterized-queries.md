---
title: 如何： 执行参数化的查询 |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23660f3d7ddbaf45ac39674c4eba23092e3ae2d2
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-perform-parameterized-queries"></a>如何：执行参数化查询
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题总结并演示了如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 执行参数化查询。  
  
有关执行参数化查询的步骤可总结为四个步骤：  
  
1.  将问号 (?) 作为参数占位符放置在属于要执行查询的 Transact-SQL 字符串中。  
  
2.  初始化或更新对应于 Transact-SQL 查询中的占位符的 PHP 变量。  
  
3.  使用步骤 2 中的 PHP 变量创建或更新它们分别对应参数值的数组中的 TRANSACT-SQL 字符串参数占位符。 数组中的参数值必须为占位符用于表示它们的顺序相同。
  
4.  执行查询：  
  
    -   如果使用的是 SQLSRV 驱动程序，请使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。  
  
    -   如果你使用的 PDO_SQLSRV 驱动程序，执行查询中的使用[pdo:: prepare](../../connect/php/pdo-prepare.md)和[pdostatement:: Execute](../../connect/php/pdostatement-execute.md)。 [PDO::prepare](../../connect/php/pdo-prepare.md) 和 [PDOStatement::execute](../../connect/php/pdostatement-execute.md) 的主题有代码示例。  
  
本主题的其余部分讨论使用 SQLSRV 驱动程序的参数化查询。  
  
> [!NOTE]  
> 参数使用 **sqlsrv_prepare**。 这意味着，如果使用 **sqlsrv_prepare** 准备参数化查询并更新参数数组中的值，将在下一次执行查询时使用更新的值。 有关更多详细信息，请参阅本主题中的下一个示例。  
  
## <a name="example"></a>示例  
以下示例更新 AdventureWorks 数据库的 *Production.ProductInventory* 表中的指定产品 ID 的数量。 数量和产品 ID 是 UPDATE 查询中的参数。  
  
然后，此示例查询数据库来验证数量是否已正确更新。 产品 ID 是 SELECT 查询中的参数。  
  
该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
上一个示例使用 **sqlsrv_query** 函数来执行查询。 本功能适合用于执行一次性查询，因为它可进行语句准备和执行。 组合**sqlsrv_prepare**/**sqlsrv_execute**最适合的查询中使用不同的参数值重新执行。 若要查看使用不同的参数值重复执行查询的示例，请参阅下一个示例。  
  
## <a name="example"></a>示例  
以下示例演示使用 **sqlsrv_prepare** 函数时隐式绑定变量。 此示例将多个销售订单插入到 *Sales.SalesOrderDetail* 表中。 *$Params*数组绑定到该语句 (*$stmt*) 时**sqlsrv_prepare**调用。 在每次执行将新的销售订单插入到表中的查询时，将使用对应于销售订单详细信息的新值更新 *$params* 数组。 后续查询执行使用新的参数值。  
  
该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[转换数据类型](../../connect/php/converting-data-types.md)

[安全注意事项 Microsoft Drivers for PHP for SQL Server](../../connect/php/security-considerations-for-php-sql-driver.md)

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
