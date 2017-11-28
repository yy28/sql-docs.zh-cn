---
title: "如何： 执行事务 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a759dbf523ff275f20436919b5f093225b2693e5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-perform-transactions"></a>如何：执行事务
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驱动程序提供以下三个函数来执行事务：  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
PDO_SQLSRV 驱动程序提供以下三种方法来执行事务：  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
有关示例，请参阅 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
此主题的其余部分介绍并演示了如何使用 SQLSRV 驱动程序执行事务。  
  
## <a name="remarks"></a>注释  
如下概述执行事务的步骤：  
  
1.  使用 **sqlsrv_begin_transaction**开始事务。  
  
2.  检查每次查询（事务的一部分）是成功还是失败。  
  
3.  在适当情况下，使用 **sqlsrv_commit**开始事务。 否则，使用 **sqlsrv_rollback**开始事务。 在调用**sqlsrv_commit**或**sqlsrv_rollback**，驱动程序返回到自动提交模式。  
  
    默认情况下，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]处于自动提交模式。 这意味着，除非使用 **sqlsrv_begin_transaction**开始事务。  
  
    如果未使用 **sqlsrv_commit**提交显式事务，在关闭脚本的连接或终止后，将回退显式事务。  
  
    不要使用嵌入式 Transact-SQL 来执行事务。 例如，不要以 Transact-SQL 查询的方式执行包含“BEGIN TRANSACTION”的语句来开始某一事务。 使用嵌入式 Transact-SQL 执行事务时，无法保证出现预期的事务行为。  
  
    应使用前面列出的 **sqlsrv** 函数执行事务。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
以下示例将多个查询作为事务的一部分执行。 如果所有查询均成功完成，将提交事务。 如果任一查询失败，将回退事务。  
  
此示例尝试从 *Sales.SalesOrderDetail* 表中删除销售订单并针对销售订单中的每个产品调整 *Product.ProductInventory* 表中的产品库存级别。 这些查询包含在一个事务中，因为所有查询都必须成功完成，数据库才能准确反映订单状态和产品供应情况。  
  
示例中的第一个查询会为指定的销售订单 ID 检索产品 ID 和数量。 此查询不是事务的一部分。 但是，如果此查询失败，脚本将结束，因为需要产品 ID 和数量才能完成属于后续事务的查询。  
  
随后的查询（删除销售订单和更新产品库存数量）是事务的一部分。  
  
该示例假定本地计算机上已安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
### <a name="code"></a>代码  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>注释  
为了重点介绍事务行为，上面的示例中未包含一些建议的错误处理。 对于生产应用程序，我们建议应检查对 **sqlsrv** 函数的任何调用是否存在错误并进行相应处理。  
  
## <a name="see-also"></a>另请参阅  
[更新数据（Microsoft Drivers for PHP for SQL Server）](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[事务 （数据库引擎）](http://go.microsoft.com/fwlink/?LinkId=105862)  
[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
