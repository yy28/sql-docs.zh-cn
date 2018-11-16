---
title: 'Pdostatement:: Execute |Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4622c75f7185fae2ad03f64a898e6625af680329
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605007"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>Parameters  
$input：（可选）包含参数标记的值的关联阵列。  
  
## <a name="return-value"></a>返回值  
如果成功，则为 True；否则为 False。  
  
## <a name="remarks"></a>Remarks  
使用 PDOStatement::execute 执行的语句必须先通过 [PDO::prepare](../../connect/php/pdo-prepare.md)准备就绪。 请参阅 [PDO_SQLSRV 驱动程序中的直接语句执行和已准备的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) 获取有关如何指定直接或已准备的语句执行的信息。  
  
输入参数数组的所有值将会视为 PDO::PARAM_STR 值。  
  
如果已准备的语句包括参数标记，你必须调用 PDOStatement::bindParam 来将 PHP 变量绑定到参数标记，或传递仅输入参数值的数组。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
> [!NOTE]
> 建议使用字符串作为输入，绑定到的值时[decimal 或 numeric 的列](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)若要确保的精确度和准确度，如 PHP 具有有限的精度[浮点数](https://php.net/manual/en/language.types.float.php)。 这同样适用于到 bigint 列，尤其是有效值的范围之外[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
