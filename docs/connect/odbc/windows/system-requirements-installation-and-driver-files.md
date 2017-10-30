---
title: "系统要求、 安装和驱动程序文件 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a11d146a889da5af037a154a1f8226e2bcb8ccb2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-installation-and-driver-files"></a>系统要求、安装和驱动程序文件
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 支持与 SQL Server 2014、SQL Server 2012 R2、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro_md.md)]、 [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]和 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]的连接。  
  
Windows 上的 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 可安装在还具有一个或多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 版本的计算机上。  
  
ODBC Driver 13 和为 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，除此之外，支持 SQL Server 2016。  
  
在连接字符串中指定的驱动程序名称是`ODBC Driver 11 for SQL Server`或`ODBC Driver 13 for SQL Server`（对于 13 和 13.1）。
  
## <a name="supported-operating-systems"></a>支持的操作系统

在以下 Windows 操作系统上，你可以使用该驱动程序运行应用程序：  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(ODBC Driver 11 仅)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安装 Microsoft ODBC Driver for SQL Server

当你运行安装了驱动程序`msodbcsql.msi`从[下载 Microsoft ODBC Driver 13.1 for Windows 上的 SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)，[下载 Microsoft ODBC Driver 13 for Windows 上的 SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)，或[下载 Microsoft ODBC Driver 11 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=36434)。 它可以是与并行安装的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]本机客户端。  

当调用`msodbcsql.msi`，默认情况下安装仅客户端组件。 客户端组件是支持运行的应用程序开发使用驱动程序的文件。 若要安装 SDK 组件，请指定`ADDLOCAL=ALL`命令行上。 例如：  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 指定`IACCEPTMSODBCSQLLICENSETERMS=YES`以接受最终用户许可条款，如果你使用`/passive`， `/qn`， `/qb`，或`/qr`安装选项。 必须以全大写字母指定此选项。 例如：  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 若要执行无提示卸载：  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
当应用程序使用该驱动程序时，应用程序应指示它依赖于通过安装选项的驱动程序`APPGUID`。 这样，在卸载之前的驱动程序安装程序链接到报表从属应用程序。 若要对此驱动程序指定的依赖关系，将设置`APPGUID`到你的产品代码时以无提示方式安装驱动程序的命令行参数。 （当使用 Microsoft Installer 捆绑应用程序安装程序时，必须创建产品代码。）例如：  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>命令行工具： sqlcmd.exe 和 bcp.exe

`bcp.exe`和`sqlcmd.exe`工具以使用驱动程序的使用可以在下载[Microsoft Command Line Utilities 11 for SQL Server](http://www.microsoft.com/download/details.aspx?id=36433)， [Microsoft 命令行实用程序 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)，或[Microsoft Command Line Utilities 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53591)。 该驱动程序已安装的必备软件`sqlcmd.exe`和`bcp.exe`。
  
`bcp.exe`和`sqlcmd.exe`安装在`110\Tools`的子文件夹`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC`版本 11 中，和`130\Tools`13 和 13.1。

使用 BCP 函数的应用程序必须指定相同的版本，传送的驱动程序的标头文件和库用于编译应用程序。  

例如，当编译 ODBC 应用程序与`msodbcsql11.lib`和`msodbcsql.h`，使用"驱动程序 = {ODBC Driver 11 for SQL Server}"中的连接字符串。

## <a name="components-of-the-microsoft-odbc-driver-13-and-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>组件的 Microsoft ODBC Driver 13 和为 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 Windows 上的 ODBC 驱动程序包含以下组件：  
  
|组件|说明|  
|---------------|-----------------|  
|msodbcsql13.dll|包含所有驱动程序功能的动态链接库 (DLL) 文件。 msodbcsql13.dll 安装在 %SYSTEMROOT%\System32 中。|  
|msodbcsqlr13.rll|驱动程序库的附带资源文件。 msodbcsqlr13.rll 安装在 %SYSTEMROOT%\System32\1033 中。|  
|s13ch_msodbcsql.chm|介绍如何创建数据源驱动程序数据源向导帮助文件。 s13ch_msodbcsql.chm 安装在 %SYSTEMROOT%\System32\1033 中|  
|msodbcsql.h|包含的所有新的定义使用的驱动程序所需的标头文件。<br /><br /> **注意：**  你无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK。|  
|msodbcsql13.lib|调用所需的库文件**bcp**属于该驱动程序的实用工具函数。<br /><br /> **注意：**  如果你确实在你的程序中引用 msodbcsql13.lib，请确保 msodbcsql13.dll 在你的系统路径中，并且在使用该应用程序的系统路径中。<br /><br /> msodbcsql13.lib 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK。|  
  
## <a name="components-of-the-microsoft-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Windows 上的 Microsoft ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的组件  
 Windows 上的 ODBC 驱动程序包含以下组件：  
  
|组件|说明|  
|---------------|-----------------|  
|msodbcsql11.dll|包含所有驱动程序功能的动态链接库 (DLL) 文件。 msodbcsql11.dll 安装在 %SYSTEMROOT%\System32 中。|  
|msodbcsqlr11.rll|驱动程序库的附带资源文件。 msodbcsqlr11.rll 安装在 %SYSTEMROOT%\System32\1033 中。|  
|s11ch_msodbcsql.chm|介绍如何创建数据源驱动程序数据源向导帮助文件。 s11ch_msodbcsql.chm 安装在 %SYSTEMROOT%\System32\1033 中|  
|msodbcsql.h|包含的所有新的定义使用的驱动程序所需的标头文件。<br /><br /> **注意：**  你无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|  
|msodbcsql11.lib|调用所需的库文件**bcp**属于该驱动程序的实用工具函数。<br /><br /> **注意：**  如果你确实在你的程序中引用 msodbcsql11.lib，请确保 msodbcsql11.dll 在你的系统路径中，并且在使用该应用程序的系统路径中。<br /><br /> msodbcsql11.lib 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  

