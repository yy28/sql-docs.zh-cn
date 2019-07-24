---
title: 直接语句预定义语句执行 PDO_SQLSRV 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993619"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 驱动程序中的直接语句执行和预定语句执行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题讨论如何使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 属性指定直接语句执行而非默认执行，即已准备的语句执行。 如果使用参数绑定多次执行语句, 则使用预定义语句可以提高性能。  
  
## <a name="remarks"></a>Remarks  
如果要将[!INCLUDE[tsql](../../includes/tsql-md.md)]语句直接发送到服务器, 而不使用驱动程序的语句准备, 则可以使用[pdo:: setAttribute](../../connect/php/pdo-setattribute.md) (或传递给[pdo:: __construct 的驱动程序选项) 设置 pdo:: SQLSRV_ATTR_DIRECT_QUERY 属性。](../../connect/php/pdo-construct.md)) 或调用[PDO::p 准备](../../connect/php/pdo-prepare.md)。 默认情况下, PDO:: SQLSRV_ATTR_DIRECT_QUERY 的值为 False (使用准备好的语句执行)。  
  
如果你使用[PDO:: query](../../connect/php/pdo-query.md), 你可能希望直接执行。 调用[pdo:: query](../../connect/php/pdo-query.md)之前, 请调用[Pdo:: setAttribute](../../connect/php/pdo-setattribute.md) , 并将 pdo:: SQLSRV_ATTR_DIRECT_QUERY 设置为 True。  对于 PDO:: SQLSRV_ATTR_DIRECT_QUERY, 每次调用[pdo:: query](../../connect/php/pdo-query.md)都可以执行不同的设置。  
  
如果你使用[PDO::p 准备](../../connect/php/pdo-prepare.md)和[PDOStatement:: execute](../../connect/php/pdostatement-execute.md)来多次使用绑定参数执行查询, 则已准备的语句执行会优化重复查询的执行。  在这种情况下, 请在驱动程序选项数组参数中调用 pdo: [:p 准备](../../connect/php/pdo-prepare.md), 并将 pdo:: SQLSRV_ATTR_DIRECT_QUERY 设置为 False。 必要时, 可以执行将 PDO:: SQLSRV_ATTR_DIRECT_QUERY 设置为 False 的预定义语句。  
  
调用 PDO 后[::p 准备](../../connect/php/pdo-prepare.md), 则在执行已准备的查询时, PDO:: SQLSRV_ATTR_DIRECT_QUERY 的值将无法更改。  
  
如果查询需要在上一个查询中设置的上下文, 则使用 "PDO:: SQLSRV_ATTR_DIRECT_QUERY" 设置为 "True" 执行查询。 例如, 如果在查询中使用临时表, PDO:: SQLSRV_ATTR_DIRECT_QUERY 必须设置为 True。  
  
下面的示例显示当需要上一个语句的上下文时, 需要将 PDO:: SQLSRV_ATTR_DIRECT_QUERY 设置为 True。 此示例使用临时表, 这些表仅在直接执行查询时对程序中的后续语句可用。  
  
> [!NOTE]
> 如果查询调用存储过程, 并且在此存储过程中使用临时表, 请改用[PDO:: exec](../../connect/php/pdo-exec.md) 。

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
[Microsoft Driver for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
