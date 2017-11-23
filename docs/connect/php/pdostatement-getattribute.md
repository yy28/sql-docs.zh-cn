---
title: "PDOStatement::getAttribute |Microsoft 文档"
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01332bc8166f2f242e4daffdd7204bbd5efe11de
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索预定义 PDOStatement 属性或自定义驱动程序属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parameters  
$*属性*： 一个整数，其中一个 PDO::ATTR_ * 或 PDO::SQLSRV_ATTR_\*常量。 受支持的属性是可以在设置的特性[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)，PDO::SQLSRV_ATTR_DIRECT_QUERY (有关详细信息，请参阅[直接语句执行和在准备语句执行PDO_SQLSRV 驱动程序](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md))，PDO::ATTR_CURSOR 和 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE (有关详细信息，请参阅[游标类型 （PDO_SQLSRV 驱动程序）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md))。  
  
## <a name="return-value"></a>返回值  
如果成功，返回预定义 PDO 属性或自定义驱动程序属性的（混合）值。 如果失败，返回 NULL。  
  
## <a name="remarks"></a>注释  
有关示例，请参阅 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
