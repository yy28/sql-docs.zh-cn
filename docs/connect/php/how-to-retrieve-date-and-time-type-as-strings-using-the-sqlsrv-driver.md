---
title: 使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 11fa40f3cdeb93463f3e5f66975e83e5d12dd6d4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797730"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

使用 SQLSRV 驱动程序时[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，可以检索日期和时间类型 (**smalldatetime**， **datetime**，**日期**，**时间**， **datetime2**，和**datetimeoffset**) 为通过指定以下选项在连接字符串中或在语句级别的字符串：

```
'ReturnDatesAsStrings'=>true
```

默认值是 false  ，这意味着 smalldatetime  、datetime  、date  、time  、datetime2  和 datetimeoffset  类型将返回为 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 对象。 如果在语句级别上设置此选项，它将覆盖连接级别设置。

PDO_SQLSRV 驱动程序默认情况下返回以字符串形式的日期和时间类型。 若要检索这些作为 PHP DateTime 对象，请参阅[如何： 检索日期和时间类型作为 PHP Datetime 对象使用 PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)

## <a name="example"></a>示例
以下示例演示的语法可用于指定要以字符串的形式检索日期和时间类型。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_close($conn);
?>
```

## <a name="example"></a>示例
以下示例演示当检索字符串时，通过指定 UTF-8 可以字符串的形式检索日期，即使连接是使用 `"ReturnDatesAsStrings" => false` 建立的也是如此。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;

sqlsrv_close($conn);
?>
```

## <a name="example"></a>示例
以下示例演示如何通过在连接字符串中指定 UTF-8 和 `"ReturnDatesAsStrings" => true` 来以字符串的形式检索日期。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8');
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;
sqlsrv_close($conn);
?>
```

## <a name="example"></a>示例
以下示例演示如何以 PHP 类型的形式检索日期。 `'ReturnDatesAsStrings'=> false` 处于打开状态。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as a DateTime object, then convert to string using PHP's date_format function
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

$date_string = date_format($date, 'jS, F Y');
echo "Date = $date_string\n";

sqlsrv_close($conn);
?>
```

## <a name="example"></a>示例
在语句级别 ReturnDatesAsStrings 选项可重写相应的连接选项。

```php
<?php
$serverName = 'MyServer';
$connectionInfo = array('Database' => 'MyDatabase', 'ReturnDatesAsStrings' => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tableName = 'MyTable';
$options = array('ReturnDatesAsStrings' => true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}
sqlsrv_execute($stmt);

// Expect the fetched value to be a string
$field = sqlsrv_get_field($stmt, 0);
echo $field . PHP_EOL;

sqlsrv_close($conn);
?>
```

## <a name="see-also"></a>另请参阅
[检索数据](../../connect/php/retrieving-data.md)

[如何：使用 PDO_SQLSRV 以 PHP Datetime 对象形式检索日期和时间类型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)
