---
title: 'Pdostatement:: Bindcolumn |Microsoft 文档'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f77fdb089f83d1d8d8f866be4a0a7ef99b9fa155
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

将变量绑定到结果集中的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>Parameters  
$*列*: （混合） 数的列 （基于 1 的索引） 或在结果集中的列的名称。  
  
&$*param*: 列将绑定到的 PHP 变量的 （混合） 名称。  
  
$*类型*: PDO::PARAM_ * 常量表示的参数的可选数据类型。  
  
$*maxLen*：可选整数，不由 Microsoft Drivers for PHP for SQL Server 使用。  
  
$*driverdata*： 可选混合驱动程序的参数。 例如，你可以指定 PDO::SQLSRV_ENCODING_UTF8 以采用 UTF-8 编码的字符串形式将列绑定到变量。  
  
## <a name="return-value"></a>返回值  
如果成功，则为 TRUE；否则为 FALSE。  
  
## <a name="remarks"></a>注释  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例显示变量可如何绑定到结果集中的列。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
