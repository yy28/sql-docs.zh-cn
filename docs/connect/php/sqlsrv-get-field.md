---
title: sqlsrv_get_field | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_get_field
apitype: NA
helpviewer_keywords:
- sqlsrv_get_field
- API Reference, sqlsrv_get_field
- retrieving data, as a single field
ms.assetid: fa17cc56-fb38-433b-a40d-65642f04dc23
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aea71596e1a977839fb7294df7324f48324e0c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvgetfield"></a>sqlsrv_get_field
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

从当前行的指定字段中检索数据。 必须按顺序访问字段数据。 例如，在访问第二个字段中的数据后，不能访问第一个字段中的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_get_field( resource $stmt, int $fieldIndex [, int $getAsType])  
```  
  
#### <a name="parameters"></a>Parameters  
*$stmt*：对应于已执行语句的语句资源。  
  
*$fieldIndex*：要检索的字段索引。 索引从零开始。  
  
*$getAsType* [可选]: A **SQLSRV**常量 (**SQLSRV_PHPTYPE_\***)，它确定返回的数据的 PHP 数据类型。 有关支持的数据类型的信息，请参阅[常量&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 如果没有指定返回类型，将返回默认 PHP 类型。 有关默认 PHP 类型的信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。 有关指定默认 PHP 数据类型的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
## <a name="return-value"></a>返回值  
字段数据。 使用 *$getAsType* 参数可以指定返回数据的 PHP 数据类型。 如果没有指定返回数据类型，将返回默认 PHP 数据类型。 有关默认 PHP 类型的信息，请参阅 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。 有关指定默认 PHP 数据类型的信息，请参阅 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
## <a name="remarks"></a>注释  
组合**sqlsrv_fetch**和**sqlsrv_get_field**提供对数据的只进访问权限。  
  
组合**sqlsrv_fetch**/**sqlsrv_get_field**加载到脚本内存中设置行结果的一个字段，并允许 PHP 返回类型规范。 (有关如何指定 PHP 返回类型的信息，请参阅[How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。)此函数组合还允许流式检索数据。 (有关检索数据的流形式的信息，请参阅[使用 SQLSRV 驱动程序流的形式检索数据](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)。)  
  
## <a name="example"></a>示例  
以下示例检索的数据行包含产品审核和审阅者名称。 若要从结果集中检索数据，请使用 **sqlsrv_get_field** 。 该示例假定 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)数据库安装在本地计算机上。 从命令行运行该示例时，所有输出都将写入控制台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of the SQL Server nvarchar type. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  

[检索数据](../../connect/php/retrieving-data.md)  

[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
