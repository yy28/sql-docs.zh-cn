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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265137"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>设置十进制字符串和 Money 值格式（SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

为了保持准确性, 将始终以精确精度和缩放的字符串形式提取[decimal 或 numeric 类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)。 如果任何值小于 1, 则缺少前导零。 这与 money 和 smallmoney 字段相同, 因为这些字段是固定刻度等于4的小数字段。

## <a name="add-leading-zeroes-if-missing"></a>如果缺少, 则添加前导零
从版本5.6.0 开始, 将选项`FormatDecimals`添加到 sqlsrv 连接和语句级别, 这允许用户设置十进制字符串的格式。 此选项需要一个布尔值 (true 或 false), 并且仅影响提取的结果中的十进制值或数值的格式设置。 换句话说, `FormatDecimals`选项对插入或更新等其他操作不起作用。

默认情况下，`FormatDecimals` 为 false  。 如果设置为 true, 则将为小于1的任何十进制值添加前导零到十进制字符串。

## <a name="configure-number-of-decimal-places"></a>配置小数位数
启用后, 另一个`DecimalPlaces`选项允许用户在显示 money 和 smallmoney 数据时配置小数位数。 `FormatDecimals` 它接受 [0, 4] 范围内的整数值, 并在显示时可能出现舍入。 但是, 基础货币数据保持不变。

这两个选项都可以设置为连接或语句级别, 并且语句设置始终会重写相应的连接设置。 请注意`DecimalPlaces` , `FormatDecimals`  选项**只**影响money数据,并且必须`DecimalPlaces`设置为 true 才能生效。 否则, 无论`DecimalPlaces`设置如何, 都将关闭格式设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段的小数位数为 4 `DecimalPlaces` , 因此将值设置为任何负数或大于4的任何值都将被忽略。 不建议使用任何格式的货币数据作为任何计算的输入。

## <a name="example---a-simple-fetch"></a>示例-简单提取
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

## <a name="example---format-the-output-parameter"></a>示例-设置输出参数的格式
如果 decimal 或 numeric 字段作为[output 参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)返回, 则返回的值将被视为常规 varchar 字符串。 但是, 如果指定了 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC, 则可以将设置`FormatDecimals`为 true, 以确保数值字符串值不会缺少前导零。 有关详细信息，请参阅[如何：使用 SQLSRV 驱动程序检索输出参数](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下面的示例演示如何格式化返回 decimal (8, 4) 值的存储过程的 output 参数。

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
