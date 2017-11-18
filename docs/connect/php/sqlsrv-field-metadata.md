---
title: "sqlsrv_field_metadata |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f7591043014153eb27863b12849aea4e4166639
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索已准备语句的字段的元数据。 有关准备语句的信息，请参阅 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。 请注意， **sqlsrv_field_metadata**可以对任何已准备的语句，预或执行后调用。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameters  
*$stmt*：寻找字段元数据的语句资源。  
  
## <a name="return-value"></a>返回值  
数组的 **array** 或 **false**。 数组由结果集中的每个字段的一个数组组成。 每个子数组具有下表中所述的键。 如果在检索字段元数据时出现错误，则返回 **false** 。  
  
|Key|说明|  
|-------|---------------|  
|名称|字段对应的列的名称。|  
|类型|对应于 SQL 类型的数值。|  
|Size|字符类型（char(n)、varchar(n)、nchar(n)、nvarchar(n)、XML）的字段的字符数。 二进制类型（binary(n)、varbinary(n)、UDT）的字段的字节数。 **NULL** 用于其他 SQL Server 数据类型。|  
|精度|变量精度类型（real、numeric、decimal、datetime2、datetimeoffset 和 time）的精度。 **NULL** 用于其他 SQL Server 数据类型。|  
|小数位数|变量小数位数类型（numeric、decimal、datetime2、datetimeoffset 和 time）的小数位数。 **NULL** 用于其他 SQL Server 数据类型。|  
|可以为 Null|枚举的值，该值指示列是否可以为 null (**SQLSRV_NULLABLE_YES**)，该列不是可以为 null (**SQLSRV_NULLABLE_NO**)，或者不知道如果列可以为 null (**SQLSRV_NULLABLE_UNKNOWN**)。|  
  
下表提供有关每个子数组的键的详细信息（有关这些类型的详细信息，请参阅 SQL Server 文档）：  
  
|SQL Server 2008 数据类型|类型|最小/最大精度|最小/最大小数位数|Size|  
|-----------------------------|--------|----------------------|------------------|--------|  
|bigint|SQL_BIGINT (-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|date|SQL_TYPE_DATE (91)|10/10|0/0||  
|datetime|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|decimal|SQL_DECIMAL (3)|1/38|0/精度值||  
|float|SQL_FLOAT (6)|4/8|||  
|图像|SQL_LONGVARBINARY (-4)|||2 GB|  
|int|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|nchar|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|numeric|SQL_NUMERIC (2)|1/38|0/精度值||  
|nvarchar|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|smallint|SQL_SMALLINT (5)|||2 字节|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 字节|  
|tinyint|SQL_TINYINT (-6)|||1 字节|  
|udt|SQL_SS_UDT (-151)|||变量|  
|uniqueidentifier|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) 零 (0) 指示允许最大大小。  
  
可以为 Null 的键可能为是或否。  
  
## <a name="example"></a>示例  
以下示例创建语句资源，然后检索并显示字段元数据。 该示例假定已在本地计算机上安装了 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 数据库。 当从命令行运行该示例时，所有输出都将写入控制台。  
  
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
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[文档中相关的代码示例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

