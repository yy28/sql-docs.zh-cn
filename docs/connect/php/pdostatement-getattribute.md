---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 014f679480caaabd42863d2551cfa4c25bbe94d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992978"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索预定义 PDOStatement 属性或自定义驱动程序属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parameters  
 $attribute：一个整数，PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常量之一。 支持的属性是可以用[PDOStatement:: setAttribute](../../connect/php/pdostatement-setattribute.md)、PDO:: SQLSRV_ATTR_DIRECT_QUERY 设置的属性 (有关详细信息, 请参阅[PDO_SQLSRV 驱动程序中的直接语句执行和已准备的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO:: ATTR_CURSOR 和 PDO:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (有关详细信息, 请参阅[游标类型 (PDO_SQLSRV 驱动程序)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md))。  
  
## <a name="return-value"></a>返回值  
如果成功，返回预定义 PDO 属性或自定义驱动程序属性的（混合）值。 如果失败，返回 NULL。  
  
## <a name="remarks"></a>Remarks  
有关示例，请参阅 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
