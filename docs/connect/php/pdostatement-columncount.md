---
title: "PDOStatement::columnCount |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d89a568-0c7c-40dd-9f54-db7313600df3
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 103eb4ede1fb61b25da00aced780d4a759a042bc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementcolumncount"></a>PDOStatement::columnCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

返回结果集中的列数。  
  
## <a name="syntax"></a>语法  
  
```  
  
int PDOStatement::columnCount ();  
```  
  
## <a name="return-value"></a>返回值  
返回结果集中的列数。 如果结果集为空，将返回零。  
  
## <a name="remarks"></a>注释  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
print $stmt->columnCount();   // 0  
  
echo "\n";  
$stmt->execute();  
print $stmt->columnCount();  
  
echo "\n";  
$stmt = $conn->query("select * from HumanResources.Department");  
print $stmt->columnCount();  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
