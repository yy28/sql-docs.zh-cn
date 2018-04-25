---
title: PDO::errorInfo |Microsoft 文档
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
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa20f4bb1f833a43f2cfc8ae99423db8d6af7751
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索数据库句柄上最近操作的扩展错误信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>返回值  
有关数据库句柄上最近操作的错误信息的阵列。 该阵列包含以下字段：  
  
-   SQLSTATE 错误代码。  
  
-   特定于驱动程序的错误代码。  
  
-   特定于驱动程序的错误消息。  
  
如果没有错误或如果未设置 SQLSTATE，特定于驱动程序的字段将为 NULL。  
  
## <a name="remarks"></a>Remarks  
PDO::errorInfo 仅对直接在数据库上执行的操作检索错误信息。 在使用 PDO::prepare 或 PDO::query 创建 PDOStatement 实例时，使用 PDOStatement::errorInfo。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
在此示例中，列名称拼写不正确（是 `Cityx` 而不是 `City`）导致了错误，随后报告了该错误。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
