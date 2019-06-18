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
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669692"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>设置十进制字符串和 Money 值格式（PDO_SQLSRV 驱动程序）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

若要保留的准确性， [decimal 或 numeric 类型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)始终提取为确切的精度和规模的字符串。 如果数值为小于 1，表示缺少前导零。 它也同样适用于 money 和 smallmoney 字段，因为它们是具有固定小数位数等于 4 的十进制字段中。

## <a name="add-leading-zeroes-if-missing"></a>如果缺少，添加前导零
从 5.6.0 版本、 连接或语句属性`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`允许用户设置十进制字符串的格式。 此属性需要布尔值 （true 或 false），并且只会影响中提取结果的 decimal 或 numeric 值的格式。 换而言之，此属性具有对其他操作，例如插入或更新没有影响。

默认情况下，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 为 false  。 如果设置为 true，到十进制字符串的前导零将添加对任何十进制值小于 1。

## <a name="configure-number-of-decimal-places"></a>配置的小数位数
与`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`开启连接或语句的另一个属性， `PDO::SQLSRV_ATTR_DECIMAL_PLACES`，允许用户显示 money 和 smallmoney 数据时配置的小数位数。 它接受的范围内的整数值 [0，4]，并舍入显示时可能会发生。 但是，底层的 money 数据保持不变。

语句属性始终重写相应的连接设置。 请注意，`PDO::SQLSRV_ATTR_DECIMAL_PLACES`选项**仅**影响 money 数据和`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`必须设置为 true。 否则，格式设置处于关闭状态而不考虑`PDO::SQLSRV_ATTR_DECIMAL_PLACES`设置。

> [!NOTE]
> 由于 money 或 smallmoney 字段有规模 4，设置`PDO::SQLSRV_ATTR_DECIMAL_PLACES`为任意负数或大于 4 将被忽略的任何值。 建议不要以任何格式化的 money 数据用作输入到任何计算。

### <a name="to-set-the-connection-attributes"></a>若要设置连接属性

-   在连接时设置属性：

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Post 连接设置属性：

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>示例-格式 money 数据
下面的示例显示如何提取资金数据使用[pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>示例-重写连接属性
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
