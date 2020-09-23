---
title: PDOStatement::getAttribute
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中 PDOStatement::getAttribute 函数的 API 参考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07cc46717dafe973dee05647f1d08134d858c58e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646747"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索预定义 PDOStatement 属性或自定义驱动程序属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>参数  
$attribute：整数，PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常量之一。 支持的属性是可使用 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、PDO::SQLSRV_ATTR_DIRECT_QUERY（有关详细信息，请参阅 [PDO_SQLSRV Driver 中的直接语句执行和准备的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)）、PDO::ATTR_CURSOR 和 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE（有关详细信息，请参阅[游标类型 (PDO_SQLSRV Driver)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)）设置的属性。  
  
## <a name="return-value"></a>返回值  
如果成功，返回预定义 PDO 属性或自定义驱动程序属性的（混合）值。 如果失败，返回 NULL。  
  
## <a name="remarks"></a>注解  
有关示例，请参阅 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
