---
title: 格式化十进制字符串和货币值（PDO_SQLSRV 驱动程序）
description: 了解如何在使用 PDO_SQLSRV 驱动程序时使用 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 和 SQLSRV_ATTR_DECIMAL_PLACES 属性来格式化十进制字符串或货币值
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae61b239fca2a923645b9de963309c62a3919b3d
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680652"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

为了保持准确性，[十进制或数字类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)始终以精确精度和数值范围的字符串形式提取。 如果任何值小于 1，则缺少前导零。 money 和 smallmoney 字段也是如此，因为这些字段是固定数值范围等于 4 的十进制字段。

## <a name="add-leading-zeroes-if-missing"></a>添加前导零（如果缺少）
从版本 5.6.0 开始，连接或语句属性 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 允许用户设置十进制字符串格式。 此属性需要一个布尔值（true 或 false），并且仅影响提取结果中的十进制值或数值的格式设置。 换言之，此属性不会对其他操作（如插入或更新）产生影响。

默认情况下，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 为 false  。 如果设置为 true，则将为小于 1 的任何十进制值添加前导零到十进制字符串。

## <a name="configure-number-of-decimal-places"></a>配置小数位数
打开 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 后，另一个连接或语句属性 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 允许用户在显示 money 和 smallmoney 数据时配置小数位数。 它接受 [0, 4] 范围内的整数值，在显示时可能会出现舍入。 但是，基础 money 数据保持不变。

语句属性始终重写相应的连接设置。 请注意，`PDO::SQLSRV_ATTR_DECIMAL_PLACES` 选项仅**** 影响 money 数据，并且 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 必须设置为 true。 否则，无论 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 如何设置，都会关闭格式设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段的数值范围为 4，因此，将 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 设置为任何负数或大于 4 的任何值都将被忽略。 不建议使用任何格式化的 money 数据作为任何计算的输入。

### <a name="to-set-the-connection-attributes"></a>设置连接属性

-   在连接时设置属性：

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   设置连接后属性：

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>示例 - 设置 money 数据格式
下面的示例演示如何使用 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 提取 money 数据：

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

## <a name="example---override-connection-attributes"></a>示例 - 重写连接属性
下面的示例演示如何重写连接属性：

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
