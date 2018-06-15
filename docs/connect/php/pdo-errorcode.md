---
title: 'Pdo:: errorcode |Microsoft 文档'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73bc57c0519c3371b77e38b00b7cc2a8a203b811
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307896"
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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
