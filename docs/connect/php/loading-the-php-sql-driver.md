---
title: 加载 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dd99ffa39de48dbf8839cbe06a8bb236fffbdf3
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606197"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>加载 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本页提供有关将 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 加载到 PHP 进程空间中的说明。  
  
您可以下载预生成的驱动程序从你的平台[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页。 每个安装包包含在线程和单线程版本 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 中，它们也是在 32 位和 64 位版本中可用。 请参阅[Microsoft Drivers for PHP for SQL Server 的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)有关每个包中包含的驱动程序文件的列表。 PHP 版本、 体系结构和 threadedness PHP 环境，必须与匹配的驱动程序文件。

在 Linux 和 macOS 上，安装驱动程序可以或者使用 PECL 中, 找到[安装教程](../../connect/php/installation-tutorial-linux-mac.md)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>将驱动程序文件移动到扩展目录中  
驱动程序文件必须位于 PHP 运行时可以找到的目录。 它是最简单的方法将驱动程序文件放入默认 PHP 扩展目录-若要查找默认目录，请运行`php -i | sls extension_dir`在 Windows 或`php -i | grep extension_dir`Linux/macOS 上。 如果不使用默认扩展目录，在 PHP 配置文件 (php.ini) 中指定一个目录使用**extension_dir**选项。 例如，在 Windows，如果已将驱动程序文件放入你`c:\php\ext`目录中，将以下行添加到 php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 启动时加载驱动程序  
若要在 PHP 启动时加载 SQLSRV 驱动程序，首先要将驱动程序文件移动到扩展目录中。 然后，按如下步骤操作：  
  
1.  若要启用**SQLSRV**驱动程序，修改**php.ini**通过将以下行添加到扩展部分，更改相应的文件名：  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上，如果你下载预生成二进制文件的分发： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果已编译 SQLSRV 二进制源中或使用 PECL，它将改为命名 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要启用**PDO_SQLSRV**驱动程序，PHP 数据对象 (PDO) 扩展必须可用，用作内置扩展，或作为动态加载扩展。

    上 Windows，预生成的 PHP 二进制文件随 PDO 内置的因此无需修改 php.ini 加载它。 如果，但是，你已编译的 PHP 的源并指定要生成单独的 PDO 扩展，它将命名为`php_pdo.dll`，并且必须将其复制到扩展目录，并将以下行添加到 php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上，如果你已安装 PHP 使用系统的包管理器，PDO 可能作为安装名为 pdo.so 动态加载扩展。 必须在 PDO_SQLSRV 扩展插件之前, 加载的 PDO 扩展或加载将失败。 通常使用单个.ini 文件加载扩展和 php.ini 后读取这些文件。 因此，如果 pdo.so 通过其自己的.ini 文件加载的则需要单独的文件后 PDO 加载 PDO_SQLSRV 驱动程序。 

    若要找出哪个目录所在的特定于扩展的.ini 文件，请运行`php --ini`并记下的目录下列出`Scan for additional .ini files in:`。 查找的文件，加载 pdo.so--可能加一个数字，如 10 pdo.ini。 数字前缀指示.ini 文件的加载顺序时按字母顺序加载没有数字前缀的文件。 创建一个文件来加载 PDO_SQLSRV 驱动程序文件称为 30 pdo_sqlsrv.ini （任何前缀 pdo.ini 工作原理的更大数字） 或 pdo_sqlsrv.ini （如果 pdo.ini 不加一个数字），并将以下行添加到它，更改为文件名相应:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    作为使用 SQLSRV，如果已编译 PDO_SQLSRV 二进制源中或使用 PECL，它将改为命名 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    将此文件复制到包含其他.ini 文件的目录。 

    如果已编译 PHP 中内置了 PDO 的支持的源，不需要单独的.ini 文件，并可以将上面的相应行添加到 php.ini。
  
3.  重新启动 Web 服务器。  
  
> [!NOTE]  
> 若要确定驱动程序是否已成功加载，请运行可调用 [phpinfo()](https://php.net/manual/en/function.phpinfo.php) 的脚本。  
  
有关 php.ini 指令的详细信息，请参阅[核心 php.ini 指令说明](https://php.net/manual/en/ini.core.php)。  
  
## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
