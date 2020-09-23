---
title: PDOStatement::closeCursor
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中 PDOStatement::closeCursor 函数的 API 参考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61ced9d3c4dca42dfe71baaef1a3201fb4f2d260
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645328"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

关闭游标，此时将再次执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>返回值  
如果成功，则为 true；否则为 false。  
  
## <a name="remarks"></a>注解  
当 MultipleActiveResultSets 连接选项设置为 false 时，closeCursor 将起作用。  有关 MultipleActiveResultSets 连接选项的详细信息，请参阅[如何：禁用多个活动的结果集 (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。  
  
也可以只将语句句柄设置为 null，而不是调用 closeCursor。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
