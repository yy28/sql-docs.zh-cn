---
title: PDOStatement::setFetchMode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f132b2af-0433-4fbe-b03f-69a7d631093a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5a9065123bbacc828c7949aabcb44de6136f62c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67935985"
---
# <a name="pdostatementsetfetchmode"></a>PDOStatement::setFetchMode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

为 PDOStatement 句柄指定提取模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::setFetchMode( $mode );  
```  
  
#### <a name="parameters"></a>参数  
$*mode*：可传递给 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 的任何有效参数。  
  
## <a name="return-value"></a>返回值  
如果成功，则为 True；否则为 False。  
  
## <a name="remarks"></a>备注  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt1 = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   while ( $row = $stmt1->fetch()) {   
      print($row['Name'] . "\n");   
   }  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_ASSOC);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_NUM);  
   $result = $stmt->fetch();  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_BOTH);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_LAZY);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_OBJ);  
   $result = $stmt->fetch();  
   print $result->Name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
