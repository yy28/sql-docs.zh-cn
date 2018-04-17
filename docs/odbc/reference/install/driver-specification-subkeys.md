---
title: 驱动程序规范子项 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52899dd2d473ac083d2d0effaca5b3b1726322c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="driver-specification-subkeys"></a>驱动程序规范子项
中的 ODBC 驱动程序子项列出每个驱动程序都有自己的子项。 此子项具有同名的 ODBC 驱动程序子项下的相应值。 此子项下的值列表的驱动程序和驱动程序安装程序 Dll，返回的驱动程序关键字的值的完整路径**SQLDrivers**，和使用情况计数。 值的格式为下表中所示。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**}|  
|CreateDSN|REG_SZ|*驱动程序说明*|  
|驱动程序|REG_SZ|*驱动程序的 DLL 的路径*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *文件 extension1*[**，\*。** *文件 extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安装|REG_SZ|*安装程序的 DLL 的路径*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*计数*|  
  
 每个关键字的使用下表所示。  
  
|关键字|用法|  
|-------------|-----------|  
|**APILevel**|一个数字，指示 ODBC 接口驱动程序支持的一致性级别：<br /><br /> 0 = 无<br /><br /> 1 = 级别 1 支持<br /><br /> 2 = 支持级别 2<br /><br /> 这必须是中的 SQL_ODBC_INTERFACE_CONFORMANCE 选项返回的值相同**SQLGetInfo**。|  
|**CreateDSN**|要在安装了驱动程序时创建的一个或多个数据源的名称。 系统信息必须包含用列出每个数据源的一个数据源规范部分**CreateDSN**关键字。 这些部分不应包含**驱动程序**关键字，因为这指定了在驱动程序规范部分中，但必须包含足够的信息供**ConfigDSN**驱动程序中的函数安装程序 DLL，而不显示任何对话框创建数据源规范。 数据源规范部分的格式，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**ConnectFunctions**|指示是否支持该驱动程序的三个字符字符串**SQLConnect**， **SQLDriverConnect**，和**SQLBrowseConnect**。 如果驱动程序支持**SQLConnect**，第一个字符是"Y"; 否则，它是"N"。 如果驱动程序支持**SQLDriverConnect**，第二个字符是"Y"; 否则，它是"N"。 如果驱动程序支持**SQLBrowseConnect**，第三个字符是"Y"; 否则，它是"N"。 例如，如果驱动程序支持**SQLConnect**和**SQLDriverConnect**但不是**SQLBrowseConnect**，三个字符的字符串是"YYN"。|  
|**DriverODBCVer**|具有 ODBC 驱动程序支持的版本字符串。 版本的形式*nn.nn*，其中前两个数字是否为主要版本，接下来的两位数字是次要版本。 有关本手册中所述的 ODBC 版本，该驱动程序必须返回"03.00"。<br /><br /> 这必须是中的 SQL_DRIVER_ODBC_VER 选项返回的值相同**SQLGetInfo**。|  
|**FileExtns**|对于基于文件的驱动程序的逗号分隔的文件扩展名的列表驱动程序可以使用。 例如，dBASE 驱动程序可能会指定\*.dbf 和格式化的文本文件驱动程序可能会指定\*.txt、\*.csv。 应用程序如何使用此信息的示例，请参阅**FileUsage**关键字。|  
|**FileUsage**|一个数字，指定如何基于文件的驱动程序直接处理数据源中的文件。<br /><br /> 0 = 驱动程序不是基于文件的驱动程序。 例如，ORACLE 驱动程序是基于 DBMS 的驱动程序。<br /><br /> 1 = 基于文件的驱动程序的视为文件数据源中为表。 例如，Xbase 驱动程序将每个 Xbase 文件视为一个表。<br /><br /> 2 = 为编录数据源中基于文件的驱动程序会将文件。 例如，Microsoft® Access 驱动程序将每个 Microsoft Access 文件视为整个数据库。<br /><br /> 应用程序可能会用于确定用户选择数据的方式。 例如，Xbase 和 Paradox 用户通常将数据存储在文件中，而 ORACLE 和 Microsoft Access 的用户通常将数据视为存储在表中。<br /><br /> 当用户选择**打开数据文件**从**文件**菜单上，应用程序可以显示**Windows 文件打开**通用对话框。 文件类型的列表将使用指定的文件扩展名**FileExtns**驱动程序指定的关键字**FileUsage**值 1 和"Y"作为第二个字符的值的**ConnectFunctions**关键字。 用户选择文件后，将调用应用程序**SQLDriverConnect**与**驱动程序**关键字，然后执行**选择\*FROM*表名称*** 语句。<br /><br /> 当用户选择**导入数据**从**文件**菜单上，应用程序可以显示的说明指定的驱动程序列表**FileUsage**值 0 或 2 和"Y"作为第二个字符的值的**ConnectFunctions**关键字。 用户选择驱动程序后，将调用应用程序**SQLDriverConnect**与**驱动程序**关键字，然后显示一个自定义**选择表**对话框。|  
|**SQLLevel**|一个数字，指定驱动程序支持的 SQL 92 语法：<br /><br /> 0 = SQL 92 条目<br /><br /> 1 = 过渡 FIPS127 2<br /><br /> 2 = SQL 92 中间<br /><br /> 3 = SQL 92 完整<br /><br /> 这必须是中的 SQL_SQL_CONFORMANCE 选项返回的值相同**SQLGetInfo**。|  
  
 有关使用情况计数的信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)本部分前面的。  
  
 应用程序不应设置的使用计数。 ODBC 将维护此计数。  
  
 例如，假设的驱动程序格式化的文本文件具有驱动程序名为 Text.dll 的 DLL，单独的驱动程序安装程序 DLL 名为 Txtsetup.dll，并已安装三次。 如果该驱动程序支持的级别 1 API 一致性级别，支持的最低 SQL 语法一致性级别，文件将其视为表，可以使用具有.txt 和.csv 扩展名的文件，该文本子项下的值可能如下所示：  
  
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
