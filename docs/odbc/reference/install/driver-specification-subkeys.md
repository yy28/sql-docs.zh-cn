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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280577"
---
# <a name="driver-specification-subkeys"></a>驱动程序规范子项
ODBC 驱动程序子项中列出的每个驱动程序都有自己的子项。 此子项与 ODBC 驱动程序子项下的相应值具有相同的名称。 此子项下的值列出了驱动程序和驱动程序安装 Dll 的完整路径、 **SQLDrivers**返回的驱动程序关键字的值和使用计数。 值的格式如下表中所示。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**N**} {**y**&#124;**N**}|  
|CreateDSN|REG_SZ|*驱动程序-说明*|  
|驱动程序|REG_SZ|*驱动程序-DLL-路径*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *extension1*[**，\*.** *文件-extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|设置|REG_SZ|*设置-DLL-路径*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*计数*|  
  
 下表显示了每个关键字的用法。  
  
|关键字|使用情况|  
|-------------|-----------|  
|**APILevel**|指示驱动程序支持的 ODBC 接口一致性级别的数字：<br /><br /> 0 = 无<br /><br /> 1 = 支持级别1<br /><br /> 2 = 支持级别2<br /><br /> 此值必须与在**SQLGetInfo**中为 SQL_ODBC_INTERFACE_CONFORMANCE 选项返回的值相同。|  
|**CreateDSN**|要在安装驱动程序时创建的一个或多个数据源的名称。 对于用**CreateDSN**关键字列出的每个数据源，系统信息必须包括一个 "数据源规范" 部分。 这些部分不应包含**driver**关键字，因为它是在驱动程序规范部分中指定的，但必须包含足够的信息，以便驱动程序安装程序 DLL 中的**ConfigDSN**函数在不显示任何对话框的情况下创建数据源规范。 有关 "数据源规范" 部分的格式，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**ConnectFunctions**|三个字符的字符串，用于指示驱动程序是否支持**SQLConnect**、 **SQLDriverConnect**和**SQLBrowseConnect**。 如果驱动程序支持**SQLConnect**，则第一个字符为 "Y";否则为 "N"。 如果驱动程序支持**SQLDriverConnect**，则第二个字符为 "Y";否则为 "N"。 如果驱动程序支持**SQLBrowseConnect**，则第三个字符是 "Y";否则为 "N"。 例如，如果驱动程序支持**SQLConnect**和**SQLDriverConnect**而不是**SQLBrowseConnect**，则三个字符的字符串为 "YYN"。|  
|**DriverODBCVer**|一个字符串，其中包含驱动程序支持的 ODBC 版本。 版本的格式为*nn. nn*，其中前两位数字是主版本，接下来的两位数字是次版本。 对于本手册中所述的 ODBC 版本，驱动程序必须返回 "03.00"。<br /><br /> 此值必须与在**SQLGetInfo**中为 SQL_DRIVER_ODBC_VER 选项返回的值相同。|  
|**FileExtns**|对于基于文件的驱动程序，驱动程序可以使用的文件扩展的逗号分隔列表。 例如，dBASE 驱动程序可以指定\*.dbf，而格式化的文本文件驱动程序可能会指定\*.txt、\*.csv。 有关应用程序如何使用此信息的示例，请参阅**FileUsage**关键字。|  
|**FileUsage**|一个数字，指示基于文件的驱动程序如何直接处理数据源中的文件。<br /><br /> 0 = 驱动程序不是基于文件的驱动程序。 例如，ORACLE 驱动程序是基于 DBMS 的驱动程序。<br /><br /> 1 = 基于文件的驱动程序以表的形式处理数据源中的文件。 例如，Xbase 驱动程序将每个 Xbase 文件视为一个表。<br /><br /> 2 = 基于文件的驱动程序将数据源中的文件视为目录。 例如，Microsoft® Access 驱动程序将每个 Microsoft Access 文件视为一个完整数据库。<br /><br /> 应用程序可以使用它来确定用户将如何选择数据。 例如，Xbase 和 Paradox 用户通常会将数据视为存储在文件中，而 ORACLE 和 Microsoft Access 用户通常会将数据视为表中存储的数据。<br /><br /> 当用户从 "**文件**" 菜单中选择 "**打开数据文件**" 时，应用程序可能会显示 " **Windows 文件打开**通用" 对话框。 文件类型列表将使用**FileExtns**关键字指定的文件扩展名作为指定**FileUsage**值1和 "Y" 的驱动程序，将值指定为**ConnectFunctions**关键字值的第二个字符。 用户选择文件后，应用程序将使用**DRIVER**关键字调用**SQLDriverConnect** ，然后执行**SELECT \* FROM *table name* **语句。<br /><br /> 当用户从 "**文件**" 菜单中选择 "**导入数据**" 时，应用程序可以显示指定**FileUsage**值为0或2的驱动程序的描述列表，并显示 "Y" 作为**ConnectFunctions**关键字值的第二个字符。 用户选择驱动程序后，应用程序将使用**driver**关键字调用**SQLDriverConnect** ，然后显示自定义的 "**选择表**" 对话框。|  
|**SQLLevel**|一个数字，用于指示驱动程序支持的 SQL-92 语法：<br /><br /> 0 = SQL-92 项<br /><br /> 1 = FIPS127-2 个过渡<br /><br /> 2 = SQL-92 中间<br /><br /> 3 = SQL-92 Full<br /><br /> 此值必须与在**SQLGetInfo**中为 SQL_SQL_CONFORMANCE 选项返回的值相同。|  
  
 有关使用计数的详细信息，请参阅本部分前面的[使用计数](../../../odbc/reference/install/usage-counting.md)。  
  
 应用程序不应设置使用计数。 ODBC 将维护此计数。  
  
 例如，假设格式化文本文件的驱动程序具有一个名为 "Txtsetup.oem" 的驱动程序 DLL，该 dll 是一个名为 "" 的独立驱动程序安装程序 DLL，并且已安装了三次。 如果驱动程序支持第1级 API 一致性级别，则支持最低 SQL 语法一致性级别，将文件视为表，并可使用带有 .txt 和 .csv 扩展名的文件，Text 子项下的值可能如下所示：  
  
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
