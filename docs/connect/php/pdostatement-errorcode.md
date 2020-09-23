---
title: PDOStatement::errorCode
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中 PDOStatement::errorCode 函数的 API 参考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4161abec-c12b-444e-9de5-f1dac7b3e0e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a514d18bc03d1cbbc05b3e75f98e93a88535c9e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645218"
---
# <a name="pdostatementerrorcode"></a>PDOStatement::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索数据库语句对象上最近操作的 SQLSTATE。  
  
## <a name="syntax"></a>语法  
  
```  
  
string PDOStatement::errorCode();  
```  
  
## <a name="return-value"></a>返回值  
如果语句句柄上没有任何操作，将以字符串或 NULL 形式返回五个字符的 SQLSTATE。  
  
## <a name="remarks"></a>注解  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例演示具有错误的 SQL 查询。  然后显示错误代码。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print $stmt->errorCode();  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
