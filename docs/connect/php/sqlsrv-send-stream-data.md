---
title: sqlsrv_send_stream_data | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_send_stream_data
apitype: NA
helpviewer_keywords:
- sqlsrv_send_stream_data
- API Reference, sqlsrv_send_stream_data
- streaming data
ms.assetid: 826c2d45-694f-42b8-b12b-cd4523a31883
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d20cba8eb5e6b9cd5a6c30142ac3b06d2ad57af
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782770"
---
# <a name="sqlsrvsendstreamdata"></a>sqlsrv_send_stream_data
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

将数据从参数流发送至服务器。 每次调用 sqlsrv_send_stream_data  时，最多可以发送八千字节 (8K) 的数据。  
  
> [!NOTE]  
> 默认情况下，当执行查询时，所有流数据都将发送到服务器。 如果未更改此默认行为，则无需使用 **sqlsrv_send_stream_data** 来向服务器发送流数据。 有关更改默认行为的信息，请参阅 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)的“参数”部分。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_send_stream_data( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameters  
*$stmt*：对应于已执行语句的语句资源。  
  
## <a name="return-value"></a>返回值  
布尔：如果有更多数据需要发送，则为 **true** 。 否则为 **false**。  
  
## <a name="example"></a>示例  
下面的示例将以流的形式打开产品评论，并将其发送到服务器。 禁用执行时发送所有流数据的默认行为。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 数据库。 从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if ($conn === false) {
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql = "UPDATE Production.ProductReview   
         SET Comments = (?)   
         WHERE ProductReviewID = 3";  
  
/* Open parameter data as a stream and put it in the $params array. */
$data = 'Insert any lengthy comment here.';
$comment = fopen('data:text/plain,'.urlencode($data), 'r');
$params = array(&$comment);
  
/* Prepare the statement. Use the $options array to turn off the  
default behavior, which is to send all stream data at the time of query  
execution. */  
$options = array("SendStreamParamsAtExec"=>0);  
$stmt = sqlsrv_prepare($conn, $tsql, $params, $options);
  
/* Execute the statement. */  
sqlsrv_execute( $stmt);  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while (sqlsrv_send_stream_data($stmt)) {
      echo "$i call(s) made.\n";  
      $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  

[更新数据（Microsoft Drivers for PHP for SQL Server）](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
