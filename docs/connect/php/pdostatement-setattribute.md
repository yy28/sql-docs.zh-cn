---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5c5c0670ceb9725c04a63a59a09b25cf72c810
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925259"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

设置预定义的 PDO 属性或自定义驱动程序属性的属性值。  
  
## <a name="syntax"></a>语法  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>parameters  
$  attribute：一个整数，PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常量之一。 请参阅可用属性列表的“备注”部分。  
  
$value：为指定的 $attribute 设置的（混合）值   。  
  
## <a name="return-value"></a>返回值  
如果成功，则为 TRUE；否则为 FALSE。  
  
## <a name="remarks"></a>备注  
下表包含可用属性列表：  
  
|Attribute|值|说明|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 到 PHP 内存限制。|配置保留客户端游标的结果集的缓冲区大小。<br /><br />默认值为 10240 KB (10 MB)。<br /><br />有关客户端游标的详细信息，请参阅[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DATA_CLASSIFICATION|True 或 False|指定在调用 [PDOStatement::getColumnMeta](../../connect/php/pdostatement-getcolumnmeta.md) 时是否检索数据分类元数据。 默认值为 false。|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|介于 0 和 4 之间（含 0 和 4）的整数|指定设置提取的 Money 值格式时的小数位数。<br /><br />将忽略任何负整数或大于 4 的值。<br /><br />此选项仅在 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 为 true 时适用。<br /><br />还可以在连接级别设置此选项。 如果是这样，此选项将覆盖连接级别选项。<br /><br />有关详细信息，请参阅[设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8（默认值）<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|设置驱动程序用于与服务器通信的字符集编码。|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|True 或 False|指定是否以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 对象形式检索日期和时间类型。 如果保留 false，则默认行为是将它们作为字符串返回。<br /><br />还可以在连接级别设置此选项。 如果是这样，此选项将覆盖连接级别选项。<br /><br />有关详细信息，请参阅[如何：使用 PDO_SQLSRV 驱动程序以 PHP DateTime 对象形式检索日期和时间类型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|True 或 False|处理带有数值 SQL 类型（bit、integer、smallint、tinyint、float 或 real）的列的数值提取。<br /><br />当打开了连接选项标志 ATTR_STRINGIFY_FETCHES，返回值将是一个字符串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于打开状态。<br /><br />如果绑定列中返回的 PDO 类型是 PDO_PARAM_INT，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于关闭状态，整数列的返回值也是 int。|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|True 或 False|指定是否在合适时向十进制字符串添加前导零。 如已设置，此选项将启用用于设置 Money 类型格式的 PDO::SQLSRV_ATTR_DECIMAL_PLACES 选项。 如果保留 false，使用的默认行为是返回精确的精度，并为小于 1 的值省略前导零。<br /><br />还可以在连接级别设置此选项。 如果是这样，此选项将覆盖连接级别选项。<br /><br />有关详细信息，请参阅[设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|设置查询超时（以秒为单位）。<br /><br />默认情况下，驱动程序将无限期等待结果。 不允许使用负数。<br /><br />0 表示没有超时。|  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
