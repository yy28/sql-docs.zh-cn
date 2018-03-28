---
title: 'Pdostatement:: Fetch |Microsoft 文档'
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
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7326279bc150c25c712ca708dcd137a9e0d805d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

从结果集中检索行。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>Parameters  
$*fetch_style*： 指定的格式的行数据的可选 （整数） 符号。 请参阅 $ 的可能的值列表的备注部分*fetch_style*。 默认值为 PDO::FETCH_BOTH。 $*fetch_style*方法将覆盖 $ 中提取*fetch_style* pdo:: query 方法中指定。  
  
$*cursor_orientation*:，该值指示要检索时在准备语句指定的行的可选 （整数） 符号`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`。 请参阅 $ 的可能的值列表的备注部分*cursor_orientation*。 有关使用可滚动游标的示例，请参阅 [PDO::prepare](../../connect/php/pdo-prepare.md) 。  
  
$*cursor_offset*： 指定要提取时的行的可选 （整数） 符号 $*cursor_orientation* PDO::FETCH_ORI_ABS 或 PDO::FETCH_ORI_REL 和 PDO::ATTR_CURSOR 是 PDO::CURSOR_SCROLL。  
  
## <a name="return-value"></a>返回值  
返回行或 false 的混合值。  
  
## <a name="remarks"></a>注释  
调用提取时，游标会自动前进。 下表包含可能列表*fetch_style*值。  
  
|$*fetch_style*|Description|  
|-------------------|---------------|  
|PDO::FETCH_ASSOC|指定按列名称进行索引的数组。|  
|PDO::FETCH_BOTH|指定按列名称和基于 0 的顺序进行索引的数组。 这是默认设置。|  
|PDO::FETCH_BOUND|返回 true，并如 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md)所指定分配值。|  
|PDO::FETCH_CLASS|创建一个实例，并将列映射到命名属性。<br /><br />在调用提取前调用 [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) 。|  
|PDO::FETCH_INTO|刷新请求类的实例。<br /><br />在调用提取前调用 [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) 。|  
|PDO::FETCH_LAZY|在访问和创建未命名对象期间创建变量名称。|  
|PDO::FETCH_NUM|指定按基于 0 的列顺序进行索引的数组。|  
|PDO::FETCH_OBJ|指定属性名称映射到列名称的未命名对象。|  
  
如果游标位于结果集末尾（已检索最后一行，并且游标已越过结果集边界），并且如果游标支持只进 (PDO::ATTR_CURSOR = PDO::CURSOR_FWDONLY)，后续提取调用将失败。  
  
如果游标可滚动 (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL)，提取将在结果集边界中移动游标。 下表包含可能列表*cursor_orientation*值。  
  
|$*cursor_orientation*|Description|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|检索下一行。 这是默认设置。|  
|PDO::FETCH_ORI_PRIOR|检索上一行。|  
|PDO::FETCH_ORI_FIRST|检索第一行。|  
|PDO::FETCH_ORI_LAST|检索最后一行。|  
|PDO::FETCH_ORI_ABS, *num*|检索在 $ 请求的行*cursor_offset*按行号。|  
|PDO::FETCH_ORI_REL， *num*|检索在 $ 请求的行*cursor_offset*按从当前位置的相对位置。|  
  
如果值为 $ 指定*cursor_offset*或 $*cursor_orientation*导致结果集边界之外的位置，提取将失败。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print( "\n---------- PDO::FETCH_CLASS -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg";  
      }  
  
      function __toString() {  
         return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
      }  
   }  
  
   $stmt->setFetchMode(PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
   while ( $row = $stmt->fetch(PDO::FETCH_CLASS)) {   
      print($row . "\n");   
   }  
  
   print( "\n---------- PDO::FETCH_INTO -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
   $c_obj = new cc( '' );  
  
   $stmt->setFetchMode(PDO::FETCH_INTO, $c_obj);  
   while ( $row = $stmt->fetch(PDO::FETCH_INTO)) {   
      echo "$c_obj\n";  
   }  
  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_ASSOC );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_NUM );  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_BOTH );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_LAZY );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_OBJ );  
   print $result->Name;  
   print( "\n \n" );  
  
   print( "\n---------- PDO::FETCH_BOUND -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->bindColumn('Name', $name);  
   $result = $stmt->fetch( PDO::FETCH_BOUND );  
   print $name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
