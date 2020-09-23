---
title: 如何：使用 PDO_SQLSRV 驱动程序以 PHP Datetime 对象形式检索日期和时间类型
description: 本主题介绍在使用 Microsoft PDO_SQLSRV Driver for PHP for SQL Server 时，如何将日期和时间类型作为 PHP DateTime 对象进行检索
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 507dc2a228419fb695d10a437681229ec6586f11
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680752"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdo_sqlsrv-driver"></a>如何：使用 PDO_SQLSRV 驱动程序以 PHP DateTime 对象形式检索日期和时间类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此功能已在版本 5.6.0 中添加，仅在针对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 PDO_SQLSRV 驱动程序时才有效。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>以 DateTime 对象形式检索日期和时间类型

使用 PDO_SQLSRV 时，日期和时间类型（smalldatetime****、datetime****、date****、time****、datetime2**** 和 datetimeoffset****）默认情况下作为字符串返回。 PDO::ATTR_STRINGIFY_FETCHES 和 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 属性都不起作用。 若要将日期和时间类型作为 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 对象进行检索，请将连接或语句属性 `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` 设置为 true****（默认情况下为 false****）。

> [!NOTE]
> 此连接或语句属性仅适用于日期和时间类型的常规获取，因为无法将 DateTime 对象指定为输出参数。

## <a name="example---use-the-connection-attribute"></a>示例 - 使用连接属性
为清楚起见，下面的示例省略了错误检查。 此示例演示如何设置连接属性：

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

## <a name="example---use-the-statement-attribute"></a>示例 - 使用语句属性
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

## <a name="example---use-the-statement-option"></a>示例 - 使用语句选项
或者，可以将语句属性设置为选项：

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

## <a name="example---retrieve-datetime-types-as-strings"></a>示例 - 以字符串形式检索 datetime 类型
下面的示例演示如何达到相反的效果（这并不是必须的，因为默认情况下为 false）：

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
