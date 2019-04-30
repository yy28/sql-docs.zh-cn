---
title: 连接转换 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f808460a1421a9ab4cb3a76c2810d810b9636b11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224508"
---
# <a name="connection-transitions"></a>连接转换
ODBC 连接具有以下状态。  
  
|State|Description|  
|-----------|-----------------|  
|C0|未分配的环境中，未分配的连接|  
|C1|分配的环境中，未分配的连接|  
|C2|分配环境中，分配连接|  
|C3|连接函数需要数据|  
|C4|已连接的连接|  
|C5|连接的连接，分配语句|  
|C6|已连接的连接，正在进行中的事务。 很可能处于状态 C6 不包含在连接上分配任何语句的连接。 例如，假设连接在手动提交模式下并处于状态 C4。 如果语句是分配、 执行 （从开始一个事务），并且然后释放，事务将保持活动状态，但在连接上没有语句。|  
  
 下表显示每个 ODBC 函数如何影响连接状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 没有 Env。|C1 的未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 此行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 此行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 调用**SQLAllocHandle**与*OutputHandlePtr*指向有效的句柄会覆盖该句柄而不考虑以前的内容 ofthat 句柄，并且可能会导致问题的 ODBC 驱动程序。 它是不正确的 ODBC 应用程序编程以调用**SQLAllocHandle**两次，为定义的相同应用程序变量 *\*OutputHandlePtr*而无需调用**SQLFreeHandle**以重新分配它之前释放句柄。 覆盖 ODBC 句柄以这种方式可能会导致不一致的行为或 ODBC 驱动程序部分的错误。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-C2 [d] [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] 的连接已在手动提交模式下。  
  
 [2] 的连接已在自动提交模式下。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 SQLStatistics、 SQLTablePrivileges 和 SQLTables  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] 的连接已在自动提交模式下，或数据源未开始事务。  
  
 [2] 的连接已在手动提交模式下，数据源开始事务。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、 SQLGetDescField、 SQLGetDescRec、 SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] 在此状态下，可用于应用程序的唯一说明符是显式分配描述符。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|-[4] 或 ([5]、 [6] 和 [8]) C4 [5] 和 [7] C5 [5]、 [6] 和 [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 由于连接处于连接状态不是，它是不受事务影响。  
  
 [4] 的提交和回滚失败的连接上。 在这种情况下，该函数返回 SQL_ERROR。  
  
 [5] 提交或回滚已成功连接上。 如果在另一个连接上提交或回滚失败或如果提交或回滚已成功上的所有连接，则函数将返回 SQL_SUCCESS，则函数将返回 SQL_ERROR。  
  
 [6] 时在连接上分配至少一个语句。  
  
 [7] 没有在连接上分配任何语句。  
  
 [8] 连接至少有一条语句为其存在已打开的游标，并且数据源可在提交或回滚事务时保持游标、 适用的为准 (具体取决于是否*CompletionType*已 SQL_提交或 SQL_ROLLBACK）。 有关详细信息，请参阅中的属性 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 [9] 如果连接没有打开的游标的任何语句，该事务已提交或回滚时未保留游标。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] 连接处于自动提交模式下，而执行的语句不是*游标**规范*（如 SELECT 语句）; 或者连接已被手动提交模式和语句执行未开始事务。  
  
 [2] 上，连接处于自动提交模式下，而执行的语句*游标**规范*（如 SELECT 语句）。  
  
 [3] 的连接已在手动提交模式下，数据源开始事务。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|-C4 [7] [5] 和 [8] C5 [6] 和 [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 此行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 此行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 没有在连接上分配的只有一条语句。  
  
 [6] 没有在连接上分配的多个语句。  
  
 [7] 的连接已在手动提交模式下。  
  
 [8] 的连接已在自动提交模式下。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] 该行显示的事务时*选项*参数是 SQL_CLOSE。  
  
 [2] 该行显示的事务时*选项*参数为 SQL_UNBIND 或 SQL_RESET_PARAMS。  
  
 [3] 上，连接处于自动提交模式下，而没有游标已打开此除外的任何语句。  
  
 [4] 的连接已在手动提交模式下或处于自动提交模式和至少一个其他语句打开游标的。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1]*特性*参数为 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或连接属性设置一个值。  
  
 [2]*特性*参数不为 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，和具有不为连接设置一个值属性。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 此行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 此行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1]*信息类型*参数为 SQL_ODBC_VER。  
  
 [2]*信息类型*参数不为 SQL_ODBC_VER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] 的连接是否处于自动提交模式，并且调用**SQLMoreResults**尚未初始化游标规范的结果集的处理。  
  
 [2] 的连接是否处于自动提交模式，并且调用**SQLMoreResults**已初始化游标规范的结果集的处理。  
  
 [3] 的连接已在手动提交模式下。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] 的连接已在自动提交模式下，或数据源未开始事务。  
  
 [2] 的连接已在手动提交模式下，数据源开始事务。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|-[3] 和 [6] C5 [8] [4] hy011 并显示 08002 [5] 或 [7]|  
  
 [1]*特性*SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION 参数不是。  
  
 [2]*特性*参数为 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3]*特性*SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE 参数不是。  
  
 [4]*特性*参数为 SQL_ATTR_ODBC_CURSORS。  
  
 [5]*特性*参数为 SQL_ATTR_PACKET_SIZE。  
  
 [6]*特性*参数不为 SQL_ATTR_AUTOCOMMIT，或*属性*参数为 SQL_ATTR_AUTOCOMMIT，将此属性设置未提交事务。  
  
 [7]*特性*参数为 SQL_ATTR_TXN_ISOLATION。  
  
 [8]*特性*参数为 SQL_ATTR_AUTOCOMMIT，并将此属性设置已提交的事务。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
