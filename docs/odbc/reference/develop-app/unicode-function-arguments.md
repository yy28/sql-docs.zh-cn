---
title: "Unicode 函数自变量 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff461881ea10c904ceefd1c51a364984ca10971b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="unicode-function-arguments"></a>Unicode 函数自变量
ODBC 3.5 （或更高版本） 驱动程序管理器支持 ANSI 和 Unicode 版本的所有接受指向字符字符串或 SQLPOINTER 在自变量的指针的函数。 Unicode 函数作为函数来实现 (为后缀*W*)，而不是宏。 ANSI 函数 (其可以调用使用或不是由后缀为*A*) 是等于当前的 ODBC API 函数。  
  
## <a name="remarks"></a>注释  
 作为计数的字符传递 Unicode 函数，始终返回或将字符串或长度参数。 对于返回的服务器数据的长度信息的函数，显示大小和精度所述的字符数。 当无法引用字符串或非字符串数据的长度 （传输的数据大小） 时，长度是八位字节长度中所述。 例如， **SQLGetInfoW**操作仍将需要用作计数的字节长度但**SQLExecDirectW**将使用的字符的计数。  
  
 计数的字符是指的字节数 （八进制） ANSI 函数和 UNICODE 函数 WCHAR （16 位字） 的数目。 具体而言，双字节字符序列 (DBCS) 或多字节字符序列 (MBCS) 可能包括多个字节。 可以由多个 WCHARs 组成 utf-16 Unicode 字符序列。  
  
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
>  已弃用的函数具有 Unicode ANSI 映射支持，因为 ODBC 3*.x*驱动程序管理器支持重新编译 ODBC 2。*x*具有 UNICODE 应用程序**#define**。  
  
 本部分包含以下主题。  
  
-   [Unicode 应用程序](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [函数映射中驱动程序管理器](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)

