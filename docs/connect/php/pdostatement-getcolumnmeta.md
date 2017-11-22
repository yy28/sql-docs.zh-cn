---
title: "PDOStatement::getColumnMeta |Microsoft 文档"
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
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c43b41503fe74744a9c28c18210af6445a216a4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索列的元数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parameters  
*$conn*: （整数） 你想要检索其元数据的列的从零开始的数。  
  
## <a name="return-value"></a>返回值  
包含列的元数据的关联阵列（键和值）。 有关数组中的字段的说明，请参阅“备注”部分。  
  
## <a name="remarks"></a>注释  
下表介绍 getColumnMeta 返回的数组中的字段。  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|指定列的 PHP 类型。 始终为字符串。|  
|driver:decl_type|指定用于表示数据库中的列值的 SQL 类型。 如果结果集中的列是函数的结果，则 PDOStatement::getColumnMeta 不会返回此值。|  
|flags|指定为此列设置的标志。 始终为 0。|  
|NAME|指定数据库中的列的名称。|  
|table|指定包含数据库中的列的表格名称。 始终为空白。|  
|len|指定列长度。|  
|精度|指定此列的数值精度。|  
|pdo_type|指定此列的类型，由 PDO::PARAM_* 常量表示。 Always PDO::PARAM_STR (2)。|  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
