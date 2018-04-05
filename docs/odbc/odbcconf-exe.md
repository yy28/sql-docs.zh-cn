---
title: ODBCCONF。EXE |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f22cf640a790f120701eda8424fb4c19edc7c49
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="odbcconfexe"></a>ODBCCONF。EXE
ODBCCONF.exe 是一个命令行工具，可以配置 ODBC 驱动程序和数据源名称。  
  
> [!NOTE]  
>  在 Windows 数据访问组件的未来版本中，将删除 ODBCCONF.exe。 请避免使用此功能，并计划修改当前使用此功能的应用程序。 可以使用 PowerShell 命令来管理驱动程序和数据源。 有关这些 PowerShell 命令的详细信息，请参阅[Windows 数据访问组件 cmdlet](https://technet.microsoft.com/library/hh771019.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>参数  
 *开关*  
 零个或多个交换机选项。 有关可用的交换机的列表，请参阅备注部分中的，本主题中后面。  
  
 *操作*  
 要执行的一个操作。 有关可用选项的列表，请参阅备注部分。  
  
## <a name="remarks"></a>注释  
 下列开关有：  
  
|开关|Description|  
|------------|-----------------|  
|/ A {*操作*}|指定操作。<br /><br /> / A 是可选的如果仅指定一个操作。|  
|/?|显示 ODBCCONF 使用情况。EXE。|  
|/C|操作失败时继续处理。|  
|/E|擦除处理结束时，使用 /F 指定响应文件。|  
|/F|使用响应文件，如`odbcconf /F my.rsp`。<br /><br /> my.rsp 可能如下所示：`REGSVR c:\my.dll`<br /><br /> 在响应文件中未使用/A。|  
|/H|显示使用情况 （帮助）。 此开关是相同 /？。|  
|/ L [*模式*] *filename*|程序输出发送到三种模式之一中的文件： 正常 (n)、 详细 (v) 和调试 (d)。 调试模式记录由 odbcconf.exe 加载的 Dll。<br /><br /> 如果指定 /L 不一种模式的情况下，日志文件将为空。<br /><br /> 例如， **/Lv log.txt**。|  
|/R|将在重启后执行的操作。|  
|/S|静默模式。 不会显示错误消息。|  
  
 有下列可用操作：  
  
|操作|Description|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name**特定于驱动程序的配置参数*|加载的适当的驱动程序安装程序 DLL 和调用**ConfigDriver**函数。<br /><br /> 等效于[SQLConfigDriver 函数](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDRIVER"驱动程序名称""CPTimeout = 60"}<br /><br /> / A {CONFIGDRIVER"驱动程序名称""DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*名称*&#124;*属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDSN"SQL Server""DSN = 名称 &#124;服务器 = srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*名称*&#124;*属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGSYSDSN"SQL Server""DSN = 名称 &#124;服务器 = srv"}|  
|INSTALLDRIVER|等效于[SQLInstallDriverEx 函数](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 有关传递给 INSTALLDRIVER 的关键字 / 值对语法的信息，请参阅[驱动程序规范子项](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {INSTALLDRIVER"驱动程序 &#124;Driver=c:\your.dll &#124;Setup=c:\your.dll &#124;APILevel = 2 &#124;ConnectFunctions = YYY &#124;DriverODBCVer = 03.50 &#124;FileUsage = 0 &#124;SQLLevel = 1"}|  
|INSTALLTRANSLATOR*转换器配置**驱动程序路径*|将添加到转换器有关的信息**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 转换器**注册表项。<br /><br /> 等效于[SQLInstallTranslatorEx 函数](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 有关传递给 INSTALLDRIVER 的关键字 / 值对语法的信息，请参阅[转换器规范子项](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {INSTALLTRANSLATOR"我转换器 &#124;Translator=c:\my.dll &#124;Setup=c:\my.dll"}|  
|REGSVR *dll*|注册 DLL。<br /><br /> 等效于 regsvr32.exe。<br /><br /> 例如：<br /><br /> / A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|当 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC。INI\ODBC 文件 DSN\DefaultDSNDir 不存在，SETFILEDSNDIR 操作会创建并将其分配 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir，后面附加有 \ODBC\Data 源处的值。<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 处的值。INI\ODBC 文件 DSN\DefaultDSNDir 指定创建基于文件的数据源时使用 ODBC 数据源管理器的默认位置。<br /><br /> 例如：<br /><br /> / A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 开放式数据库连接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
