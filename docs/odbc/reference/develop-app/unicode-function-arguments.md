---
title: 单代码函数参数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284287"
---
# <a name="unicode-function-arguments"></a>Unicode 函数自变量
ODBC 3.5（或更高版本）驱动程序管理器支持所有函数的 ANSI 和 Unicode 版本，这些函数在其参数中接受指向字符串或 SQLPOINTER 的指针。 Unicode 函数作为函数实现（后缀为*W），* 而不是宏。 ANSI 函数（可以使用或不使用*A*的后缀调用）与当前的 ODBC API 函数相同。  
  
## <a name="remarks"></a>备注  
 始终返回或获取字符串或长度参数的 Unicode 函数作为字符计数传递。 对于返回服务器数据长度信息的函数，显示大小和精度以字符数表示。 当长度（数据的传输大小）可以引用字符串或非字符串数据时，长度以八点长度描述。 例如 **，SQLGetInfoW**仍将长度作为字节数，但**SQLExecDirectW**将使用字符计数。  
  
 字符计数是指 ANSI 函数的字节数（八位数）和 UNICODE 函数的 WCHAR（16 位字数）。 特别是，双字节字符序列 （DBCS） 或多字节字符序列 （MBCS） 可以由多个字节组成。 UTF-16 Unicode 字符序列可以由多个 WR 组成。  
  
 以下是支持 Unicode （W） 和 ANSI （A） 版本的 ODBC API 函数的列表：  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColattributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLData源**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSet 连接选项**|  
|**SQLExecDirect**|**SQLSetCursor 名称**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 以下是支持 Unicode （W） 和 ANSI （A） 版本的 ODBC 安装程序和 ODBC 转换器函数的列表：  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstall驱动程序管理器**|  
|**SQLCreate数据源**|**SQL 安装程序错误**|  
|**SQLDataSourceto驱动程序**|**SQLInstallODBC**|  
|**SQLDriverto数据源**|**SQLReadFileDSN**|  
|**SQLGet 可驱动程序**|**SQLremoveSnfromINININ**|  
|**SQLGet 安装驱动程序**|**SQLValidDSN**|  
|**SQLGet 转换器**|**SQLwriteSntoINI**|  
|**SQL安装驱动程序**||  
  
> [!NOTE]
>  弃用函数具有 Unicode 到 ANSI 映射支持，因为 ODBC *3.x*驱动程序管理器支持使用 UNICODE **#define**重新编译 ODBC *2.x*应用程序。  
  
 本部分包含以下主题。  
  
-   [Unicode 应用程序](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驱动程序](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驱动程序管理器中的函数映射](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
