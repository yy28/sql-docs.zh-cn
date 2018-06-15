---
title: PDO::errorInfo |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4a5dc723d735436bde18b813a8716b054779971
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307876"
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
  
如果没有错误，或如果未设置 SQLSTATE，特定于驱动程序的字段均为 NULL。  
  
## <a name="remarks"></a>Remarks  
PDO::errorInfo 仅对直接在数据库上执行的操作检索错误信息。 在使用 PDO::prepare 或 PDO::query 创建 PDOStatement 实例时，使用 PDOStatement::errorInfo。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
在此示例中，列的名称拼写错误 (`Cityx`而不是`City`)，从而导致错误，然后报告。  
  
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
  
## <a name="see-also"></a>请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
