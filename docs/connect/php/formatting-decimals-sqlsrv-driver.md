---
title: 设置十进制字符串和 Money 值格式（SQLSRV 驱动程序）| Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676516"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>设置十进制字符串和 Money 值格式（SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

若要保留的准确性， [decimal 或 numeric 类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)始终提取为确切的精度和规模的字符串。 如果数值为小于 1，表示缺少前导零。 它也同样适用于 money 和 smallmoney 字段，因为它们是具有固定小数位数等于 4 的十进制字段中。

## <a name="add-leading-zeroes-if-missing"></a>如果缺少，添加前导零
从版本 5.6.0，选项`FormatDecimals`添加到 sqlsrv 连接和语句级别中，这样用户就可以设置十进制字符串的格式。 此选项需要布尔值 （true 或 false），并且只影响在提取结果中的 decimal 或 numeric 值的格式设置。 换而言之，`FormatDecimals`选项没有任何影响插入或更新等其他操作。

默认情况下，`FormatDecimals` 为 false。 如果设置为 true，到十进制字符串的前导零将添加对任何十进制值小于 1。

## <a name="configure-number-of-decimal-places"></a>配置的小数位数
与`FormatDecimals`开启，另一个选项， `DecimalPlaces`，允许用户显示 money 和 smallmoney 数据时配置的小数位数。 它接受的范围内的整数值 [0，4]，并舍入显示时可能会发生。 但是，底层的 money 数据保持不变。

这两个选项可设置为连接或语句级别，并且语句始终设置将替代相应的连接设置。 请注意，`DecimalPlaces`选项**仅**影响 money 数据并`FormatDecimals`必须设置为 true 的`DecimalPlaces`才会生效。 否则，格式设置处于关闭状态而不考虑`DecimalPlaces`设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段有规模 4，设置`DecimalPlaces`为任意负数或大于 4 将被忽略的任何值的值。 建议不要以任何格式化的 money 数据用作输入到任何计算。

## <a name="example---a-simple-fetch"></a>示例-简单读取
下面的示例演示如何在简单提取中使用新的选项。

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>示例-格式输出参数
如果返回为 decimal 或 numeric 字段[输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)，返回的值将视为正则 varchar 字符串。 但是，如果指定了 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC，可以设置`FormatDecimals`为 true，以确保没有任何缺少的前导零的数字的字符串值。 有关详细信息，请参阅[如何：使用 SQLSRV 驱动程序检索输出参数](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下面的示例演示如何设置返回 decimal(8,4) 值的存储过程的输出参数的格式。

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>另请参阅
[设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[检索数据](../../connect/php/retrieving-data.md)
