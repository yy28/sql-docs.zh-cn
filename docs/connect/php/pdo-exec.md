---
title: "Pdo:: exec |Microsoft 文档"
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
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48b1d6f918d87d2ad65b4be8b47a5a23975d1811
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在单个函数调用中准备和执行 SQL 语句，从而返回受该语句影响的行数。  
  
## <a name="syntax"></a>语法  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parameters  
*$statement*：包含要执行的 SQL 语句的字符串。  
  
## <a name="return-value"></a>返回值  
报告受影响行数的整数。  
  
## <a name="remarks"></a>注释  
如果 *$statement* 包含多个 SQL 语句，则仅为最后一个语句报告受影响行的计数。  
  
PDO::exec 不为 SELECT 语句返回结果。  
  
以下属性会影响 PDO::exec 的行为：  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
有关详细信息，请参阅 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例删除表 1 中的行，该行在第 1 列中具有“xxxyy”。 然后，该示例报告已删除的行数。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
