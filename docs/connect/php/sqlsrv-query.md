---
title: "sqlsrv_query |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1dbc5c20a1d9fb1210bb7729f36299ea4392ebc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

准备并执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_query( resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parameters  
*$conn*：与已准备的语句相关联的连接资源。  
  
*$tsql*： 对应于已准备的语句的 TRANSACT-SQL 表达式。  
  
*$params* [可选]:**数组**的对应参数化查询中的参数的值。 该阵列的每个元素可以是以下项之一：  
  
-   文字值。  
  
-   PHP 变量。  
  
-   具有以下结构的 **阵列** ：  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    下表提供对阵列的每个元素的描述：  
  
    |元素|说明|  
    |-----------|---------------|  
    |*$value*|参数值、PHP 变量或通过引用传递的 PHP 变量。|  
    |*$direction*[可选]|以下项之一**SQLSRV_PARAM_\* **常量用于指示参数方向： **SQLSRV_PARAM_IN**， **SQLSRV_PARAM_OUT**， **SQLSRV_PARAM_INOUT**。 默认值是**SQLSRV_PARAM_IN**。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[可选]|A **SQLSRV_PHPTYPE_\* **指定 PHP 数据类型的返回值的常量。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$sqlType*[可选]|A **SQLSRV_SQLTYPE_\* **常量，用于指定输入值的 SQL Server 数据类型。<br /><br />有关 PHP 常量的详细信息，请参阅[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
  
*$options* [可选]: 用于设置查询属性的关联数组。 支持的键如下：  
  
|Key|支持的值|说明|  
|-------|--------------------|---------------|  
|QueryTimeout|正整数值。|设置查询超时（以秒为单位）。 默认情况下，驱动程序将无限期等待结果。|  
|SendStreamParamsAtExec|**true** 或 **false**<br /><br />默认值为 **true**。|配置要发送所有流在执行数据的驱动程序 (**true**)，或将流数据发送消息块 (**false**)。 默认情况下，该值设置为 **true**。 有关详细信息，请参阅 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可滚动|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|有关这些值的详细信息，请参阅 [指定游标类型和选择行](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>返回值  
语句资源。 如果该语句不能进行创建和/或执行， **false**返回。  
  
## <a name="remarks"></a>注释  
**Sqlsrv_query**函数非常适合一次性查询，并应为执行查询，除非特殊情况下应用的默认选项。 此函数提供了一个简化的方法，以便使用最少的代码来执行查询。 **Sqlsrv_query**函数不会语句准备和语句执行，并可用于执行参数化的查询。  
  
有关详细信息，请参阅 [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>示例  
在下面的示例中，向 AdventureWorks 数据库的 *Sales.SalesOrderDetail* 表格中插入单个行。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
> [!NOTE]  
> 虽然下面的示例使用 INSERT 语句演示了利用**sqlsrv_query**对于一次性语句的执行，这一概念适用于任何 Transact SQL 语句。  
  
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
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if( $stmt )  
{  
     echo "Row successfully inserted.\n";  
}  
else  
{  
     echo "Row insertion failed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>示例  
下面的示例将更新 AdventureWorks 数据库的 *Sales.SalesOrderDetail* 表格中的字段。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ( ?)   
         WHERE SalesOrderDetailID = ( ?)";  
  
/* Assign literal parameter values. */  
$params = array( 5, 10);  
  
/* Execute the query. */  
if( sqlsrv_query( $conn, $tsql, $params))  
{  
      echo "Statement executed.\n";  
}   
else  
{  
      echo "Error in statement execution.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[如何：执行参数化查询](../../connect/php/how-to-perform-parameterized-queries.md)  
[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
[如何：以流的形式发送数据](../../connect/php/how-to-send-data-as-a-stream.md)  
[使用方向参数](../../connect/php/using-directional-parameters.md)  
  

