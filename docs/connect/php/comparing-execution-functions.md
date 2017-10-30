---
title: "比较执行函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e74c7433ab2e3a831d6aa800a2a1a9abbbda5863
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="comparing-execution-functions"></a>比较执行函数
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 提供用于执行函数的若干选项。  
  
如果使用的是 SQLSRV 驱动程序，使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 执行单个查询，并结合使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 执行已准备的语句，每次执行的参数值均不同。  
  
如果使用的是 PDO_SQLSRV 驱动程序，可以使用以下命令之一执行查询：  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) 和 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)。  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驱动程序参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  

