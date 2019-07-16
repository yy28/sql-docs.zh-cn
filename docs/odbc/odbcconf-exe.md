---
title: ODBCCONF.EXE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7934226ec489af0ac0b1f655c7d27660cb6a928
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996267"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe 是一个命令行工具，可用于配置 ODBC 驱动程序和数据源名称。  
  
> [!NOTE]  
>  Windows 数据访问组件的未来版本中，将删除 ODBCCONF.exe。 避免使用此功能，并计划修改当前使用此功能的应用程序。 可以使用 PowerShell 命令来管理驱动程序和数据源。 有关这些 PowerShell 命令的详细信息，请参阅[Windows 数据访问组件 cmdlet](https://technet.microsoft.com/library/hh771019.aspx)。  
  
## <a name="syntax"></a>语法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>参数  
 *switches*  
 零个或多个交换机选项。 可用的参数的列表，请参阅本主题后面的备注部分。  
  
 *action*  
 要执行的一个操作。 有关可用选项的列表，请参阅备注部分。  
  
## <a name="remarks"></a>备注  
 提供了以下开关：  
  
|开关|描述|  
|------------|-----------------|  
|/ A {*操作*}|指定的操作。<br /><br /> 如果仅指定一个操作/A 是可选的。|  
|/?|为 ODBCCONF 显示使用情况。EXE。|  
|/C|如果操作失败，则继续进行处理。|  
|/E|清除时处理完成后，使用 /F 指定响应文件。|  
|/F|使用响应文件，如`odbcconf /F my.rsp`。<br /><br /> my.rsp 可能如下所示： `REGSVR c:\my.dll`<br /><br /> 响应文件中不使用/A。|  
|/H|显示使用情况 （帮助）。 此开关等同于 /？。|  
|/ L [*模式下*]*文件名*|发送到三种模式之一中的文件的程序输出： 标准 (n)、 详细 (v) 和调试 (d)。 调试模式下记录由 odbcconf.exe 加载的 Dll。<br /><br /> 如果没有一种模式指定 /L，日志文件将为空。<br /><br /> 例如， **/Lv log.txt**。|  
|/R|在重新启动后，将执行的操作。|  
|/S|静默模式。 不显示错误消息。|  
  
 提供了以下操作：  
  
|Action|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 特定于驱动程序的配置参数*|加载相应的驱动程序安装程序 DLL 并调用**ConfigDriver**函数。<br /><br /> 等效于[SQLConfigDriver 函数](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDRIVER"驱动程序名称""CPTimeout = 60"}<br /><br /> / A {CONFIGDRIVER"驱动程序名称""DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*名称* &#124; *属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*名称* &#124; *属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|/INSTALLDRIVER|等效于[SQLInstallDriverEx 函数](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 传递给 /installdriver 的关键字值对语法信息，请参阅[驱动程序规范子项](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {/installdriver"您的驱动程序&#124;Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR*转换器配置 * * 驱动程序路径*|添加了有关为转换器的信息**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 翻译人员**注册表项。<br /><br /> 等效于[SQLInstallTranslatorEx 函数](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 传递给 /installdriver 的关键字值对语法信息，请参阅[转换器规范子项](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {INSTALLTRANSLATOR"我转换器&#124;Translator=c:\my.dll &#124; Setup=c:\my.dll"}|  
|REGSVR *dll*|注册 DLL。<br /><br /> 等效于 regsvr32.exe。<br /><br /> 例如：<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|当 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC。INI\ODBC 文件 DSN\DefaultDSNDir 不存在，SETFILEDSNDIR 操作将创建它并将其分配 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir，后面附加有 \ODBC\Data 源处的值。<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 处的值。INI\ODBC 文件 DSN\DefaultDSNDir 指定创建基于文件的数据源时使用 ODBC 数据源管理器的默认位置。<br /><br /> 例如：<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 开放式数据库连接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
