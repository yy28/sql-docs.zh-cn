---
title: 系统要求 Microsoft Drivers for PHP for SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cfb813b857557a3a30bd89d9c96346ee261bc89
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174944"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 系统要求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文档列出了必须访问在 SQL Server 或 Azure SQL 数据库中使用的数据在系统安装的组件[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。

正式支持版本 3.1 和更高版本的 Microsoft PHP Drivers for SQL Server。 有关支持生命周期和要求，包括早期版本的 PHP 驱动程序的完整详细信息，请参阅[支持矩阵](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

要了解如何下载并安装最新的稳定 PHP 二进制文件，请参阅 [PHP 网站](http://php.net)。  Microsoft Drivers for PHP for SQL Server 需要以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; PHP 版本|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+（在 Windows 上）<br/>在其他平台上 7.2.0+ | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4 +  |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   某个版本的驱动程序文件必须位于 PHP 扩展目录中。 请参阅[驱动程序版本](#driver-versions)有关不同驱动程序文件信息。  若要下载驱动程序，请参阅[下载 Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md)。 要了解如何配置适用于 PHP 的驱动程序，请参阅[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   Web 服务器是必需的。 必须将 Web 服务器配置为运行 PHP。 有关托管 PHP 应用程序使用 IIS 的信息，请参阅[PHP 的网站教程](http://php.net/manual/fa/install.windows.iis.php)。  

    已通过结合使用 IIS 10 和 FastCGI 对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 进行了测试。  

    > [!NOTE]  
    > Microsoft 仅提供对 IIS 的支持。  

-   Microsoft Drivers for PHP for SQL Server 版本 5.3 将上一次，以支持 PHP 7.0。

## <a name="odbc-driver"></a>ODBC 驱动程序

在其运行 PHP 的计算机上需要 Microsoft ODBC Driver for SQL Server 的正确版本。 您可以下载所有受支持的版本的驱动程序的受支持的平台上[本页](https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)。

如果正在下载 64 位版本的 Windows 上的驱动程序的 Windows 版本，则 ODBC 64 位安装程序将安装 32 位和 64 位 ODBC 驱动程序。 如果使用 Windows 的 32 位版本，使用 ODBC x86 安装程序。 在非 Windows 平台上只有 64 位版本的驱动程序可用。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595;ODBC 驱动程序版本|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|ODBC 驱动程序 17+ |是|是| | | | |
|ODBC 驱动程序 13.1|是|是|是|是| | |
|ODBC 驱动程序 13  | | | |是| | |
|ODBC 驱动程序 11  |是|是|是|是|是|是|

如果使用的 SQLSRV 驱动程序， [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)返回的版本有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在使用 Microsoft ODBC Driver for SQL Server [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 如果使用的是 PDO_SQLSRV 驱动程序，可以使用 [PDO::getAttribute](../../connect/php/pdo-getattribute.md) 来发现版本。  

## <a name="sql-server"></a>SQL Server

支持 azure SQL 数据库。 有关信息，请参阅[连接到 Microsoft Azure SQL 数据库](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; SQL Server 版本|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Azure SQL Database        |是|是|是| | | |
|Azure SQL 托管实例|是|是|是| | | |
|Azure SQL 数据仓库  |是|是|是| | | |
|SQL Server 2017           |是|是|是| | | |
|SQL Server 2016           |是|是|是|是| | |
|SQL Server 2014           |是|是|是|是|是|是|
|SQL Server 2012           |是|是|是|是|是|是|
|SQL Server 2008 R2        |是|是|是|是|是|是|
|SQL Server 2008           | | | |是|是|是|

## <a name="operating-systems"></a>操作系统
有关版本的驱动程序支持的操作系统如下所示：

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Windows Server 2016                      |是|是|是| | | |
|Windows Server 2012 R2                   |是|是|是|是|是|是|
|Windows Server 2012                      |是|是|是|是|是|是|
|Windows Server 2008 R2 SP1               | | | |是|是|是|
|Windows Server 2008 SP2                  | | | |是|是|是|
|Windows 10                               |是|是|是|是| | |
|Windows 8.1                              |是|是|是|是|是|是|
|Windows 8                                | | |是|是|是|是|
|Windows 7 SP1                            | | | |是|是|是|
|Windows Vista SP2                        | | | |是|是|是|
|Ubuntu 18.04 （64 位）                    |是| | | | | |
|Ubuntu 17.10 （64 位）                    |是|是| | | | |
|Ubuntu 16.04 （64 位）                    |是|是|是|是| | |
|Ubuntu 15.10 （64 位）                    | | |是| | | |
|Ubuntu 15.04 （64 位）                    | | | |是| | |
|Debian 9 （64 位）                        |是|是| | | | |
|Debian 8 （64 位）                        |是|是|是| | | |
|Red Hat Enterprise Linux 7（64 位）      |是|是|是|是| | |
|Suse Enterprise Linux 12 （64 位）        |是|是| | | | |
|macOS High Sierra （64 位）               |是| | | | | |
|macOS Sierra （64 位）                    |是|是|是| | | |
|macOS El Capitan （64 位）                |是|是|是| | | |

## <a name="driver-versions"></a>驱动程序版本  
本部分列出了所含的每个版本的驱动程序文件[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 每个安装包包含在线程和单线程版本 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 中，它们也是在 32 位和 64 位版本中可用。 若要配置 PHP 运行时使用的驱动程序，请按照中的安装说明[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

在受支持版本的 Linux 和 macOS，相应的驱动程序可以使用安装 PHP 的 PECL 程序包系统，遵循[Linux 和 macOS 安装说明](../../connect/php/installation-tutorial-linux-mac.md)。 或者，可以下载预生成二进制文件从您的平台[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页，即以下各表列出的预构建的二进制程序包中找到的文件。

**Microsoft Drivers 5.3 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位 php7.dll|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位 php7ts.dll|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位 php7ts.dll|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位 php7.dll|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位 php7ts.dll|   
|32 位 php_sqlsrv_72_nts.dll<br />32 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位 php7.dll|  
|32 位 php_sqlsrv_72_ts.dll <br />32 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_72_nts.dll<br />64 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_72_ts.dll <br />64 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位 php7ts.dll|  

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 5.2 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位 php7.dll|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位 php7ts.dll|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位 php7ts.dll|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位 php7.dll|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位 php7ts.dll|   
|32 位 php_sqlsrv_72_nts.dll<br />32 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |32 位 php7.dll|  
|32 位 php_sqlsrv_72_ts.dll <br />32 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_72_nts.dll<br />64 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_72_ts.dll <br />64 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|64 位 php7ts.dll|  

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32 位 php7.dll|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32 位 php7ts.dll|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64 位 php7ts.dll|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32 位 php7.dll|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32 位 php7ts.dll|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64 位 php7.dll|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64 位 php7ts.dll|   

在 Linux 上，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  

**Microsoft Drivers 4.0 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

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

**Microsoft Drivers 3.2 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server：**  

在 Windows 中，将包括以下版本的驱动程序：

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  

## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
