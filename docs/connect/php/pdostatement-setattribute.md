---
title: 'Pdostatement:: Setattribute |Microsoft Docs'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e3523e432c9f2f33d63c0db7ed6f64359299549
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655494"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

设置预定义的 PDO 属性或自定义驱动程序属性的属性值。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parameters  
$attribute：一个整数，PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常量之一。 请参阅可用属性列表的“备注”部分。  
  
$value：为指定的 $attribute 设置的（混合）值。  
  
## <a name="return-value"></a>返回值  
如果成功，则为 TRUE；否则为 FALSE。  
  
## <a name="remarks"></a>Remarks  
下表包含可用属性列表：  
  
|attribute|值|描述|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 到 PHP 内存限制。|配置保留客户端游标的结果集的缓冲区大小。<br /><br />默认值为 10240 KB (10 MB)。<br /><br />有关客户端游标的详细信息，请参阅[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8（默认值）<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|设置驱动程序用于与服务器通信的字符集编码。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|True 或 False|处理与数值 SQL 类型 （位、 integer、 smallint、 tinyint、 float、 或实际） 列中数值的提取操作。<br /><br />当连接选项标志 ATTR_STRINGIFY_FETCHES 上时，返回值将是一个字符串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 位于上。<br /><br />PDO_PARAM_INT 绑定列中的返回的 PDO 类型时，整数列的返回值将是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 处于关闭状态。|  
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

[PDO](http://php.net/manual/book.pdo.php)  
  
