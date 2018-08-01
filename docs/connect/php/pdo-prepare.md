---
title: 'Pdo:: prepare |Microsoft Docs'
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 717657cabc469488565985e3e37d111bb9d592b8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979762"
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
|PDO::ATTR_EMULATE_PREPARES|当 pdo:: ATTR_EMULATE_PREPARES 上时，已准备的语句中的占位符替换为绑定参数。 一个完整的 SQL 语句与没有占位符然后发送到在执行数据库。 <br /><br />可以使用 pdo:: ATTR_EMULATE_PREPARES 绕过 SQL Server 中的一些限制。 例如，SQL Server 不支持某些 TRANSACT-SQL 子句中已命名或位置参数。 此外，SQL Server 有 2100年参数绑定的限制。<br /><br />您可以将 pdo:: ATTR_EMULATE_PREPARES 属性设置为 true。 例如：<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />默认情况下，此属性设置为 False。<br /><br />**注意：** 当你使用 `PDO::ATTR_EMULATE_PREPARES => true`时，参数化查询的安全性不会生效。 你的应用程序应确保绑定到参数的数据未包含恶意 Transact-SQL 代码。<br /><br />**限制：**： 因为参数未绑定使用数据库的参数化的查询功能，不支持输入和输出参数。|  
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
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
