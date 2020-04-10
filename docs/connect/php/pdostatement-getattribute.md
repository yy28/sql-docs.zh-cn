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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a401cded16dc139e5efc70129ceb0d66fd68dcd6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923455"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

检索预定义 PDOStatement 属性或自定义驱动程序属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>parameters  
$  attribute：一个整数，PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常量之一。 支持的属性是可使用 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、PDO::SQLSRV_ATTR_DIRECT_QUERY（有关详细信息，请参阅 [PDO_SQLSRV Driver 中的直接语句执行和准备的语句执行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)）、PDO::ATTR_CURSOR 和 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE（有关详细信息，请参阅[游标类型 (PDO_SQLSRV Driver)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)）设置的属性。  
  
## <a name="return-value"></a>返回值  
如果成功，返回预定义 PDO 属性或自定义驱动程序属性的（混合）值。 如果失败，返回 NULL。  
  
## <a name="remarks"></a>备注  
有关示例，请参阅 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
