---
title: "连接转换 |Microsoft 文档"
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
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8af5cd175cdd9ab7d96cdb141bcd0a6b6100ea80
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connection-transitions"></a>连接转换
ODBC 连接具有以下状态。  
  
|State|Description|  
|-----------|-----------------|  
|C0|未分配的环境，未分配的连接|  
|C1|已分配的环境，未分配的连接|  
|C2|分配分配连接的环境|  
|C3|连接函数需要数据|  
|C4|连接的连接|  
|C5|连接连接，分配语句|  
|C6|连接的连接，正在进行的事务。 它有可能处于不包含任何语句分配连接上的状态 C6 的连接。 例如，假设连接在手动提交模式下并处于状态 C4。 如果语句是分配、 执行 （从开始事务），然后释放，事务将保持活动状态，但不有连接上的任何语句。|  
  
 下表显示每个 ODBC 函数如何影响连接状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 没有 Env。|未分配的 C1|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 调用**SQLAllocHandle**与*OutputHandlePtr*指向有效的句柄将覆盖该句柄而不考虑以前的内容 ofthat 句柄，并可能会导致 ODBC 驱动程序的问题。 它是不正确的 ODBC 应用程序编程调用**SQLAllocHandle**两次是使用相同的应用程序变量为定义 *\*OutputHandlePtr*而不调用**SQLFreeHandle**重新分配它之前释放句柄。 覆盖 ODBC 以此方式的句柄可能导致不一致的行为或部分 ODBC 驱动程序的错误。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-[d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|-[1] C5 [2]|  
  
 [1] 上，连接时手动提交模式。  
  
 [2] 上，连接时自动提交模式。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 SQLStatistics、 SQLTablePrivileges，和 SQLTables  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6 [2]|--|  
  
 [1] 的连接已在自动提交模式下，或数据源未开始事务。  
  
 [2] 上，连接处于手动提交模式下，而数据源开始事务。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、 SQLGetDescField、 SQLGetDescRec、 SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] 在此状态下，应用程序的唯一描述符显式分配描述符。  
  
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
|(IH)|(IH)|C4 s-n [f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|-[4] 或 ([5]、 [6] 和 [8]) C4 [5] 和 [7] C5 [5]、 [6] 和 [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 由于连接不是已连接状态，它不会影响事务。  
  
 [4] 上，提交或回滚在连接上失败。 在这种情况下，该函数返回 SQL_ERROR。  
  
 [5] 上，提交或回滚成功连接上。 如果在另一个连接上失败，提交或回滚或函数返回 SQL_SUCCESS 如果提交或回滚对所有连接成功，则该函数返回 SQL_ERROR。  
  
 [6] 没有分配连接上的至少一个语句。  
  
 [7] 分配连接上没有语句。  
  
 [8] 连接至少有一个语句为其存在已打开的游标，和数据源时提交或回滚事务，则保留游标、 适用的为准 (具体取决于是否*CompletionType*已 SQL_提交或 SQL_ROLLBACK）。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 属性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 [9] 如果连接了没有打开的游标任何语句，如果事务已提交或回滚未保留游标。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6 [2] C6 [3]|--|  
  
 [1] 的连接已在自动提交模式下，而执行的语句没有*光标**规范*（例如 SELECT 语句）; 或者连接已被手动提交模式下和语句执行未开始事务。  
  
 [2] 上，连接处于自动提交模式下，而执行的语句已*光标**规范*（例如 SELECT 语句）。  
  
 [在手动提交模式下，已 3] 上，连接和数据源开始事务。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4 [5]-[6]|-C4 [7] [5] 和 [8] C5 [6] 和 [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 没有分配连接上只有一条语句。  
  
 [6] 没有分配连接上的多个语句。  
  
 [7] 上，连接时手动提交模式。  
  
 [在自动提交模式下已 8] 连接。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5 [3]-[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] 该行显示事务时*选项*自变量是 SQL_CLOSE。  
  
 [2] 该行显示事务时*选项*SQL_UNBIND 或 SQL_RESET_PARAMS，则参数。  
  
 [3] 的连接已在自动提交模式下，没有游标都被，打开除此任何语句。  
  
 [4] 的连接已在手动提交模式下，或它已处于自动提交模式和至少一个其他语句上打开游标的。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1]*属性*自变量为 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或连接属性已设置一个值。  
  
 [2]*属性*自变量不 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，而且必须不为连接设置一个值属性。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
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
  
 [1]*信息类型*自变量为 SQL_ODBC_VER。  
  
 [2]*信息类型*参数不是 SQL_ODBC_VER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6 [2]|-[3] C5 [1]|  
  
 [1] 的连接已处于自动提交模式，并且调用**SQLMoreResults**未初始化的游标说明结果集的处理。  
  
 [2] 的连接已处于自动提交模式，并且调用**SQLMoreResults**已初始化的游标说明结果集的处理。  
  
 [3] 上，连接时手动提交模式。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6 [2]|--|  
  
 [1] 的连接已在自动提交模式下，或数据源未开始事务。  
  
 [2] 上，连接处于手动 – 提交模式下，而数据源开始事务。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|-08002 [3] [4] HY011 [5]|-08002 [3] [4] HY011 [5]|-[3] 和 [6] C5 [8] [4] HY011 08002 [5] 或 [7]|  
  
 [1]*属性*参数不为 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [2]*属性*参数为 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3]*属性*参数不为 SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE。  
  
 [4]*属性*自变量为 SQL_ATTR_ODBC_CURSORS。  
  
 [5]*属性*自变量为 SQL_ATTR_PACKET_SIZE。  
  
 [6]*属性*参数不是 SQL_ATTR_AUTOCOMMIT，或*属性*自变量为 SQL_ATTR_AUTOCOMMIT 和设置此属性未提交该事务。  
  
 [7]*属性*自变量为 SQL_ATTR_TXN_ISOLATION。  
  
 [8]*属性*自变量为 SQL_ATTR_AUTOCOMMIT，并将此属性设置提交事务。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|C0<br /><br /> 没有 Env。|C1<br /><br /> 未分配|C2<br /><br /> 分配|C3<br /><br /> 需要数据|C4<br /><br /> 已连接|C5<br /><br /> 。|C6<br /><br /> 事务|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|

