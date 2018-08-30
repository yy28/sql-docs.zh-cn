---
title: PDO 类 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9c77b68d-0649-44af-96fa-586cbb319f5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0de878aa647d3d0f337c0882ec055d252da0041a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784684"
---
# <a name="pdo-class"></a>PDO 类
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO 类包含一些方法，允许 PHP 应用程序连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
PDO {}  
```  
  
## <a name="remarks"></a>Remarks  
PDO 类包含以下方法：  
  
[PDO::__construct](../../connect/php/pdo-construct.md)  

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
[PDO::commit](../../connect/php/pdo-commit.md)  
  
[PDO::errorCode](../../connect/php/pdo-errorcode.md)  
  
[PDO::errorInfo](../../connect/php/pdo-errorinfo.md)  
  
[PDO::exec](../../connect/php/pdo-exec.md)  
  
[PDO::getAttribute](../../connect/php/pdo-getattribute.md)  
  
[PDO::getAvailableDrivers](../../connect/php/pdo-getavailabledrivers.md)  
  
[PDO::lastInsertId](../../connect/php/pdo-lastinsertid.md)  
  
[PDO::prepare](../../connect/php/pdo-prepare.md)  
  
[PDO::query](../../connect/php/pdo-query.md)  
  
[PDO::quote](../../connect/php/pdo-quote.md)  
  
[PDO::rollback](../../connect/php/pdo-rollback.md)  
  
[PDO::setAttribute](../../connect/php/pdo-setattribute.md)  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Microsoft Drivers for PHP for SQL Server 概述](../../connect/php/overview-of-the-php-sql-driver.md)

[常量（Microsoft Drivers for PHP for SQL Server）](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
