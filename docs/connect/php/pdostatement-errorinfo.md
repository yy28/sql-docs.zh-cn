---
title: 'Pdostatement:: Errorinfo |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23ada0e81599b2f44a00d1964f9c5bfc67ab6cda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810545"
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索语句句柄上最新操作的扩展错误信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>返回值  
语句句柄上有关最新操作的错误信息的数组。 该数组包含以下字段：  
  
-   SQLSTATE 错误代码  
  
-   特定于驱动程序的错误代码  
  
-   特定于驱动程序的错误消息  
  
如果没有错误或如果未设置 SQLSTATE，特定于驱动程序的字段将为 NULL。  
  
## <a name="remarks"></a>Remarks  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
在此示例中，SQL 语句具有一个错误，随后将报告该错误。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
