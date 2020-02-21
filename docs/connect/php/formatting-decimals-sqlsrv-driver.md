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
manager: v-mabarw
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68265137"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>设置十进制字符串和 Money 值格式（SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

为了保持准确性，[十进制或数字类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)始终以精确精度和数值范围的字符串形式提取。 如果任何值小于 1，则缺少前导零。 money 和 smallmoney 字段也是如此，因为这些字段是固定数值范围等于 4 的十进制字段。

## <a name="add-leading-zeroes-if-missing"></a>添加前导零（如果缺少）
从版本 5.6.0 开始，将选项 `FormatDecimals` 添加到 sqlsrv 连接和语句级别，这允许用户设置十进制字符串格式。 此选项需要一个布尔值（true 或 false），并且仅影响提取结果中的十进制值或数值的格式设置。 换言之，`FormatDecimals` 选项不会对其他操作（如插入或更新）产生影响。

默认情况下，`FormatDecimals` 为 false  。 如果设置为 true，则将为小于 1 的任何十进制值添加前导零到十进制字符串。

## <a name="configure-number-of-decimal-places"></a>配置小数位数
打开 `FormatDecimals` 后，另一个选项 `DecimalPlaces` 允许用户在显示 money 和 smallmoney 数据时配置小数位数。 它接受 [0, 4] 范围内的整数值，在显示时可能会出现舍入。 但是，基础 money 数据保持不变。

这两个选项都可以设置为连接或语句级别，并且语句设置始终会重写相应的连接设置。 请注意，`DecimalPlaces` 选项仅  影响 money 数据，并且 `FormatDecimals` 必须设置为 true 才能使 `DecimalPlaces` 生效。 否则，无论 `DecimalPlaces` 如何设置，都会关闭格式设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段的数值范围为 4，因此将 `DecimalPlaces` 值设置为负数或大于 4 的任何值都将被忽略。 不建议使用任何格式化的 money 数据作为任何计算的输入。

## <a name="example---a-simple-fetch"></a>示例 - 简单提取
下面的示例演示如何在简单提取中使用新选项。

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

## <a name="example---format-the-output-parameter"></a>示例 - 设置输出参数的格式
如果 decimal 或 numeric 字段作为[输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)返回，则返回的值将被视为常规 varchar 字符串。 但是，如果指定了 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC，则可以将 `FormatDecimals` 设置为 true，以确保数值字符串值不会缺少前导零。 有关详细信息，请参阅[如何：使用 SQLSRV 驱动程序检索输出参数](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下面的示例演示如何格式化返回十进制 (8,4) 值的存储过程的输出参数。

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
