---
title: 比较执行函数
description: 本主题列出了使用 Microsoft Drivers for PHP for SQL Server 时的不同查询执行函数
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680742"
---
# <a name="comparing-execution-functions"></a>比较执行函数
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 提供用于执行函数的若干选项。  

## <a name="sqlsrv-execution-functions"></a>SQLSRV 执行函数  
如果使用的是 SQLSRV 驱动程序，使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 执行单个查询，并结合使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 执行已准备的语句，每次执行的参数值均不同。  

## <a name="pdo_sqlsrv-execution-functions"></a>PDO_SQLSRV 执行函数 
如果使用的是 PDO_SQLSRV 驱动程序，可以使用以下命令之一执行查询：  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) 和 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)。  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Microsoft Drivers for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
