---
title: Microsoft Drivers for PHP for SQL Server 系统要求 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992566"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 系统要求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文档列出了必须在系统上安装才能使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]访问 SQL SERVER 或 Azure SQL 数据库中的数据的组件。

正式支持适用于 SQL Server 的 Microsoft PHP 驱动程序版本3.1 及更高版本。 有关支持生命周期和要求 (包括早期版本的 PHP 驱动程序) 的完整详细信息, 请参阅[支持矩阵](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)。

## <a name="php"></a>PHP

要了解如何下载并安装最新的稳定 PHP 二进制文件，请参阅 [PHP 网站](https://php.net)。  适用于 PHP 的 Microsoft 驱动程序 SQL Server 需要以下版本的 PHP:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; PHP 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. 版本7.2.1 和更高版本在 Windows 上受支持, 而 Linux 和 macOS 上支持版本7.2.0 和更高版本。

-   某个版本的驱动程序文件必须位于 PHP 扩展目录中。 有关不同驱动程序文件的信息, 请参阅[驱动程序版本](#driver-versions)。  若要下载驱动程序，请参阅[下载 Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md)。 要了解如何配置适用于 PHP 的驱动程序，请参阅[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。

-   Web 服务器是必需的。 必须将 Web 服务器配置为运行 PHP。 有关如何在 IIS 中托管 PHP 应用程序的信息, 请参阅[php 网站上的教程](http://docs.php.net/manual/da/install.windows.iis7.php)。

    已通过结合使用 IIS 10 和 FastCGI 对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 进行了测试。  

    > [!NOTE]  
    > Microsoft 仅提供对 IIS 的支持。  

## <a name="odbc-driver"></a>ODBC 驱动程序

运行 PHP 的计算机上需要 Microsoft ODBC Driver for SQL Server 的正确版本。 你可以在[此页](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)上下载受支持平台的所有受支持的驱动程序版本。

如果要在64位版本的 Windows 上下载 Windows 版本的驱动程序, 则 ODBC 64 位安装程序将同时安装32位和64位 ODBC 驱动程序。 如果使用的是32位版本的 Windows, 请使用 ODBC x86 安装程序。 在非 Windows 平台上, 仅64位版本的驱动程序可用。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; ODBC 驱动程序版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 驱动程序 17+ |是|是|是| | | | |
|ODBC 驱动程序 13.1|是|是|是|是|是| | |
|ODBC 驱动程序 13  | | | | |是| | |
|ODBC 驱动程序 11  |是|是|是|是|是|是|是|

如果使用的是 SQLSRV 驱动程序, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)将返回有关[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]正在使用哪个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的 Microsoft ODBC Driver for SQL Server 的信息。 如果使用的是 PDO_SQLSRV 驱动程序，可以使用 [PDO::getAttribute](../../connect/php/pdo-getattribute.md) 来发现版本。  

## <a name="sql-server"></a>SQL Server

支持 Azure SQL 数据库。 有关信息，请参阅[连接到 Microsoft Azure SQL 数据库](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; SQL Server 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Database        |是|是|是|是| | | |
|Azure SQL 托管实例|是|是|是|是| | | |
|Azure SQL 数据仓库  |是|是|是|是| | | |
|SQL Server 2017           |是|是|是|是| | | |
|SQL Server 2016           |是|是|是|是|是| | |
|SQL Server 2014           |是|是|是|是|是|是|是|
|SQL Server 2012           |是|是|是|是|是|是|是|
|SQL Server 2008 R2        |是|是|是|是|是|是|是|
|SQL Server 2008           | | | | |是|是|是|

## <a name="operating-systems"></a>操作系统
每个版本的驱动程序支持的操作系统如下所示:

|SQL Server 驱动程序版本的 PHP&#8594;<br />&#8595; 操作系统|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |是  |是  |是  |是  |   |   |   |
|Windows Server 2012 R2              |是  |是  |是  |是  |是  |是  |是  |
|Windows Server 2012                 |是  |是  |是  |是  |是  |是  |是  |
|Windows Server 2008 R2 SP1          |   |   |   |   |是  |是  |是  |
|Windows Server 2008 SP2             |   |   |   |   |是  |是  |是  |
|Windows 10                          |是  |是  |是  |是  |是  |   |   |
|Windows 8.1                         |是  |是  |是  |是  |是  |是  |是  |
|Windows 8                           |   |   |   |是  |是  |是  |是  |
|Windows 7 SP1                       |   |   |   |   |是  |是  |是  |
|Windows Vista SP2                   |   |   |   |   |是  |是  |是  |
|Ubuntu 18.10 (64)               |是  |   |   |   |   |   |   |
|Ubuntu 18.04 (64)               |是  |是  |   |   |   |   |   |
|Ubuntu 17.10 (64)               |   |是  |是  |   |   |   |   |
|Ubuntu 16.04 (64)               |是  |是  |是  |是  |是  |   |   |
|Ubuntu 15.10 (64)               |   |   |   |是  |   |   |   |
|Ubuntu 15.04 (64)               |   |   |   |   |是  |   |   |
|Debian 9 (64 位)                   |是  |是  |是  |   |   |   |   |
|Debian 8 (64 位)                   |是  |是  |是  |是  |   |   |   |
|Red Hat Enterprise Linux 7（64 位） |是  |是  |是  |是  |是  |   |   |
|Suse Enterprise Linux 15 (64 位)   |是  |   |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 位)   |是  |是  |是  |   |   |   |   |
|macOS Mojave (64 位)               |是  |   |   |   |   |   |   |
|macOS (64 位)          |是  |是  |   |   |   |   |   |
|macOS Sierra (64 位)               |是  |是  |是  |是  |   |   |   |
|macOS El Capitan (64 位)           |   |是  |是  |是  |   |   |   |

## <a name="driver-versions"></a>驱动程序版本  
本部分列出了每个版本[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]附带的驱动程序文件。 每个安装包都包含串接和非线程变体中的 SQLSRV 和 PDO_SQLSRV 驱动程序文件。 在 Windows 上, 它们也可用于32位和64位变体。 若要配置用于 PHP 运行时的驱动程序, 请按照[加载用于 php 的 Microsoft 驱动程序来 SQL Server](../../connect/php/loading-the-php-sql-driver.md)中的安装说明进行操作。

在支持的 Linux 和 macOS 版本上, 可以使用 PHP 的 PECL 包系统安装适当的驱动程序, 遵循[Linux 和 macOS 安装说明](../../connect/php/installation-tutorial-linux-mac.md)。 或者, 你可以从[Microsoft 的 PHP 驱动程序 for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页中为平台下载预生成的二进制文件。下表列出了在预生成的二进制包中找到的文件。

**Microsoft Drivers 5.6 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32位 php7|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32位 php7ts|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64位 php7|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64位 php7ts|   
|32 位 php_sqlsrv_72_nts.dll<br />32 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |32位 php7|  
|32 位 php_sqlsrv_72_ts.dll <br />32 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|32位 php7ts|  
|64 位 php_sqlsrv_72_nts.dll<br />64 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |64位 php7|  
|64 位 php_sqlsrv_72_ts.dll <br />64 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|64位 php7ts|  
|32 位 php_sqlsrv_73_nts.dll<br />32 位 php_pdo_sqlsrv_73_nts.dll|7.3|否 |32位 php7|  
|32 位 php_sqlsrv_73_ts.dll <br />32 位 php_pdo_sqlsrv_73_ts.dll |7.3|是|32位 php7ts|  
|64 位 php_sqlsrv_73_nts.dll<br />64 位 php_pdo_sqlsrv_73_nts.dll|7.3|否 |64位 php7|  
|64 位 php_sqlsrv_73_ts.dll <br />64 位 php_pdo_sqlsrv_73_ts.dll |7.3|是|64位 php7ts|  

在 Linux 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|否 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|是|

**Microsoft Drivers 5.3 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32位 php7|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32位 php7ts|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64位 php7|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64位 php7ts|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32位 php7|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32位 php7ts|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64位 php7|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64位 php7ts|   
|32 位 php_sqlsrv_72_nts.dll<br />32 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |32位 php7|  
|32 位 php_sqlsrv_72_ts.dll <br />32 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|32位 php7ts|  
|64 位 php_sqlsrv_72_nts.dll<br />64 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |64位 php7|  
|64 位 php_sqlsrv_72_ts.dll <br />64 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|64位 php7ts|  

在 Linux 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 5.2 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32位 php7|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32位 php7ts|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64位 php7|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64位 php7ts|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32位 php7|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32位 php7ts|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64位 php7|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64位 php7ts|   
|32 位 php_sqlsrv_72_nts.dll<br />32 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |32位 php7|  
|32 位 php_sqlsrv_72_ts.dll <br />32 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|32位 php7ts|  
|64 位 php_sqlsrv_72_nts.dll<br />64 位 php_pdo_sqlsrv_72_nts.dll|7.2|否 |64位 php7|  
|64 位 php_sqlsrv_72_ts.dll <br />64 位 php_pdo_sqlsrv_72_ts.dll |7.2|是|64位 php7ts|  

在 Linux 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|否 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|是|

**Microsoft Drivers 4.3 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32 位 php_sqlsrv_7_nts.dll <br />32 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |32位 php7|
|32 位 php_sqlsrv_7_ts.dll  <br />32 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|32位 php7ts|
|64 位 php_sqlsrv_7_nts.dll <br />64 位 php_pdo_sqlsrv_7_nts.dll |7.0|否 |64位 php7|  
|64 位 php_sqlsrv_7_ts.dll  <br />64 位 php_pdo_sqlsrv_7_ts.dll  |7.0|是|64位 php7ts|
|32 位 php_sqlsrv_71_nts.dll<br />32 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |32位 php7|  
|32 位 php_sqlsrv_71_ts.dll <br />32 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|32位 php7ts|  
|64 位 php_sqlsrv_71_nts.dll<br />64 位 php_pdo_sqlsrv_71_nts.dll|7.1|否 |64位 php7|  
|64 位 php_sqlsrv_71_ts.dll <br />64 位 php_pdo_sqlsrv_71_ts.dll |7.1|是|64位 php7ts|   

在 Linux 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|否 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|是|  

**Microsoft Drivers 4.0 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32位 php7|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32位 php7ts|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64位 php7|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64位 php7ts|   

在 Linux 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|否 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|是|

**Microsoft Drivers 3.2 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server：**  

在 Windows 上, 包括以下版本的驱动程序:

|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  

## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Driver for PHP for SQL Server 编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
