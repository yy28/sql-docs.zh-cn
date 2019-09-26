---
title: 系统要求、安装和驱动程序文件 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8e7098cbd454b37e7de0a221c55b86194f883c3
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71250943"
---
# <a name="system-requirements-installation-and-driver-files"></a>系统要求、安装和驱动程序文件

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文讨论连接到 SQL Server 的 ODBC 驱动程序。

## <a name="driver-versions"></a>驱动程序版本

| 驱动程序版本 | 支持说明 |
| :------------- | :--------------------- |
| ODBC Driver 11 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 支持与 SQL Server 2014、SQL Server 2012、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]、和[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]的连接。 |
| 适用于 Windows 的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC Driver 11 for | 可以安装在还具有一个或多个本机客户端版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]计算机上。 |
| ODBC Driver 13 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 支持与 SQL Server 2016、SQL Server 2014、SQL Server 2012、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]和[!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]的连接。 |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]， <br/> 除了上述13 | 支持 SQL Server 2017。 |
| ODBC Driver 17 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 支持与13.1 相同的数据库版本。 |
| 适用于 SQL Server 的 ODBC 驱动程序 17 | 支持从驱动程序版本17.3 开始 SQL Server 2019。 |
| &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>连接字符串详细信息

在连接字符串中指定的驱动程序名称为`ODBC Driver 11 for SQL Server`或`ODBC Driver 13 for SQL Server` (对于13和 13.1) 或`ODBC Driver 17 for SQL Server`。

## <a name="supported-operating-systems"></a>受支持的操作系统

可通过驱动程序在下列 Windows 操作系统上运行应用程序：  

- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Vista SP2 &nbsp; _（仅限 ODBC Driver 11）_
- Windows 7
- Windows 8
- Windows 8.1
- Windows 10

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安装 Microsoft ODBC Driver for SQL Server

从以下链接之一运行`msodbcsql.msi`时, 将安装该驱动程序:

- [在 Windows 上下载 Microsoft ODBC Driver 17 for SQL Server](https://www.microsoft.com/download/details.aspx?id=56567)
- [在 Windows 上下载 Microsoft ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)
- [在 Windows 上下载 Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)
- [在 Windows 上下载 Microsoft ODBC Driver 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36434)

> [!NOTE]
> 对于安装了驱动程序17.1.0.1 或以下的用户，建议在安装较新版本的驱动程序之前手动将其卸载。

### <a name="side-by-side-with-native-client"></a>与 Native Client 并行

驱动程序可以与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 并行安装。

调用 `msodbcsql.msi` 时，默认仅安装客户端组件。 客户端组件是一些文件，它们支持运行通过驱动程序开发的应用程序。 要安装 SDK 组件，请在命令行中指定 `ADDLOCAL=ALL`。 以下是一个示例。
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>最终用户许可证

如果使用 `/passive`、`/qn`、`/qb` 或 `/qr` 选项进行安装，请指定 `IACCEPTMSODBCSQLLICENSETERMS=YES` 以接受最终用户许可条款。 必须以全大写字母指定此选项。 以下是一个示例。
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>无提示卸载

下面的示例演示如何执行无提示卸载。
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>指示依赖项

应用程序使用驱动程序时，该程序应指示它通过安装选项 `APPGUID` 依赖于驱动程序。 在卸载前，此指示可使驱动程序安装程序报告依赖的应用程序。 要在驱动程序上指定依赖项，请在无提示安装驱动程序时将 `APPGUID` 命令行参数设置为你的产品代码。 当使用 Microsoft Installer 捆绑应用程序安装程序时，必须创建产品代码。 以下是一个示例。
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>命令行工具：sqlcmd.exe 和 bcp.exe

用于驱动`sqlcmd.exe`程序的和工具可在[microsoft命令行实用程序11上下载SQLServer](https://www.microsoft.com/download/details.aspx?id=36433),[microsoft命令行实用程序13用于SQLServer](https://www.microsoft.com/download/details.aspx?id=52680),或microsoft命令行实用程序13.1`bcp.exe` [SQL Server](https://www.microsoft.com/download/details.aspx?id=53591)。 驱动程序是安装`sqlcmd.exe`和`bcp.exe`的必备组件。
  
`bcp.exe`和`sqlcmd.exe`安装`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` `130\Tools`在版本11的的子文件夹中,为13和13.1。`110\Tools`

对于使用 BCP 函数的应用程序，它指定的驱动程序必须来自与编辑应用程序所用的头文件和库一并传输的相同版本。  

例如, 使用`msodbcsql11.lib`和`msodbcsql.h`编译 ODBC 应用程序时, 请在连接字符串中使用 "DRIVER = {ODBC DRIVER 11 for SQL Server}"。

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的组件

Windows 上的 ODBC 驱动程序包含以下组件：

| 组件 | 描述 |
| :-------- | :---------- |
|msodbcsql17.dll 或 <br/> msodbcsql13.dll 或 <br/> msodbcsql11.dll|包含所有驱动程序功能的动态链接库 (DLL) 文件。 此文件安装在%Systemroot%\system32 中。|  
|msodbcdiag17 或 <br/> msodbcdiag13 或 <br/> msodbcdiag11.dll|包含驱动程序诊断 (跟踪) 界面的动态链接库 (DLL) 文件。 此文件安装在%Systemroot%\system32 中。|
|msodbcsqlr17.rll 或 <br/> msodbcsqlr13.rll 或 <br/> msodbcsqlr11.rll|驱动程序库的附带资源文件。 此文件安装在%Systemroot%\system32\1033 中。| 
|s13ch_msodbcsql.chm 或 <br/> s11ch_msodbcsql.chm |数据源向导帮助文件，它记录如何为驱动程序创建数据源。 此文件安装在%Systemroot%\system32\1033 中中。 <br /> <br /> **注意:** ODBC Driver 17 没有 chm 文件。 |  
|msodbcsql.h|头文件，它包含使用驱动程序所需的所有新定义。<br /><br /> **注意：**  你无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h for ODBC Driver 17 或 13 的安装路径为 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK。 <br /> ODBC Driver 11 msodbcsql.h 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。| 
|msodbcsql17.lib 或 <br/> msodbcsql13.lib 或 <br/> msodbcsql11.lib|库文件，调用属于驱动程序的 bcp 实用工具函数时需使用此文件  。<br /><br /> **注意：**  如果确实在程序中引用此库文件，请确保它在你的系统路径中，并且在使用该应用程序的系统路径中。<br /><br /> msodbcsql17.lib 或 msodbcsql13.lib 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。<br /> msodbcsql11.lib 安装在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另请参阅

[Windows 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
