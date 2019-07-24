---
title: 加载 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936384"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>加载 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本页提供有关将 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 加载到 PHP 进程空间中的说明。  
  
可以从适用于[PHP 的 Microsoft 驱动程序 SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页下载适用于你的平台的预构建驱动程序。 每个安装包都包含串接和非线程变体中的 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 上, 它们也可用于32位和64位变体。 有关每个包中包含的驱动程序文件的列表, 请参阅[Microsoft driver FOR PHP for SQL Server 的系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)。 驱动程序文件必须与 php 环境的 PHP 版本、体系结构和 threadedness 匹配。

在 Linux 和 macOS 上, 还可以使用 PECL 安装驱动程序, 如[安装教程](../../connect/php/installation-tutorial-linux-mac.md)中所示。

还可以在生成 PHP 或使用`phpize`时从源生成驱动程序。 如果选择基于源构建驱动程序, 则可以选择将它们静态生成到 PHP, 而不是将其生成为共享扩展, 方法`--enable-sqlsrv=static --with-pdo_sqlsrv=static`是在中添加 (在 Linux `--enable-sqlsrv=static --with-pdo-sqlsrv=static`和 macOS 上) 或 ( `./configure`在 Windows 上)构建 PHP。 有关 php 生成系统和`phpize`的详细信息, 请参阅[php 文档](http://php.net/manual/install.php)。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>将驱动程序文件移动到扩展目录中  
驱动程序文件必须位于 PHP 运行时可以找到它的目录中。 最简单的方法是将驱动程序文件放在默认的 PHP 扩展目录中, 以便查找默认目录`php -i | sls extension_dir` , 在 Windows `php -i | grep extension_dir`或 Linux/macOS 上运行。 如果使用的不是默认扩展目录, 请使用**extension_dir**选项在 php 配置文件 (php) 中指定一个目录。 例如, 在 Windows 上, 如果将驱动程序文件放在`c:\php\ext`目录中, 请将以下行添加到 php .ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>在 PHP 启动时加载驱动程序  
若要在 PHP 启动时加载 SQLSRV 驱动程序，首先要将驱动程序文件移动到扩展目录中。 然后，按如下步骤操作：  
  
1.  若要启用**SQLSRV**驱动程序, 请通过将以下行添加到扩展部分来修改**php** , 并根据需要更改文件名:  
  
    在 Windows 上： 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    在 Linux 上, 如果已为分发下载预生成的二进制文件: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    如果已从源或 PECL 编译 SQLSRV 二进制文件, 则它将改为 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  若要启用**PDO_SQLSRV**驱动程序, PHP 数据对象 (PDO) 扩展必须可用于内置扩展或动态加载的扩展。

    在 Windows 上, 预生成的 PHP 二进制文件内置了 PDO, 因此, 无需修改 PHP 即可将其加载。 不过, 如果已从源编译了 PHP, 并指定了要生成的单独的 PDO 扩展, 则将其命名`php_pdo.dll`为, 并且必须将其复制到扩展目录, 并将以下行添加到 PHP .ini:  
    ```
    extension=php_pdo.dll  
    ```
    在 Linux 上, 如果已使用系统的包管理器安装了 PHP, 则 PDO 可能安装为名为 pdo.so 的动态加载扩展。 必须先加载 PDO 扩展, 然后才能加载 PDO_SQLSRV 扩展, 否则加载将失败。 通常使用各个 .ini 文件加载扩展, 并在 php 之后读取这些文件。 因此, 如果通过其自己的 .ini 文件加载了 pdo.so, 则需要在 PDO 后加载 PDO_SQLSRV 驱动程序的单独文件。 

    若要找出扩展插件特定的 .ini 文件所在的目录, 请运行`php --ini`并记下`Scan for additional .ini files in:`列出的目录。 查找加载 pdo.so 的文件--可能会以数字作为前缀, 如10-pdo。 数字前缀指示 .ini 文件的加载顺序, 而没有数字前缀的文件则按字母顺序加载。 创建一个文件以加载名为30-pdo_sqlsrv 的 PDO_SQLSRV 驱动程序文件 (该文件的数量大于为 pdo 的前缀) 或 PDO_SQLSRV (如果 pdo 不是以数字作为前缀), 并向其添加以下行, 并将 filename 改为适宜  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    对于 SQLSRV, 如果已从源或 PECL 编译 PDO_SQLSRV 二进制文件, 则将改为将其命名为 PDO_SQLSRV。因此:
    ```
    extension=pdo_sqlsrv.so
    ```
    将此文件复制到包含其他 .ini 文件的目录。 

    如果已从使用内置 PDO 支持的源编译了 PHP, 则不需要单独的 .ini 文件, 并且可以将上面相应的行添加到 PHP。
  
3.  重新启动 Web 服务器。  
  
> [!NOTE]  
> 若要确定驱动程序是否已成功加载，请运行可调用 [phpinfo()](https://php.net/manual/en/function.phpinfo.php) 的脚本。  
  
有关 php.ini 指令的详细信息，请参阅[核心 php.ini 指令说明](https://php.net/manual/en/ini.core.php)  。  
  
## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Microsoft Driver for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
