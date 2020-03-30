---
title: 文档中相关的代码示例 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc76cee723c11d49a4d6149a7c3a1df4cedbc256
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015167"
---
# <a name="about-code-examples-in-the-documentation"></a>文档中相关的代码示例
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>有关代码示例的备注
在执行 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 文档中的代码示例时要注意以下几点：  
  
-   几乎所有示例都假定已在本地计算机上安装了 SQL Server 2008 或更高版本和 AdventureWorks 数据库。  
  
    有关如何下载免费版和试用版的 SQL Server 的信息，请参阅 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193)。  
  
    有关如何下载和安装 AdventureWorks 数据库的信息，请参阅 [SQL Server 示例 Github 存储库中的 AdventureWorks 页](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)。
  
-   本文档中的几乎所有代码示例都计划从命令行中运行，这可支持自动测试所有代码示例。 有关如何从命令行运行 PHP 的信息，请参阅 [从命令行使用 PHP](https://php.net/manual/en/features.commandline.php)。  
  
-   虽然示例应当从命令行中运行，但每个示例均可通过在不对脚本进行任何更改的情况下从浏览器调用来运行。 若要更好地格式化输出，请在每个示例中将每个“n”替换为“\<\/br>”，然后再从浏览器中调用它。  
  
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
[Microsoft Drivers for PHP for SQL Server 概述](../../connect/php/overview-of-the-php-sql-driver.md)
  
