---
title: 驱动程序规范子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b15aa278e2fe38afe93f5628433a6c8f4b41cd8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198317"
---
# <a name="driver-specification-subkeys"></a>驱动程序规范子项
在 ODBC 驱动程序的子项中列出每个驱动程序具有其自己的子项。 此子项有同名的 ODBC 驱动程序子项下的相应值。 此子项下的值中列出的驱动程序和驱动程序安装程序 Dll，返回的驱动程序关键字的值的完整路径**SQLDrivers**，和使用情况计数。 值的格式为下表中所示。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*driver-description*|  
|驱动程序|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *文件 extension1*[ **，\*。** *file-extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安装|REG_SZ|*setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*计数*|  
  
 下表中显示的每个关键字使用。  
  
|关键字|用法|  
|-------------|-----------|  
|**APILevel**|一个数字，指示 ODBC 接口驱动程序支持的一致性级别：<br /><br /> 0 = 无<br /><br /> 1 = 1 级支持<br /><br /> 2 = 2 级支持<br /><br /> 这必须是与中的 SQL_ODBC_INTERFACE_CONFORMANCE 选项返回的值相同**SQLGetInfo**。|  
|**CreateDSN**|若要安装该驱动程序时创建的一个或多个数据源的名称。 系统信息必须包含一个数据源规范部分列出与每个数据源**CreateDSN**关键字。 不应包含这些部分**驱动程序**关键字，因为这指定了在驱动程序规范部分中，但必须包含足够的信息供**ConfigDSN**驱动程序中的函数安装程序 DLL 而不显示任何对话框创建数据源规范。 有关数据源规范部分的格式，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**ConnectFunctions**|包含三个字符的字符串，该值指示是否支持该驱动程序**SQLConnect**， **SQLDriverConnect**，并**SQLBrowseConnect**。 如果该驱动程序支持**SQLConnect**，第一个字符为"Y"; 否则，它是"N"。 如果该驱动程序支持**SQLDriverConnect**，第二个字符为"Y"; 否则，它是"N"。 如果该驱动程序支持**SQLBrowseConnect**，第三个字符"Y"; 否则，它是"N"。 例如，如果驱动程序支持**SQLConnect**并**SQLDriverConnect**但不是**SQLBrowseConnect**，三个字符字符串是"YYN"。|  
|**DriverODBCVer**|使用 ODBC 驱动程序支持的版本字符串。 版本是窗体*nn.nn*，其中前两个数字是否为主要版本，接下来的两位数字是次要版本。 有关 ODBC 本手册中所述的版本，则驱动程序必须返回"03.00"。<br /><br /> 这必须是与中的 SQL_DRIVER_ODBC_VER 选项返回的值相同**SQLGetInfo**。|  
|**FileExtns**|有关基于文件的驱动程序，以逗号分隔列表的文件扩展名的驱动程序可以使用。 例如，指定 dBASE 驱动程序可能\*.dbf 和格式化的文本文件驱动程序可能会指定\*.txt，\*.csv。 有关如何应用程序可能会使用此信息的示例，请参阅**FileUsage**关键字。|  
|**FileUsage**|指示如何基于文件的驱动程序直接处理数据源中的文件的数字。<br /><br /> 0 = 驱动程序不是基于文件的驱动程序。 例如，ORACLE 驱动程序是基于 DBMS 的驱动程序。<br /><br /> 1 = 为表的基于文件的驱动程序将文件数据源中。 例如，Xbase 驱动程序将每个 Xbase 文件视为一个表。<br /><br /> 2 = 为编录数据源中的基于文件的驱动程序处理文件。 例如，Microsoft® Access 驱动程序将每个 Microsoft Access 文件视为完整的数据库。<br /><br /> 应用程序可以使用此来确定用户将如何选择数据。 例如，Xbase 和 Paradox 用户通常将存储在文件中，而 ORACLE 和 Microsoft Access 用户通常认为数据是存储在表中的数据。<br /><br /> 如果用户选择**打开数据文件**从**文件**菜单中，应用程序可以显示**Windows 文件打开**公共对话框。 文件类型的列表将使用指定的文件扩展名**FileExtns**指定的驱动程序的关键字**FileUsage**值 1 的值的第二个字符"Y" **ConnectFunctions**关键字。 用户选择文件后，应用程序将调用 **SQLDriverConnect** 与 **驱动程序** 关键字，然后执行 **选择** \*FROM *表名称* 语句。<br /><br /> 当用户选择**导入数据**从**文件**菜单中，应用程序无法显示的说明指定的驱动程序列表**FileUsage**值为 0 或 2 和"Y"值的第二个字符作为**ConnectFunctions**关键字。 应用程序在用户选择一个驱动程序后，将调用**SQLDriverConnect**与**驱动程序**关键字，然后显示一个自定义**选择表**对话框。|  
|**SQLLevel**|一个数字，指示由驱动程序支持的 SQL-92 语法：<br /><br /> 0 = SQL-92 条目<br /><br /> 1 = 过渡 FIPS127 2<br /><br /> 2 = SQL-92 中间<br /><br /> 3 = SQL-92 Full<br /><br /> 这必须是与中的 SQL_SQL_CONFORMANCE 选项返回的值相同**SQLGetInfo**。|  
  
 有关使用情况计数信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)本部分前面。  
  
 应用程序不应设置的使用计数。 ODBC 将保持此计数。  
  
 例如，假设用于格式化的文本的文件的驱动程序具有驱动程序 DLL 名为 Text.dll，单独的驱动程序安装程序 DLL 名为 Txtsetup.dll，并已安装三次。 如果驱动程序支持的级别 1 API 一致性级别、 支持最小 SQL 语法的一致性级别，将文件视为表，并且可以使用具有.txt 和.csv 扩展名的文件，在文本子项下的值可能如下所示：  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
