---
title: ':: __Construct |Microsoft 文档'
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
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0161c9ac0fdb75848e045fa49025270e3c475501
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

创建与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parameters  
*$dsn*： 包含的前缀名称的字符串 (始终`sqlsrv`)、 冒号和 Server 关键字。 例如， `"sqlsrv:server=(local)"`。 你可以选择指定其他连接关键字。 有关 Server 关键字和其他连接关键字的介绍，请参阅 [Connection Options](../../connect/php/connection-options.md) 。 因为整个 *$dsn* 包含在引号中，所以每个连接关键字不应单独引用。  
  
*$username*：可选。 包含用户名的字符串。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接，请指定登录 ID。 若要使用 Windows 身份验证进行连接，请指定 `""`。  
  
*$password*：可选。 包含用户密码的字符串。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接，请指定密码。 若要使用 Windows 身份验证进行连接，请指定 `""`。  
  
*$driver_options*： 可选。 您可以指定 PDO 驱动程序管理器属性和[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]特定驱动程序属性--PDO::SQLSRV_ATTR_ENCODING，PDO::SQLSRV_ATTR_DIRECT_QUERY。 无效的属性不会生成异常。 当使用 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)指定时，无效属性会生成异常。  
  
## <a name="return-value"></a>返回值  
返回 PDO 对象。 如果失败，则返回 PDOException 对象。  
  
## <a name="exceptions"></a>异常  
PDOException  
  
## <a name="remarks"></a>注释  
你可以通过将实例设置为 NULL 来关闭连接对象。  
  
连接后，pdo:: errorcode 将显示 01000 而非 00000。  
  
如果出于任何原因失败:: __construct，是引发异常，即使 PDO::ATTR_ERRMODE 设置为 PDO::ERRMODE_SILENT。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
此示例显示如何使用 Windows 身份验证连接到服务器，以及如何指定数据库。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>示例  
此示例显示如何连接到服务器，从而指定更高版本的数据库。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
