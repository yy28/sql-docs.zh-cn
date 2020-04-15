---
title: 药点。EXE |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307528"
---
# <a name="odbcconfexe"></a>药点。Exe
ODBCCONF.exe 是一个命令行工具，允许您配置 ODBC 驱动程序和数据源名称。  
  
> [!NOTE]  
>  ODBCCONF.exe 将在将来版本的 Windows 数据访问组件中删除。 避免使用此功能，并计划修改当前使用此功能的应用程序。 您可以使用 PowerShell 命令来管理驱动程序和数据源。 有关这些 PowerShell 命令的详细信息，请参阅[Windows 数据访问组件 cmdlet](/powershell/module/wdac)。  
  
## <a name="syntax"></a>语法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>参数  
 *开关*  
 零个或多个开关选项。 有关可用交换机的列表，请参阅本主题后面的备注部分。  
  
 *行动*  
 要执行一个操作。 有关可用选项的列表，请参阅备注部分。  
  
## <a name="remarks"></a>备注  
 以下交换机可用：  
  
|开关|描述|  
|------------|-----------------|  
|/A =*操作*||指定操作。<br /><br /> 如果只指定一个操作，则 /A 是可选的。|  
|/?|显示 ODBCCONF 的使用情况。Exe。|  
|/C|如果操作失败，处理将继续。|  
|/E|处理完成后，擦除使用 /F 指定的响应文件。|  
|/F|使用响应文件，如`odbcconf /F my.rsp`。<br /><br /> 我的.rsp 可能如下所示：`REGSVR c:\my.dll`<br /><br /> /A 不在响应文件中使用。|  
|/H|显示使用情况（帮助）。 此开关与 /？ 相同。|  
|/L+*模式*=*文件名*|以三种模式之一将程序输出发送到文件：普通 （n）、详细 （v） 和调试 （d）。 调试模式记录由 odbcconf.exe 加载的 DLL。<br /><br /> 如果指定 /L 而不带模式，日志文件将为空。<br /><br /> 例如 **，/Lv log.txt**。|  
|/R|重新启动后将执行该操作。|  
|/S|静默模式。 不显示错误消息。|  
  
 可使用以下操作：  
  
|操作|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name_特定于驱动程序的配置参数*|加载相应的驱动程序设置 DLL 并调用**ConfigDriver**函数。<br /><br /> 等效于[SQLConfig驱动程序函数](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGDRIVER " 驱动程序名称" "CPTimeout=60"]<br /><br /> /A [CONFIGDRIVER " 驱动程序名称" "驱动程序+03.80"]|  
|CONFIGDSN *driver_name* DSN_*名称*&#124;*属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGDSN"SQL 服务器""DSN_名称&#124;服务器_srv"]|  
|CONFIGSYSDSN *driver_name* DSN**名称*&#124;*属性*|添加或修改系统数据源。<br /><br /> 等效于[SQLConfigDataSource 函数](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGSYSDSN"SQL 服务器""DSN_名称&#124;服务器=srv"]|  
|安装驱动程序|等效于[SQLInstallDriverEx 函数](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 有关传递给 INSTALLDRIVER 的关键字-值对语法的信息，请参阅[驱动程序规范子键](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A [SETUPDRIVER"您的驱动程序&#124;驱动程序\c：\&#124;安装程序\c：\您的.dll &#124; APILevel_2 &#124;连接功能_YYy&#124;驱动程序ODBCVer_03.50 &#124;文件使用情况{0 &#124; SQLLevel_1"]|  
|安装*转换器配置_驱动程序路径*|将有关转换器的信息添加到**HKEY_LOCAL_MACHINE_软件_ODBC_ODBCINST。INI_ODBC 译员**注册表项。<br /><br /> 等效于[SQLInstall 翻译器Ex 函数](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 有关传递给 INSTALLDRIVER 的关键字-值对语法的信息，请参阅[翻译器规范子键](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A [安装翻译&#124;翻译器\c：\my.dll &#124;安装程序\c：\my.dll"]|  
|REGSVR *dll*|注册 DLL。<br /><br /> 等效于 regsvr32.exe。<br /><br /> 例如：<br /><br /> /A [REGSVR c：[my.dll]|  
|塞特·拉迪斯纳尔迪|当HKEY_LOCAL_MACHINE_软件_ODBC_ODBC时。INI_ODBC 文件 DSN_默认DSNDir不存在，SETFILEDSNDIR 操作将创建它，并在HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Windows_当前版本_常见文件Dir处为其分配值，并附加了 [ODBC_数据源》。<br /><br /> HKEY_LOCAL_MACHINE_软件_ODBC_ODBC 处的值。INI_ODBC 文件 DSN_默认DSNDir指定 ODBC 数据源管理员在创建基于文件的数据源时使用的默认位置。<br /><br /> 例如：<br /><br /> /A [SETFILEDSNDIR]|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 开放式数据库连接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
