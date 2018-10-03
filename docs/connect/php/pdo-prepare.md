---
title: 'Pdo:: prepare |Microsoft Docs'
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca5e1a4d0dd3f76b3fabefa6549eb644a894845a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745135"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

准备语句用于执行。  
  
## <a name="syntax"></a>语法  
  
```  
  
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )  
```  
  
#### <a name="parameters"></a>Parameters  
$*statement*：包含 SQL 语句的字符串。  
  
key_pair：包含属性名称和值的数组。 有关详细信息，请参阅“备注”部分。  
  
## <a name="return-value"></a>返回值  
如果成功，则返回 PDOStatement 对象。 如果失败，则返回 PDOException 对象或 False，具体取决于 PDO::ATTR_ERRMODE 的值。  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 在执行已准备的语句之前不会对其进行评估。  
  
下表列出可能的 key_pair 值。  
  
|Key|描述|  
|-------|---------------|  
|PDO::ATTR_CURSOR|指定游标行为。 默认值为 PDO::CURSOR_FWDONLY。 PDO::CURSOR_SCROLL 是静态游标。<br /><br />例如， `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`。<br /><br />如果使用 PDO::CURSOR_SCROLL，你可以使用下方介绍的 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE。<br /><br />有关 PDO_SQLSRV 驱动程序中的结果集和游标的详细信息，请参阅[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::ATTR_EMULATE_PREPARES|默认情况下，此属性为 false，这可以更改此`PDO::ATTR_EMULATE_PREPARES => true`。 请参阅[模拟准备](#emulate-prepare)有关详细信息和示例。|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8（默认值）<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|如果为 Ture，则指定直接查询执行。 False 表示已准备的语句执行。 有关 PDO::SQLSRV_ATTR_DIRECT_QUERY 的详细信息，请参阅 [PDO_SQLSRV 驱动程序中的直接语句执行和已准备的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|有关详细信息，请参阅 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)。|  
  
如果使用 PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL，你可以使用 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE。 例如，  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
下表显示 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE 的可能值。  
  
|ReplTest1|描述|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|创建客户端（缓冲）静态游标。 有关客户端游标的详细信息，请参阅[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_CURSOR_DYNAMIC|创建服务器端（无缓冲）动态游标，该游标支持你采用任意顺序访问行，并且可以反映数据库中的更改。|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|创建服务器端键集游标。 如果从表中删除某一行，键集游标不会更新行计数（将返回不含任何值的已删除行）。|  
|PDO::SQLSRV_CURSOR_STATIC|创建服务器端静态游标，该游标支持你采用任意顺序访问行，但不会反映数据库中的更改。<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL 暗指 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC。|  
  
通过将 PDOStatement 对象设置为 NULL 来将其关闭。  
  
## <a name="example"></a>示例  
本示例演示如何将 PDO::prepare 方法与参数标记以及只进游标结合使用。  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table1(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
echo "\n";  
  
$query = "insert into Table1(col1, col2) values(:col1, :col2)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );  
print $stmt->rowCount();  
  
$stmt = null  
?>  
```  

## <a name="example"></a>示例  
本示例演示如何将 PDO::prepare 方法与客户端游标结合使用。 有关展示服务器端游标的示例，请参阅[游标类型（PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  

<a name="emulate-prepare" />

## <a name="example"></a>示例 

此示例演示如何使用 pdo:: prepare 方法与`PDO::ATTR_EMULATE_PREPARES`设置为 true。 

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL, 
                                          [name] nvarchar(max))", 
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

PDO_SQLSRV 驱动程序在内部使用的绑定的参数替换所有占位符[PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md)。 因此，没有占位符包含的 SQL 查询字符串发送到服务器。 请考虑此示例中，

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

使用`PDO::ATTR_EMULATE_PREPARES`设置为 false （默认情况下），发送到数据库的数据是：

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

服务器将执行查询使用的绑定参数其参数化的查询的功能。 但是，与`PDO::ATTR_EMULATE_PREPARES`实质上是设置为 true，发送到服务器的查询：

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

设置`PDO::ATTR_EMULATE_PREPARES`为 true 可以绕过 SQL Server 中的一些限制。 例如，SQL Server 不支持某些 TRANSACT-SQL 子句中已命名或位置参数。 此外，SQL Server 的绑定 2100年参数的限制。

> [!NOTE]
> Emulate 准备设置为 true，参数化查询的安全性不起作用。 因此，应用程序应确保绑定到参数的数据不包含恶意 Transact-SQL 代码。

### <a name="encoding"></a>编码

如果用户想要将具有不同的编码 （例如，utf-8 或二进制文件） 的参数绑定，用户应明确指定编码在 PHP 脚本中。

PDO_SQLSRV 驱动程序首先检查中指定的编码`PDO::bindParam()`(例如， `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`)。 

如果找不到，该驱动程序会检查如果中设置任何编码`PDO::prepare()`或`PDOStatement::setAttribute()`。 否则，该驱动程序将使用中指定的编码`PDO::__construct()`或`PDO::setAttribute()`。

### <a name="limitations"></a>限制

正如您所看到的在内部将绑定通过驱动程序。 执行不带任何参数的情况下，有效的查询发送到服务器。 与一般情况相比，不使用参数化的查询功能时产生一些限制。

- 它并不适用于参数绑定为`PDO::PARAM_INPUT_OUTPUT`。
    - 当用户指定了`PDO::PARAM_INPUT_OUTPUT`在`PDO::bindParam()`，PDO 异常。
- 不适用于参数绑定为输出参数。
    - 用户创建时已准备的语句使用占位符，用于输出参数 (即，紧接着占位符时遇到一个等号，如`SELECT ? = COUNT(*) FROM Table1`)，将 PDO 引发异常。
    - 当已准备的语句作为输出参数的参数调用存储的过程与占位符时，将不引发任何异常，因为该驱动程序无法检测到的输出参数。 但是，用户提供的输出参数的变量将保持不变。
- 不起作用的二进制编码参数重复的占位符

## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
