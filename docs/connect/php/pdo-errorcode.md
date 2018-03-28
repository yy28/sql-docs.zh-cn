---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 143a7bef0a0be2d125068a7f003b0b941ff39617
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode 检索数据库句柄上最近操作的 SQLSTATE。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>返回值  
如果数据库句柄上没有任何操作，PDO::errorCode 将以字符串或 NULL 形式返回五个字符的 SQLSTATE。  
  
## <a name="remarks"></a>注释  
Pdo:: errorcode PDO_SQLSRV 驱动程序中的针对某些成功操作返回警告。 例如，在成功连接，pdo:: errorcode 返回"01000"，该值指示 SQL_SUCCESS_WITH_INFO。  
  
PDO::errorCode 仅检索直接在数据库连接上执行的操作的错误代码。 如果创建 PDOStatement 实例通过 pdo:: prepare 或 pdo:: query 和错误可在语句对象上生成，pdo:: errorcode 不会检索该错误。 必须调用 PDOStatement::errorCode 才可以返回在特定语句对象上执行的操作的错误代码。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
在此示例中，列的名称拼写错误 (`Cityx`而不是`City`)，从而导致错误，然后报告。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
