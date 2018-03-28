---
title: 关于文档中的代码示例 |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
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
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5515db3c5b98ddb0c3645016eade20ecf4f224b
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="about-code-examples-in-the-documentation"></a>文档中相关的代码示例
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>有关代码示例的备注
在执行 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 文档中的代码示例时要注意以下几点：  
  
-   几乎所有示例都假设在本地计算机上安装 SQL Server 2008 或更高版本和 AdventureWorks 数据库。  
  
    有关如何下载免费版和试用版的 SQL Server 的信息，请参阅 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193)。  
  
    有关如何下载和安装 AdventureWorks 数据库的信息，请参阅[SQL Server 示例 Github 存储库中的 AdventureWorks 页](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)。
  
-   本文档中的几乎所有代码示例都计划从命令行中运行，这可支持自动测试所有代码示例。 有关如何从命令行运行 PHP 的信息，请参阅 [从命令行使用 PHP](http://php.net/manual/en/features.commandline.php)。  
  
-   尽管示例意在从命令行运行，则可以通过调用其从浏览器而无需对脚本进行任何更改运行每个示例。 若要很好地格式化输出，将每个"\n"替换"\<\/巴西 >"中每个示例之前调用其从浏览器。  
  
-   为保持每个示例均有所侧重，不会在所有示例中进行正确的错误处理。 建议检查任何对 **sqlsrv** 函数或 PDO 方法的调用是否有错误，并根据应用程序需求进行处理。  
  
    在遇到错误时获取错误信息的简单方法是，使用以下代码行退出脚本：  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    或者，如果你使用的是 PDO，  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    有关处理错误和警告的详细信息，请参阅 [处理错误和警告](../../connect/php/handling-errors-and-warnings.md)。  
  
## <a name="see-also"></a>另请参阅  
[Microsoft Drivers for PHP for SQL Server 的概述](../../connect/php/overview-of-the-php-sql-driver.md)
  
