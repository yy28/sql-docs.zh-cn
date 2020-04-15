---
title: ODBC 功能和可视化福克斯 Pro ODBC 驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- ODBC level 1 API functions [ODBC]
- functions [ODBC], API
- ODBC API functions [ODBC]
- level 1 API functions [ODBC]
- API functions [ODBC]
- core level API functions [ODBC]
- level 2 API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 512f9cee-ffad-439b-b612-b49c34c32658
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26bb1f24a7dbb307d3048b8ec2a8ae293ddbe7ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298097"
---
# <a name="odbc-functions-and-the-visual-foxpro-odbc-driver"></a>ODBC 函数和 Visual FoxPro ODBC 驱动程序
本节中的主题简要概述了 ODBC API 功能以及任何特定于 Visual FoxPro 的详细信息。  
  
> [!NOTE]  
>  有关 ODBC 函数的一般信息，请参阅"ODBC 程序员指南"中的[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 ODBC API 函数已划分为三个主要类别：核心级 API 函数、1 级 API 函数和 2 级 API 函数。  
  
> [!NOTE]  
>  根据数据源是定义为与[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)目录 （.dbf 文件） 或 Visual FoxPro[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 文件） 的连接，一些函数的行为会有所不同。 某些操作仅支持数据库连接。  
  
## <a name="core-level-api-support"></a>核心级 API 支持  
 下表列出了 ODBC 核心级 API 函数。 所有这些功能都由 Visual FoxPro ODBC 驱动程序提供支持。  
  
|||  
|-|-|  
|[SQLAlloc连接](../../odbc/microsoft/sqlallocconnect-visual-foxpro-odbc-driver.md)|[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)|  
|[SQLAllocEnv](../../odbc/microsoft/sqlallocenv-visual-foxpro-odbc-driver.md)|[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)|  
|[SQLAllocStmt](../../odbc/microsoft/sqlallocstmt-visual-foxpro-odbc-driver.md)|[SQLFreeConnect](../../odbc/microsoft/sqlfreeconnect-visual-foxpro-odbc-driver.md)|  
|[SQLBindCol](../../odbc/microsoft/sqlbindcol-visual-foxpro-odbc-driver.md)|[SQLFreeEnv](../../odbc/microsoft/sqlfreeenv-visual-foxpro-odbc-driver.md)|  
|[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)|[SQLFreeStmt](../../odbc/microsoft/sqlfreestmt-visual-foxpro-odbc-driver.md)|  
|[SQLColattributes](../../odbc/microsoft/sqlcolattributes-visual-foxpro-odbc-driver.md)|[SQLGetCursorName](../../odbc/microsoft/sqlgetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)|[SQLNumResultCols](../../odbc/microsoft/sqlnumresultcols-visual-foxpro-odbc-driver.md)|  
|[SQLDescribeCol](../../odbc/microsoft/sqldescribecol-visual-foxpro-odbc-driver.md)|[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)|  
|[SQL 断开](../../odbc/microsoft/sqldisconnect-visual-foxpro-odbc-driver.md)|[SQLRowCount](../../odbc/microsoft/sql-row-count-visual-foxpro-odbc-driver.md)|  
|[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)|[SQLSetCursor 名称](../../odbc/microsoft/sqlsetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)|[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-1-api-support"></a>1 级 API 支持  
 下表列出了 ODBC 级别 1 API 函数。 所有这些功能都全部或部分由 Visual FoxPro ODBC 驱动程序提供支持。  
  
|||  
|-|-|  
|[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)|[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)|  
|[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)|[SQLParamData](../../odbc/microsoft/sqlparamdata-visual-foxpro-odbc-driver.md)|  
|[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)|[SQLPutData](../../odbc/microsoft/sqlputdata-visual-foxpro-odbc-driver.md)|  
|[SQLGetConnectOption](../../odbc/microsoft/sqlgetconnectoption-visual-foxpro-odbc-driver.md)|[SQLSet 连接选项](../../odbc/microsoft/sqlsetconnectoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetData](../../odbc/microsoft/sqlgetdata-visual-foxpro-odbc-driver.md)|[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetFunctions](../../odbc/microsoft/sqlgetfunctions-visual-foxpro-odbc-driver.md)|[SQLSpecialColumns](../../odbc/microsoft/sqlspecialcolumns-visual-foxpro-odbc-driver.md)|  
|[SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md)|[SQLStatistics](../../odbc/microsoft/sqlstatistics-visual-foxpro-odbc-driver.md)|  
|[SQLGetStmtOption](../../odbc/microsoft/sqlgetstmtoption-visual-foxpro-odbc-driver.md)|[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-2-api-support"></a>2 级 API 支持  
 以下 ODBC 级别 2 API 功能完全支持或部分支持：  
  
-   [SQLData源](../../odbc/microsoft/sqldatasources-visual-foxpro-odbc-driver.md)  
  
-   [SQLDrivers](../../odbc/microsoft/sqldrivers-visual-foxpro-odbc-driver.md)  
  
-   [SQL 扩展获取](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)  
  
-   [SQLMoreResults](../../odbc/microsoft/sqlmoreresults-visual-foxpro-odbc-driver.md)  
  
-   [SQLNumParams](../../odbc/microsoft/sqlnumparams-visual-foxpro-odbc-driver.md)  
  
-   [SQLParamOptions](../../odbc/microsoft/sqlparamoptions-visual-foxpro-odbc-driver.md)  
  
-   [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetPos](../../odbc/microsoft/sqlsetpos-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetScroll 选项](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)（部分支持）  
  
 不支持以下 2 级 API 功能：  
  
-   SQLBrowseConnect  
  
-   SQLColumnPrivileges  
  
-   SQLDescribeParam  
  
-   SQLForeignKeys  
  
-   SQLNativeSql  
  
-   SQLProcedureColumns  
  
-   SQLProcedures  
  
-   SQLTablePrivileges
