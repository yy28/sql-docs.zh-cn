---
title: 关于文档中的代码示例 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2ff8b884253f43c0b1092eb5ad7244eca7f3e3db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605815"
---
# <a name="about-code-examples-in-the-documentation"></a>文档中相关的代码示例
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>有关代码示例的备注
在执行 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 文档中的代码示例时要注意以下几点：  
  
-   几乎所有示例都假定本地计算机上安装 SQL Server 2008 或更高版本和 AdventureWorks 数据库。  
  
    有关如何下载免费版和试用版的 SQL Server 的信息，请参阅 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193)。  
  
    有关如何下载和安装 AdventureWorks 数据库的信息，请参阅[SQL Server 示例 Github 存储库中的 AdventureWorks 页](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)。
  
-   本文档中的几乎所有代码示例都计划从命令行中运行，这可支持自动测试所有代码示例。 有关如何从命令行运行 PHP 的信息，请参阅 [从命令行使用 PHP](http://php.net/manual/en/features.commandline.php)。  
  
-   虽然示例应当从命令行中运行，但每个示例均可通过在不对脚本进行任何更改的情况下从浏览器调用来运行。 若要很好地格式化输出，将替换为每个"\n""\<\/b >"中每个示例之前从浏览器中调用它。  
  
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
  
