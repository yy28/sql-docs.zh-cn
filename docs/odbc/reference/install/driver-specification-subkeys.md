---
title: 驱动程序规格子键 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280577"
---
# <a name="driver-specification-subkeys"></a>驱动程序规范子项
ODBC 驱动程序子键中列出的每个驱动程序都有其自己的子键。 此子键的名称与 ODBC 驱动程序子键下的相应值相同。 此子键下的值列出了驱动程序和驱动程序设置 DLL 的完整路径 **、SQLDriver**返回的驱动程序关键字的值以及使用情况计数。 值的格式如下表所示。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|API 级别|REG_SZ|**0** &#124; **1** &#124; **2**|  
|连接功能|REG_SZ|[**Y**&#124;**N****]** Y&#124;**N**=**Y**&#124;**N**||  
|创建DSN|REG_SZ|*驱动程序描述*|  
|驱动程序|REG_SZ|*驱动程序-DLL 路径*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|文件 Extns|REG_SZ|**\*.** *文件扩展名1*=**\*。** *文件扩展名2*|...|  
|文件使用|REG_SZ|**0** &#124; **1** &#124; **2**|  
|设置|REG_SZ|*设置-DLL路径*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|使用情况计数|REG_DWORD|*count*|  
  
 下表显示了每个关键字的使用。  
  
|关键字|使用情况|  
|-------------|-----------|  
|**API 级别**|指示驱动程序支持的 ODBC 接口一致性级别的数字：<br /><br /> 0 = 无<br /><br /> 1 = 支持 1 级<br /><br /> 2 = 支持 2 级<br /><br /> 这必须与**SQLGetInfo**中SQL_ODBC_INTERFACE_CONFORMANCE选项返回的值相同。|  
|**创建DSN**|安装驱动程序时要创建的一个或多个数据源的名称。 系统信息必须包含一个数据源规范部分，用于**使用 CreateDSN**关键字列出的每个数据源。 这些节不应包括**Driver**关键字，因为这在驱动程序规范部分中指定，但必须在驱动程序设置 DLL 中包含足够的**ConfigDSN**函数的信息，以创建数据源规范而不显示任何对话框。 有关数据源规范部分的格式，请参阅[数据源规范子键](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**连接功能**|一个三字符字符串，指示驱动程序是否支持**SQLConnect、SQLDriverConnect**和**SQLBrowseConnect**。 **SQLConnect** 如果驱动程序支持**SQLConnect，** 则第一个字符为"Y";如果驱动程序支持 SQLConnect，则第一个字符为"Y"。"，则为"Y"。"，则为"Y"。"，则为否则，它是"N"。 如果驱动程序支持**SQLDriverConnect，** 则第二个字符为"Y";如果驱动程序支持 SQLDriverConnect，则第二个字符为"Y"。"，则为"Y"。"，则为"Y"。"，则为"否则，它是"N"。 如果驱动程序支持**SQLBrowseConnect，** 则第三个字符为"Y";如果驱动程序支持 SQLBrowseConnect，则第三个字符为"Y"。"，则为"Y"。"，则为"Y"。"，则为"否则，它是"N"。 例如，如果驱动程序支持**SQLConnect**和**SQLDriverConnect，** 但不支持**SQLBrowseConnect，** 则三个字符字符串为"YYN"。|  
|**DriverODBCVer**|具有驱动程序支持的 ODBC 版本的字符串。 版本是形式*nn.nn，* 其中前两位数字是主要版本，接下来的两位数字是次要版本。 对于本手册中描述的 ODBC 版本，驱动程序必须返回"03.00"。<br /><br /> 这必须与**SQLGetInfo**中SQL_DRIVER_ODBC_VER选项返回的值相同。|  
|**文件 Extns**|对于基于文件的驱动程序，驱动程序可以使用的文件扩展名的逗号分隔列表。 例如，dBASE 驱动程序可能指定\*.dbf，格式化的文本文件驱动程序可能指定\*.txt..csv。\* 有关应用程序如何使用此信息的示例，请参阅**文件使用**关键字。|  
|**文件使用**|指示基于文件的驱动程序如何处理数据源中的文件的数字。<br /><br /> 0 = 驱动程序不是基于文件的驱动程序。 例如，ORACLE 驱动程序是基于 DBMS 的驱动程序。<br /><br /> 1 = 基于文件的驱动程序将数据源中的文件视为表。 例如，Xbase 驱动程序将每个 Xbase 文件视为表。<br /><br /> 2 = 基于文件的驱动程序将数据源中的文件视为目录。 例如，Microsoft®访问驱动程序将每个 Microsoft Access 文件视为一个完整的数据库。<br /><br /> 应用程序可能用它来确定用户如何选择数据。 例如，Xbase 和 Paradox 用户通常认为数据存储在文件中，而 ORACLE 和 Microsoft Access 用户通常认为数据存储在表中。<br /><br /> 当用户从 **"文件**"菜单中选择 **"打开的数据文件"** 时，应用程序可以显示**Windows 文件打开**通用对话框。 文件类型列表将使用**FileExtns**关键字指定的文件扩展名，用于指定**FileUse**值 1 和"Y"作为**ConnectFunctions**关键字值的第二个字符的驱动程序。 用户选择文件后，应用程序将使用**DRIVER**关键字调用**SQLDriverConnect，** 然后执行**\*SELECT FROM*表名*** 语句。<br /><br /> 当用户从 **"文件"** 菜单中选择 **"导入数据**"时，应用程序可以显示指定**文件使用**值 0 或 2 的驱动程序的说明列表，以及作为**ConnectFunctions**关键字值的第二个字符的"Y"的说明列表。 用户选择驱动程序后，应用程序将使用**DRIVER**关键字调用**SQLDriverConnect，** 然后显示自定义**选择表**对话框。|  
|**SQLLevel**|指示驱动程序支持的 SQL-92 语法的数字：<br /><br /> 0 = SQL-92 条目<br /><br /> 1 = FIPS127-2 过渡<br /><br /> 2 = SQL-92 中间<br /><br /> 3 = SQL-92 完整<br /><br /> 这必须与**SQLGetInfo**中SQL_SQL_CONFORMANCE选项返回的值相同。|  
  
 有关使用情况计数的信息，请参阅本节前面[先查看使用情况计数](../../../odbc/reference/install/usage-counting.md)。  
  
 应用程序不应设置使用计数。 ODBC 将保留此计数。  
  
 例如，假设格式化文本文件的驱动程序具有名为 Text.dll 的驱动程序 DLL，一个单独的驱动程序设置 DLL 名为 Txtsetup.dll，并且已安装三次。 如果驱动程序支持级别 1 API 一致性级别，支持最小 SQL 语法一致性级别，将文件视为表，并且可以使用具有 .txt 和 .csv 扩展名的文件，则 Text 子键下的值可能如下所示：  
  
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
