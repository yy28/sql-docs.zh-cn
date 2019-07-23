---
title: 设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）| Microsoft Docs
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
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265154"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

为了保持准确性, 将始终以精确精度和缩放的字符串形式提取[decimal 或 numeric 类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)。 如果任何值小于 1, 则缺少前导零。 这与 money 和 smallmoney 字段相同, 因为这些字段是固定刻度等于4的小数字段。

## <a name="add-leading-zeroes-if-missing"></a>如果缺少, 则添加前导零
从版本5.6.0 开始, 连接或语句特性`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`允许用户设置十进制字符串的格式。 此属性需要一个布尔值 (true 或 false), 并且仅影响提取的结果中的十进制值或数值的格式设置。 换言之, 此属性不会对其他操作 (如插入或更新) 产生影响。

默认情况下，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 为 false  。 如果设置为 true, 则将为小于1的任何十进制值添加前导零到十进制字符串。

## <a name="configure-number-of-decimal-places"></a>配置小数位数
启用后, 另一个连接或语句`PDO::SQLSRV_ATTR_DECIMAL_PLACES`属性允许用户配置显示 money 和 smallmoney 数据时的小数位数。 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 它接受 [0, 4] 范围内的整数值, 并在显示时可能出现舍入。 但是, 基础货币数据保持不变。

语句属性始终重写相应的连接设置。 请注意,  `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`选项只影响 money 数据, 并且必须设置为 true。 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 否则, 无论`PDO::SQLSRV_ATTR_DECIMAL_PLACES`设置如何, 都将关闭格式设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段的小数位数为 4 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` , 因此设置为任何负数或大于4的任何值都将被忽略。 不建议使用任何格式的货币数据作为任何计算的输入。

### <a name="to-set-the-connection-attributes"></a>设置连接属性

-   在连接时设置属性:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   设置属性后连接:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>示例-设置货币格式的数据
下面的示例演示如何使用[PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md)提取 money 数据:

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>示例-替代连接属性
下面的示例演示如何重写连接属性:

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>另请参阅
[设置十进制字符串和 Money 值格式（SQLSRV 驱动程序）](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[检索数据](../../connect/php/retrieving-data.md)
