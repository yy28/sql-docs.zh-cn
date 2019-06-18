---
title: 如何：使用 PDO_SQLSRV 驱动程序以 PHP DateTime 对象形式检索日期和时间类型 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 54e5b5c9c1ba59ed64db740fbbb1a643e7cb1b2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63210440"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>如何：使用 PDO_SQLSRV 驱动程序以 PHP DateTime 对象形式检索日期和时间类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

当使用 PDO_SQLSRV 驱动程序时，版本 5.6.0 中, 添加了此功能才有效[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>若要作为 DateTime 对象中检索日期和时间类型

当使用 PDO_SQLSRV，日期和时间类型 (**smalldatetime**， **datetime**，**日期**，**时间**， **datetime2**，并**datetimeoffset**) 在默认情况下以字符串形式返回。 PDO::ATTR_STRINGIFY_FETCHES 和 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 属性都不起作用。 为了形式检索日期和时间类型[PHP DateTime](http://php.net/manual/en/class.datetime.php)对象，设置连接或语句属性`PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE`到**true** (它是**false**默认情况下)。

> [!NOTE]
> 此连接或语句属性仅应用到正则提取的日期和时间类型因为 DateTime 对象不能指定为输出参数。

## <a name="example---use-the-connection-attribute"></a>示例-使用连接属性
下面的示例省略了错误检查，为清楚起见。 此演示如何设置连接属性：

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>示例-使用语句属性
此示例演示如何设置语句属性：

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>示例-使用语句选项
或者，可以作为一个选项设置语句属性：

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>示例-以字符串形式检索日期时间类型
下面的示例说明了如何完成相反 （这是不真正必要因为它是默认值为 false）：

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>另请参阅
[检索数据](../../connect/php/retrieving-data.md)

[使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)