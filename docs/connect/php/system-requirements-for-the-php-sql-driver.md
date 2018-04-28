---
title: 系统要求 Microsoft Drivers for PHP for SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44a18257abc758ee910fb9c4953cbdef02239fbd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>系统要求 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文档列出了必须在 SQL Server 或 Azure SQL 数据库中使用的访问数据在系统安装的组件[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。

版本 3.1 和更高版本的 SQL Server 的 Microsoft PHP 驱动程序均获得官方支持。 有关支持生命周期和包括早期版本的 PHP 驱动程序的要求的完整详细信息，请参阅[支持矩阵](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

有关如何下载和安装最新稳定 PHP 二进制文件的信息，请参阅[PHP 网站](http://php.net)。  Microsoft Drivers for PHP for SQL Server 需要以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;PHP 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|在 Windows 上的 7.2.1+<br/>在其他平台上的 7.2.0+ | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4+  |        |
|5.5|       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   某个版本的驱动程序文件必须位于 PHP 扩展目录中。 请参阅[驱动程序版本](#driver-versions)有关不同驱动程序文件信息。  若要下载驱动程序，请参阅[下载 Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md)。 有关为 PHP 配置驱动程序的信息，请参阅[Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   Web 服务器是必需的。 必须将 Web 服务器配置为运行 PHP。 有关托管 PHP 应用程序使用 IIS 的信息，请参阅[教程 PHP 的网站上](http://php.net/manual/fa/install.windows.iis.php)。  

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]已经过测试使用 FastCGI 的 IIS 10。  

    > [!NOTE]  
    > Microsoft 仅提供对 IIS 的支持。  

## <a name="odbc-driver"></a>ODBC 驱动程序

Microsoft ODBC Driver for SQL Server 的正确版本是 PHP 运行时所在的计算机上需要的。 从以下链接下载：
- [Microsoft ODBC Driver 17 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 for SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)

如果你使用的 64 位操作系统，则 ODBC 64 位安装程序将安装 32 位和 64 位 ODBC 驱动程序。 如果你使用 32 位操作系统，使用 ODBC x86 安装程序。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;ODBC 驱动程序版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|ODBC 驱动程序 17  |是| | | | |
|ODBC Driver 13.1|是|是|是| | |
|ODBC Driver 13  | | |是| | |
|ODBC Driver 11  |是|是|是|是|是|

如果你使用的 SQLSRV 驱动程序， [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)返回哪些版本的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Microsoft ODBC Driver for SQL Server 正在使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 如果你使用的 PDO_SQLSRV 驱动程序，则可以使用[pdo:: getattribute](../../connect/php/pdo-getattribute.md)来发现版本。  

## <a name="sql-server"></a>SQL Server

支持 azure SQL 数据库。 有关信息，请参阅[连接到 Microsoft Azure SQL 数据库](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;SQL Server 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Azure SQL 托管的实例<br/> （扩展特邀预览阶段）|是|是| | | |
|Azure SQL 数据仓库|是|是| | | |
|SQL Server 2017   |是|是| | | |
|SQL Server 2016   |是|是|是| | |
|SQL Server 2014   |是|是|是|是|是|
|SQL Server 2012   |是|是|是|是|是|
|SQL Server 2008 R2|是|是|是|是|是|
|SQL Server 2008   | | |是|是|是|

## <a name="operating-systems"></a>操作系统
支持的操作系统版本的驱动程序如下所示：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;操作系统|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Windows Server 2016                      |是|是| | | |
|Windows Server 2012 R2                   |是|是|是|是|是|
|Windows Server 2012                      |是|是|是|是|是|
|Windows Server 2008 R2 SP1               | | |是|是|是|
|Windows Server 2008 SP2                  | | |是|是|是|
|Windows 10                               |是|是|是| | |
|Windows 8.1                              |是|是|是|是|是|
|Windows 8                                | |是|是|是|是|
|Windows 7 SP1                            | | |是|是|是|
|Windows Vista SP2                        | | |是|是|是|
|Ubuntu 17.10 （64 位）                    |是| | | | |
|Ubuntu 16.04 （64 位）                    |是|是|是| | |
|Ubuntu 15.10 （64 位）                    | |是| | | |
|Ubuntu 15.04 （64 位）                    | | |是| | |
|Debian 9 （64 位）                        |是| | | | |
|Debian 8 （64 位）                        |是|是| | | |
|Red Hat Enterprise Linux 7 （64 位）      |是|是|是| | |
|Suse Enterprise Linux 12 （64 位）        |是| | | | |
|macOS Sierra （64 位）                    |是|是| | | |
|macOS El Capitan （64 位）                |是|是| | | |

## <a name="driver-versions"></a>驱动程序版本  
本部分列出附带的每个版本的驱动程序文件[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 每个安装程序包中包含在线程和非线程变体的 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 上，它们也会出现在 32 位和 64 位版本。 若要配置与 PHP 运行时使用的驱动程序，请按照中的安装说明[Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

在受支持版本的 Linux 和 macOS，适当的驱动程序可以使用安装 PHP 的 PECL 包系统，以下[Linux 和 macOS 安装说明](../../connect/php/installation-tutorial-linux-mac.md)。 或者，你可以下载预建的二进制文件从平台[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页 — 下表列出预构建的二进制文件包中找到的文件。

**Microsoft Drivers 5.2 for PHP for SQL Server:**  

在 Windows 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位 php7ts.dll|
|64 位 php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位 php7ts.dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位 php7ts.dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位 php7.dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位 php7ts.dll|  

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server:**  

在 Windows 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位 php7ts.dll|
|64 位 php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位 php7ts.dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位 php7ts.dll|   

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  

**Microsoft Drivers 4.0 for PHP for SQL Server:**  

在 Windows 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位 php7ts.dll|   

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|

**Microsoft Drivers 3.2 for PHP for SQL Server:**  

在 Windows 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server:**  

在 Windows 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  

## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[For PHP for SQL Server 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
