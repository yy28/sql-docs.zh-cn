---
title: "PHP SQL 驱动程序的系统要求 |Microsoft 文档"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba7e8cde4b8d3b77effca06b00303984223551f5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-php-sql-driver"></a>PHP SQL 驱动程序的系统要求
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在 SQL Server 或 Azure SQL 数据库中使用的访问数据[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，你必须在计算机上安装以下组件：  
  
-   PHP 是必需的。 有关如何下载和安装最新的稳定二进制文件的信息，请参阅[http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876)。  Microsoft Drivers for PHP for SQL Server 需要以下版本：
  
|Microsoft Drivers for PHP for SQL Server 版本|支持的 PHP 版本|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 和 PHP 7.1| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4+ 或<br /><br />PHP 5.5.16+ 或<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16+ 或<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 或<br /><br />PHP 5.3.0|  
|2.0|PHP 5.3.0 或<br /><br />PHP 5.2.4 或<br /><br />PHP 5.2.13|  
  
-   某个版本的驱动程序文件必须位于 PHP 扩展目录中。 有关不同驱动程序文件的信息，请参阅本主题后面的“驱动程序版本”。 有关为 PHP 运行时配置驱动程序的信息，请参阅 [加载 PHP SQL 驱动程序](../../connect/php/loading-the-php-sql-driver.md)  。 若要下载驱动程序，请参阅 [Microsoft Drivers for PHP for SQL Server](http://www.microsoft.com/download/details.aspx?id=20098)。  
  
-   Web 服务器是必需的。 必须将 Web 服务器配置为运行 PHP。 有关托管 PHP 应用程序与 Internet 信息服务 (IIS) 6.0 的信息，请参阅[使用 FastCGI 在 IIS 6.0 上托管 PHP 应用程序](http://go.microsoft.com/fwlink/?LinkId=117131)。 有关使用 IIS 7.0 托管 PHP 应用程序的信息，请参阅 [使用 FastCGI 在 IIS 7.0 上托管 PHP 应用程序](http://go.microsoft.com/fwlink/?LinkId=117132)。  
  
    已通过结合使用 IIS 6 和 IIS 7 与 FastCGI 对 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 进行了测试。  
  
    > [!NOTE]  
    > Microsoft 仅提供对 IIS 的支持。  
  
-   Microsoft ODBC Driver for SQL Server 或 SQL Server Native Client 的正确版本是 PHP 正在其中运行的计算机上需要的。  如果你使用的 64 位操作系统，则 ODBC 64 位安装程序将安装 32 位和 64 位 ODBC 驱动程序。 如果你使用 32 位操作系统，使用 ODBC x86 安装程序。

|Microsoft Drivers for PHP for SQL Server 版本|版本的 Microsoft ODBC Driver for SQL Server 或 SQL Server Native Client|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 for SQL Server 或 Microsoft ODBC Driver 13.1 for SQL Server。 若要下载 Microsoft ODBC 驱动程序，请参阅[Microsoft ODBC Driver 11 for SQL Server 页](http://www.microsoft.com/download/details.aspx?id=36434)或[Microsoft ODBC Driver 13.1 SQL Server 页](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 for SQL Server 或 Microsoft ODBC Driver 13 for SQL Server。 若要下载 Microsoft ODBC 驱动程序，请参阅[Microsoft ODBC Driver 11 for SQL Server 页](http://www.microsoft.com/download/details.aspx?id=36434)或[Microsoft ODBC Driver 13 for SQL Server 页](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 或 <br><br> 3.1|Microsoft ODBC Driver 11 for SQL Server。 若要下载 Microsoft ODBC 驱动程序，请参阅[Microsoft ODBC Driver 11 for SQL Server 页](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client。 可以从 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] SQL Server 2012 功能包页面 [下载 Microsoft](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2.0|Microsoft[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)]本机客户端：<br /><br />[下载 X86 程序包](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409)对于 32 位操作系统 <br /><br />[下载 X64 程序包](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409)对于 64 位操作系统|  

  
如果你使用的 SQLSRV 驱动程序， [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)返回哪些版本的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]本机客户端或 Microsoft ODBC Driver for SQL Server 正在使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 如果你使用的 PDO_SQLSRV 驱动程序，则可以使用[pdo:: getattribute](../../connect/php/pdo-getattribute.md)来发现版本。  



## <a name="database-versions"></a>数据库版本
-   支持 azure SQL 数据库。 有关信息，请参阅[连接到 Microsoft Azure SQL 数据库](../../connect/php/connecting-to-microsoft-azure-sql-database.md)。 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 4.3 支持 SQL Server 2008 R2 及更高版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 4.0 支持 SQL Server 2008 及更高版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 3.1 支持 SQL Server 2008 及更高版本
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 2.0 和 3.0 支持 SQL Server 2005 和更高版本


## <a name="driver-versions"></a>驱动程序版本  
本部分列出的驱动程序附带的每个版本[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  
  
若要配置与 PHP 运行时使用的驱动程序，请按照中的安装说明[加载 PHP SQL 驱动程序](../../connect/php/loading-the-php-sql-driver.md)。  
  
**Microsoft Drivers 4.3 for PHP for SQL Server:**  

在 Windows 上，对于 4.3 以下版本的驱动程序安装：
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位 php7.dll| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位 php7ts.dll| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位 php7ts.dll| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|否|32 位 php7.dll|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|是|32 位 php7ts.dll|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|否|64 位 php7.dll|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|是|64 位 php7ts.dll|   
  
**Microsoft Drivers 4.0 for PHP for SQL Server:**  

在 Windows 上，对于 4.0 以下版本的驱动程序安装：
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|否|32 位 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|是|32 位 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|否|64 位 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|是|64 位 php7ts.dll|   
  
在支持的 Linux 版本，可以使用 PHP 的 PECL 包系统安装 sqlsrv 和/或 pdo_sqlsrv 的适当版本。 
  
**Microsoft Drivers 3.2 for PHP for SQL Server 安装以下版本的驱动程序：**  
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|否|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|是|php5ts.dll|  
  
**Microsoft Drivers 3.1 for PHP for SQL Server 安装以下版本的驱动程序：**  
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|否|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|是|php5ts.dll|  
  
**Microsoft Drivers 3.0 for PHP for SQL Server 安装以下版本的驱动程序：**  
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|否|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|是|php5ts.dll|  
  
**Microsoft Drivers 2.0 for PHP for SQL Server 安装以下版本的驱动程序：**  
  
|驱动程序文件|PHP 版本|线程是否安全？|与 PHP .dll 一起使用|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|否|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|是|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|否|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|是|php5ts.dll|  
  
如果驱动程序文件的名称中包含“vc9”，它应与使用 Visual C++ 9.0 编译的 PHP 版本一起使用。  
## <a name="operating-systems"></a>操作系统 
支持的操作系统版本的驱动程序如下所示：

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 （64 位）
    -   Ubuntu 16.04 （64 位）
    -   Debian 8 （64 位）
    -   Red Hat Enterprise Linux 7 （64 位）
    -   Mac OS Sierra （64 位）
    -   Mac OS El Capitan （64 位）
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 （64 位）
    -   Ubuntu 16.04 （64 位）
    -   Red Hat Enterprise Linux 7 （64 位）

 
-   3.2 和 3.1:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] Service Pack 1  
    -   Windows XP Service Pack 3  
    -   Windows Vista Service Pack 1 或更高版本  
    -   Windows Server 2008（可能为英文页面）  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序入门](../../connect/php/getting-started-with-the-php-sql-driver.md)
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
  

