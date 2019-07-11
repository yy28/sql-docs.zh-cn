---
title: Unicode 函数自变量 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83cb2faad86268c3270e9386ca10b25e4807e030
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793751"
---
# <a name="unicode-function-arguments"></a>Unicode 函数自变量
ODBC 3.5 （或更高版本） 驱动程序管理器支持所有函数接受字符串或 SQLPOINTER 中其自变量的指针的 ANSI 和 Unicode 的版本。 Unicode 函数作为函数实现 (为后缀*W*)，而不是宏。 ANSI 函数 (带有或不带后缀的可以调用*A*) 与当前的 ODBC API 函数完全相同。  
  
## <a name="remarks"></a>备注  
 Unicode 函数始终返回或需要字符串或长度参数将作为字符计数传递。 对于返回的服务器数据的长度信息的函数，显示大小和精度所述的字符数。 长度 （传输的数据大小） 无法引用字符串或非字符串数据，长度是八位字节长度中所述。 例如， **SQLGetInfoW**操作仍将需要为计数字节的长度，但**SQLExecDirectW**将使用的字符数。  
  
 字符数表示的字节数 （八进制） ANSI 函数和对于 UNICODE 函数 WCHAR （16 位字） 数。 具体而言，双字节字符序列 (DBCS) 或多字节字符序列 (MBCS) 可以包含多个字节。 可以包含多个 WCHARs utf-16 Unicode 字符序列。  
  
 下面是支持 Unicode (W) 和 ANSI (A) 版本的 ODBC API 函数的列表：  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
  
 下面是支持 Unicode (W) 和 ANSI (A) 版本的 ODBC 安装程序和 ODBC 转换器函数的列表：  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  已弃用的函数具有 Unicode 到 ANSI 映射支持，因为 ODBC *3.x*重新编译 ODBC 驱动程序管理器支持*2.x*应用程序使用 UNICODE **#define**.  
  
 本部分包含以下主题。  
  
-   [Unicode 应用程序](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驱动程序管理器中的函数映射](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
