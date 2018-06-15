---
title: 加载 Microsoft Drivers for PHP for SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f257439fe011948ac264ac7aea33975abcf06dd
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308036"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>加载 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此页提供有关加载说明[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]到 PHP 进程空间。  
  
你可以从平台下载的预构建的驱动程序[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页。 每个安装程序包中包含在线程和非线程变体的 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 上，它们也会出现在 32 位和 64 位版本。 请参阅[Microsoft Drivers for PHP for SQL Server 的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)有关每个包中包含的驱动程序文件的列表。 PHP 版本、 体系结构和 threadedness PHP 环境，则必须与匹配的驱动程序文件。

在 Linux 和 macOS 上，安装驱动程序可以或者中可使用 PECL，[安装教程](../../connect/php/installation-tutorial-linux-mac.md)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>将驱动程序文件移动到扩展目录中  
驱动程序文件必须位于 PHP 运行时可在其中找到一个目录。 它是最简单的方法将驱动程序文件放入默认 PHP 扩展目录-若要查找的默认目录，请运行`php -i | sls extension_dir`Windows 上或`php -i | grep extension_dir`在 Linux/macOS 上。 如果你未使用的默认扩展目录，PHP 配置文件 (php.ini) 中指定一个目录使用**extension_dir**选项。 例如，在 Windows 上，如果你已将驱动程序文件放在你`c:\php\ext`目录中，将以下行添加到 php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 启动时加载驱动程序  
若要在 PHP 启动时加载 SQLSRV 驱动程序，首先将驱动程序文件移动到扩展目录中。 然后，按如下步骤操作：  
  
1.  若要启用**SQLSRV**驱动程序，修改**php.ini**通过将以下行添加到扩展部分，更改为适当的文件名：  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上，如果你下载的预构建的二进制文件的分发： 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果已编译 SQLSRV 二进制源从或 PECL，则它将改为命名 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要启用**PDO_SQLSRV**驱动程序，PHP 数据对象 (PDO) 扩展必须可用作内置扩展，或者作为动态加载扩展。

    在 Windows 上，预构建的 PHP 二进制文件由 PDO 内置，所以无需修改 php.ini 加载它。 如果在但是，你已编译的源中的 PHP，并指定要生成的单独的 PDO 扩展，它将命名`php_pdo.dll`，你必须将其复制到扩展目录，并将以下行添加到 php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上，如果你已安装 PHP 使用您的系统的包管理器，PDO 可能作为安装名为 pdo.so 动态加载扩展。 PDO 扩展必须加载之前 PDO_SQLSRV 扩展，或加载将失败。 通常使用单个.ini 文件加载扩展的之后 php.ini, 读取这些文件。 因此，如果 pdo.so 加载通过其自己的.ini 文件中，则需要单独的文件加载后 PDO PDO_SQLSRV 驱动程序。 

    若要了解哪个目录特定于扩展的.ini 文件位于，运行`php --ini`并记下下面列出的目录`Scan for additional .ini files in:`。 查找的文件，加载 pdo.so--它可能由一个数字，如 10 pdo.ini 的前缀。 数字前缀表示.ini 文件中，加载顺序，而按字母顺序加载的文件没有数字前缀。 创建要加载 30 pdo_sqlsrv.ini （任何大于前缀 pdo.ini 工作原理的一个数字） 或 pdo_sqlsrv.ini （如果不由很多的前缀 pdo.ini），调用 PDO_SQLSRV 驱动程序文件并将以下行添加到它，更改为文件名的文件适当:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    作为使用 SQLSRV，如果在已编译 PDO_SQLSRV 二进制源从或 PECL，它将改为命名 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    将此文件复制到包含其他.ini 文件的目录。 

    如果你进行了编译 PHP 具有内置 PDO 支持的源中，你不需要单独的.ini 文件，并可以将上面的相应行添加到 php.ini。
  
3.  重新启动 Web 服务器。  
  
> [!NOTE]  
> 若要确定是否已成功加载驱动程序，请运行调用的脚本[phpinfo （)](http://php.net/manual/en/function.phpinfo.php)。  
  
有关详细信息**php.ini**指令，请参阅[核心 php.ini 指令说明](http://php.net/manual/en/ini.core.php)。  
  
## <a name="see-also"></a>请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[系统要求 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[For PHP for SQL Server 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
