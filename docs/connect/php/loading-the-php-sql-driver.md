---
title: 加载 Microsoft Drivers for PHP
description: 本页介绍了如何将 Microsoft Drivers for PHP for SQL Server 加载到 PHP 进程空间中。
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73899b2ea917c3981b0c696b78de453eacbf894d
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632769"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>加载 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本页提供有关将 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 加载到 PHP 进程空间中的说明。  
  
可以从 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub 项目页下载适用于你的平台的预生成驱动程序。 每个安装包都包含线程和非线程变体中的 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 上，它们也可用于 32 位和 64 位变体。 有关每个包中包含的驱动程序文件的列表，请参阅 [Microsoft Drivers for PHP for SQL Server 系统要求](system-requirements-for-the-php-sql-driver.md)。 驱动程序文件必须与 PHP 环境的 PHP 版本、体系结构和线程性匹配。

在 Linux 和 macOS 上，可以也使用 PECL 安装驱动程序，如[安装教程](installation-tutorial-linux-mac.md)中所示。

还可以在构建 PHP 时或使用 `phpize` 从源生成驱动程序。 如果选择从源生成驱动程序，则可以通过在生成 PHP 时将 `--enable-sqlsrv=static --with-pdo_sqlsrv=static`（在 Linux 和 macOS 上）或 `--enable-sqlsrv=static --with-pdo-sqlsrv=static`（在 Windows 上）添加到 `./configure` 命令来将驱动程序静态生成到 PHP 中，而不是将它们生成为共享扩展。 有关 PHP 生成系统和 `phpize` 的详细信息，请参阅 [PHP 文档](http://php.net/manual/install.php)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>将驱动程序文件移动到扩展目录中  
驱动程序文件必须位于 PHP 运行时可以找到它的目录中。 最简单的方法是将驱动程序文件放入默认的 PHP 扩展目录中。要查找默认目录，只需在 Windows 上运行 `php -i | sls extension_dir` 或在 Linux/macOS 上运行 `php -i | grep extension_dir`。 如果使用的不是默认扩展目录，请使用 extension_dir  选项在 PHP 配置文件 (php.ini) 中指定一个目录。 例如，在 Windows 上，如果已将驱动程序文件置于 `c:\php\ext` 目录中，则将以下行添加到 php.ini 中：
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 启动时加载驱动程序  
若要在 PHP 启动时加载 SQLSRV 驱动程序，首先要将驱动程序文件移动到扩展目录中。 然后，按如下步骤操作：  
  
1.  要启用 SQLSRV  驱动程序，请通过向扩展部分添加以下行并适当地更改文件名来修改 php.ini  ：  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上，如果已经下载用于分发的预生成二进制文件： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果已从源代码或使用 PECL 编译了 SQLSRV 二进制文件，则会将其命名为 sqlsrv.so：
    ```
    extension=sqlsrv.so
    ```
  
2.  要启用 PDO_SQLSRV  驱动程序，PHP 数据对象 (PDO) 必须可用作内置扩展，或用作动态加载的扩展。

    在 Windows 上，预生成的 PHP 二进制文件带有内置的 PDO，因此无需修改 php.ini 即可加载它。 但是，如果已从源编译 PHP 并指定了要生成的单独 PDO 扩展，它将被命名为 `php_pdo.dll`，并且必须将其复制到扩展目录中并将以下行添加到 php.ini 中：  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上，如果使用系统的包管理器安装了 PHP，则 PDO 可能会作为名为 pdo.so 的动态加载扩展进行安装。 必须先加载 PDO 扩展，然后才能加载 PDO_SQLSRV 扩展，否则，加载会失败。 扩展通常使用单个 .ini 文件加载，这些文件在 php.ini 之后读取。 因此，如果通过其自己的 .ini 文件加载 pdo.so，则需要一个可在 PDO 之后加载 PDO_SQLSRV 驱动程序的单独文件。 

    要查找扩展特定的 .ini 文件位于哪个目录，请运行 `php --ini` 并记下 `Scan for additional .ini files in:` 下列出的目录。 查找加载 pdo.so 的文件。 此文件的前缀可能是数字（如 10-pdo.ini）。 数字前缀表示加载 .ini 文件的顺序，而没有数字前缀的文件则按字母顺序加载。 创建一个文件以加载名为 30-pdo_sqlsrv.ini（任何大于 pdo.ini 前缀的数字都适用）或 pdo_sqlsrv.ini（如果 pdo.ini 没有数字前缀）的 PDO_SQLSRV 驱动程序文件，然后将以下行添加到驱动程序，并相应地更改文件名：  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    与 SQLSRV 一样，如果已从源或使用 PECL 编译了 PDO_SQLSRV 二进制文件，则会将其命名为 pdo_sqlsrv.so：
    ```
    extension=pdo_sqlsrv.so
    ```
    将此文件复制到包含其他 .ini 文件的目录中。 

    如果使用内置的 PDO 支持从源编译 PHP，则不需要单独的 .ini 文件，可以将上面相应的行添加到 php.ini 中。
  
3.  重新启动 Web 服务器。  
  
> [!NOTE]  
> 若要确定驱动程序是否已成功加载，请运行可调用 [phpinfo()](https://php.net/manual/en/function.phpinfo.php) 的脚本。  
  
有关 php.ini 指令的详细信息，请参阅[核心 php.ini 指令说明](https://php.net/manual/en/ini.core.php)  。  
  
## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 系统要求](system-requirements-for-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 编程指南](programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](pdo-sqlsrv-driver-reference.md)  
  
