---
title: 指示语句的准备语句执行 PDO_SQLSRV 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca5e180f38ad82621880e1e6aaab9cdc4b43cfc2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 驱动程序中的直接语句执行和预定语句执行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

讨论如何使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 属性指定直接语句执行而非默认执行，即已准备的语句执行。 如果不止一次使用参数绑定执行语句，则将使用已准备的语句可以导致更好的性能。  
  
## <a name="remarks"></a>Remarks  
如果你想要发送[!INCLUDE[tsql](../../includes/tsql_md.md)]直接向服务器而无需由驱动程序的语句准备的语句，你可以设置与该 PDO::SQLSRV_ATTR_DIRECT_QUERY 属性[pdo:: setattribute](../../connect/php/pdo-setattribute.md) （或驱动程序选项传递给[:: __Construct](../../connect/php/pdo-construct.md)) 或当调用[pdo:: prepare](../../connect/php/pdo-prepare.md)。 默认情况下，PDO::SQLSRV_ATTR_DIRECT_QUERY 的值为 False （准备的语句执行时使用）。  
  
如果你使用[pdo:: query](../../connect/php/pdo-query.md)，你可能想直接执行。 之前调用[pdo:: query](../../connect/php/pdo-query.md)，调用[pdo:: setattribute](../../connect/php/pdo-setattribute.md)并且 PDO::SQLSRV_ATTR_DIRECT_QUERY 设置为 True。  每次调用[pdo:: query](../../connect/php/pdo-query.md)为 PDO::SQLSRV_ATTR_DIRECT_QUERY 可以具有不同设置执行。  
  
如果你使用[pdo:: prepare](../../connect/php/pdo-prepare.md)和[pdostatement:: Execute](../../connect/php/pdostatement-execute.md)执行多次的查询使用绑定的参数，准备的语句执行优化的重复的查询的执行。  在此情况下，调用[pdo:: prepare](../../connect/php/pdo-prepare.md)与 PDO::SQLSRV_ATTR_DIRECT_QUERY 驱动程序选项数组参数中设置为 False。 如有必要，你可以执行已准备的语句与 PDO::SQLSRV_ATTR_DIRECT_QUERY 设置为 False。  
  
调用后[pdo:: prepare](../../connect/php/pdo-prepare.md)，PDO::SQLSRV_ATTR_DIRECT_QUERY 的值不能更改时执行已准备的查询。  
  
如果查询需要在前面的查询中所设置的上下文，然后执行您的查询与 PDO::SQLSRV_ATTR_DIRECT_QUERY 设置为 True。 例如，如果在查询中使用临时表，PDO::SQLSRV_ATTR_DIRECT_QUERY 必须设置为 True。  
  
下面的示例演示了需要从上一条语句的上下文时，你需要将 PDO::SQLSRV_ATTR_DIRECT_QUERY 设置为 True。  此示例使用临时表，直接执行查询时才可用于在程序中后面的语句。  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[For PHP for SQL Server 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
