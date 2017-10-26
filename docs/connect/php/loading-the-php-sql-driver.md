---
title: "加载 PHP SQL 驱动程序 |Microsoft 文档"
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
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cb2200b2c5d151981e9dcdf8322dd7c43b91c6ee
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="loading-the-php-sql-driver"></a>加载 PHP SQL 驱动程序
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题提供有关将 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 加载到 PHP 进程空间中的说明。  
  
加载驱动程序有以下两个选项。 驱动程序可以在 PHP 启动时加载，也可以在 PHP 脚本运行时加载。  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>将驱动程序文件移动到扩展目录中  
无论使用哪个过程，第一步都是要将驱动程序文件放在 PHP 运行时可以找到它的目录中。 因此，将驱动程序文件放在你的 PHP 扩展目录中。 有关与 [一同安装的驱动程序文件列表，请参阅](../../connect/php/system-requirements-for-the-php-sql-driver.md) PHP SQL 驱动程序系统要求 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  
  
如有必要，可以在 PHP 配置文件 (php.ini) 中指定的驱动程序文件的目录位置使用**extension_dir**选项。 例如，如果要将驱动程序文件放在 c:\php\ext 目录中，则使用此选项：  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>在 PHP 启动时加载驱动程序  
若要在 PHP 启动时加载 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，首先要将驱动程序文件移动到扩展目录中。 然后，按如下步骤操作：  
  
1.  若要启用**SQLSRV**驱动程序，修改**php.ini**通过将以下行添加到扩展部分，或修改已存在的行：  
  
    在 Windows 上 （此示例使用用于 PHP 7 版本 4.0 线程安全驱动程序）： 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    在 Linux 上 （此示例使用为通过 PECL 已安装的版本）： 
    ```  
    extension=sqlsrv.so  
    ```  
    若要启用**PDO_SQLSRV**驱动程序，修改**php.ini**通过将以下行添加到扩展部分，或修改已存在的行：  
  
    在 Windows 上 （此示例使用用于 PHP 7 版本 4.0 线程安全驱动程序）：
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    在 Linux 上 （此示例使用为通过 PECL 已安装的版本）：
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  如果你想要使用**PDO_SQLSRV**驱动程序，PHP 数据对象 (PDO) 扩展必须可用作内置扩展，或者作为动态加载扩展。 如果你需要动态加载 PDO_SQLSRV 驱动程序，php_pdo.dll （或在 Linux 上的 pdo.so） 必须出现在扩展目录中，并且以下行需要位于 php.ini:

    在 Windows 上：  
    ```
    extension=php_pdo.dll  
    ```  
    在 Linux 上：  
    ```
    extension=pdo.so  
    ```  
  
3.  重新启动 Web 服务器。  
  
> [!NOTE]  
> 若要确定是否已成功加载驱动程序，请运行调用的脚本[phpinfo （)](http://go.microsoft.com/fwlink/?LinkId=108678)。  
  
有关 **php.ini** 指令的详细信息，请参阅 [核心 php.ini 指令说明](http://go.microsoft.com/fwlink/?LinkId=105817)。  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>在 PHP 脚本运行时加载驱动程序  
若要在脚本运行时加载 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ，首先要将驱动程序文件移动到扩展目录中。 则包括匹配的驱动程序文件名的 PHP 脚本开头的以下行：  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
有关与动态加载扩展相关的 PHP 函数的详细信息，请参阅[dl](http://go.microsoft.com/fwlink/?LinkId=105818)和[extension_loaded。](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序入门](../../connect/php/getting-started-with-the-php-sql-driver.md)
[一同安装的驱动程序文件列表，请参阅](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
  

