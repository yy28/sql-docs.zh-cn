---
title: "语句转换 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45ee32a803f8c337b5d937699d2000abd718502f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="statement-transitions"></a>语句转换
ODBC 语句具有以下状态。  
  
|State|Description|  
|-----------|-----------------|  
|S0|未分配的语句。 （必须是连接状态，C4，C5 或 C6。 有关详细信息，请参阅[连接转换](../../../odbc/reference/appendixes/connection-transitions.md)。)|  
|S1|已分配的语句。|  
|S2|已准备的语句。 将不创建任何结果集。|  
|S3|已准备的语句。 将创建一个 （可能为空） 的结果集。|  
|S4|创建的语句执行和任何结果集。|  
|S5|创建的语句执行和 （可能为空） 的结果集。 游标已打开并且定位结果集的第一行之前。|  
|S6|将光标放与**SQLFetch**或**SQLFetchScroll**。|  
|S7|将光标放与**SQLExtendedFetch**。|  
|S8|函数需要数据。 **SQLParamData**尚未调用。|  
|S9|函数需要数据。 **SQLPutData**尚未调用。|  
|S10|函数需要数据。 **SQLPutData**已调用。|  
|S11|仍在执行。 语句是后以异步方式执行的函数将返回 SQL_STILL_EXECUTING 处于此状态。 语句将暂时处于此状态时执行的语句句柄可以接受任何函数。 处于 S11 除外的状态表的任何状态表中不会显示的状态的临时居住**SQLCancel**。 该函数时语句暂时处于状态 S11，可以取消通过调用**SQLCancel**从另一个线程。|  
|S12|已取消的异步执行。 在 S12，应用程序必须调用已取消的函数，直到它返回 SQL_STILL_EXECUTING 以外的值。 仅当该函数将返回 SQL_ERROR 和 SQLSTATE HY008，该函数已成功取消 （已取消的操作）。 如果它返回任何其他值，如 SQL_SUCCESS，取消操作失败，并通常执行的函数。|  
  
 状态 S2 和 S3 称为已准备状态，状态通过 S7 S5 时，光标状态，这些状态通过 S10 S8 作为需要数据状态，以及状态 S11 和 S12 作为异步状态。 在每个这些组，转换将单独显示仅时它们仍然是不同的组中; 每种状态在大多数情况下，每个转换状态在每个组都是相同。  
  
 下表显示每个 ODBC 函数如何影响语句的状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 调用**SQLAllocHandle**与*OutputHandlePtr*指向有效的句柄将覆盖该句柄而不考虑与以前的内容处理，并可能会导致 ODBC 驱动程序的问题。 它是不正确的 ODBC 应用程序编程调用**SQLAllocHandle**两次是使用相同的应用程序变量为定义 *\*OutputHandlePtr*而不调用**SQLFreeHandle**重新分配它之前释放句柄。 覆盖 ODBC 以此方式的句柄可能会导致不一致的行为或部分 ODBC 驱动程序的错误。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect、 SQLConnect 和 SQLDriverConnect  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|请参阅下一个表|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-[s] S8 [d] S11 [x]|-[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [nr] 和 [2] S3 [r] 和 [2] S5 [3] 和 [5] S6 ([3] 或 [4]) 和 [6] S7 [4] 和 [7]|请参阅下一个表|  
  
 [1] **SQLExecDirect**返回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回 SQL_NEED_DATA。  
  
 [3] **SQLBulkOperations**返回 SQL_NEED_DATA。  
  
 [4] **SQLSetPos**返回 SQL_NEED_DATA。  
  
 [5] **SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**不调用一样。  
  
 [6] **SQLFetch**或**SQLFetchScroll**已调用一样。  
  
 [7] **SQLExtendedFetch**已调用一样。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel （异步状态）  
  
|S11<br /><br /> 仍在执行|S12<br /><br /> 异步取消|  
|-----------------------------|-----------------------------|  
|NS [1] S12 [2]|S12|  
  
 [1] 语句处于临时状态 S11 函数执行期间。 **SQLCancel**从另一个线程调用。  
  
 [2] 上，语句处于状态 S11，因为异步调用一个函数返回 SQL_STILL_EXECUTING。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|请参阅下一个表|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute （已准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-[s] S11 x|  
  
 [1] *FieldIdentifier*已 SQL_DESC_COUNT。  
  
 [2] *FieldIdentifier*未 SQL_DESC_COUNT。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 SQLStatistics、 SQLTablePrivileges，和 SQLTables  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] 和 [1] S5 [s] 和 [1] S11 [x] 和 [1] 24000 [2]|请参阅下一个表|HY010|NS [c] HY010 o|  
  
 [1] 当前结果的上一次或仅结果，或没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 当前结果并不是最后一个结果。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 SQLStatistics、 SQLTablePrivileges，和 SQLTables （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [如果，会返回由驱动程序管理器 1] 此错误**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和在驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
|IH [2]|HY010|请参阅下一个表|24000|-[s] S11 x|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
  
 [1] 该行显示转换时*SourceDescHandle*参数为 ARD、 APD 或 IPD。  
  
 [2] 该行显示转换时*SourceDescHandle*自变量为 IRD。  
  
 [3] *SourceDescHandle*和*TargetDescHandle*自变量是中的相同**SQLCopyDesc**以异步方式运行的函数。  
  
 [4] 或者*SourceDescHandle*自变量或*TargetDescHandle*自变量 （或两者） 已与中不同**SQLCopyDesc**正在运行的函数以异步方式。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc （已准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|24000[1]|-[s] S11 [x]|  
  
 [1]该行显示转换时*SourceDescHandle*自变量为 IRD。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|请参阅下一个表|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol （已准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|07005|-[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] 调用**SQLDisconnect**释放与连接关联的所有语句。 此外，这将返回的连接状态到 C2;连接状态必须是 C4 语句状态之前 S0。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] 或 [3] S1 [1]|-[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S2 [p] 和 [2]|-[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S3 [p] 和 [2]|(HY010)|(HY010)|  
  
 [1] *CompletionType*自变量是 SQL_COMMIT 和**SQLGetInfo**返回 SQL_CB_DELETE SQL_CURSOR_COMMIT_BEHAVIOR 信息类型，或*CompletionType*自变量是 SQL_ROLLBACK 和**SQLGetInfo**返回 SQL_CB_DELETE SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型。  
  
 [2] *CompletionType*自变量是 SQL_COMMIT 和**SQLGetInfo**返回 SQL_CB_CLOSE SQL_CURSOR_COMMIT_BEHAVIOR 信息类型，或*CompletionType*自变量是 SQL_ROLLBACK 和**SQLGetInfo**返回 SQL_CB_CLOSE SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型。  
  
 [3] *CompletionType*自变量是 SQL_COMMIT 和**SQLGetInfo**返回 SQL_CB_PRESERVE SQL_CURSOR_COMMIT_BEHAVIOR 信息类型，或*CompletionType*自变量是 SQL_ROLLBACK 和**SQLGetInfo**返回 SQL_CB_PRESERVE SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] 和 [nr] S5 [s] 和 [r] [d] S8 S11 [x]|-[e] 和 [1] S1 [e] 和 [2] S4 [s] 和 [nr] S5 [s] 和 [r] [d] S8 S11 [x]|-[e]，[1] 和 [3] S1 [e]、 [2] 和 [3] S4 [s]，[nr] 和 [3] S5 [s]，[r] 和 [3] S8 [d] 和 [3] S11 [x] 和 [3] 24000 [4]|请参阅下一个表|HY010|NS [c] HY010 [o]|  
  
 [由驱动程序管理器返回了 1] 错误。  
  
 [2] 上，不返回了错误的驱动程序管理器。  
  
 [3] 上，当前结果的上一次或仅结果，或没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 当前结果并不是最后一个结果。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [如果，会返回由驱动程序管理器 1] 此错误**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，并且如果由驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|请参阅下一个表|S2 [e] p 和 [1] S4 [s]，[p] [nr] 和 [1] S5 [s]，[p] [r] 和 [1] S8 [d]、 [p] 和 [1] S11 [x]，[p] 和 [1] 24000 [p] 和 [2] HY010 [np]|请参阅光标状态表|HY010|NS [c] HY010 [o]|  
  
 [1] 当前结果的上一次或仅结果，或没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 当前结果并不是最后一个结果。  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute （已准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|S4 [s] [d] S8 S11 [x]|S5 [s] [d] S8 S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]、 [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [如果，会返回由驱动程序管理器 1] 此错误**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，并且如果由驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|请参阅下一个表|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 或 [nf] S11 [x]|S1010|-[s] 或 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 和 SQLFetchScroll  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|请参阅下一个表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 和 SQLFetchScroll （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 或 [nf] S11 [x]|-[s] 或 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] 该行显示转换时*HandleType* SQL_HANDLE_ENV 或 SQL_HANDLE_DBC。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [3] 该行显示转换时*HandleType*已 SQL_HANDLE_DESC 和显式分配的描述符。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] 该行显示转换时*选项*已 SQL_CLOSE。  
  
 [2] 该行显示转换时*选项*SQL_UNBIND 或 SQL_RESET_PARAMS。 如果*选项*自变量为 SQL_DROP 和基础驱动程序是 ODBC 3*.x*驱动程序，驱动程序管理器映射此对的调用**SQLFreeHandle**与*HandleType*设置为 SQL_HANDLE_STMT。 有关详细信息，请参阅有关的转换表[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|请参阅下一个表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] 或 [nf] [x] 24000 [b] HY109 S11 [i]|-[s] 或 [nf] [x] 24000 [b] HY109 S11 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|-[1] 或 [2] HY010 [3]|请参阅下一个表|-[1] 或 [2] 24000 [3]|-[1]，[2] 或 [3] S11 [3] 和 [x]|HY010|NS [c] 或 [4] HY010 [o] 和 [5]|  
  
 [1] *DescriptorHandle*参数为 APD 或 ARD。  
  
 [2] *DescriptorHandle*自变量为 IPD。  
  
 [3] *DescriptorHandle*自变量为 IRD。  
  
 [4] *DescriptorHandle*自变量为相同*DescriptorHandle*中的参数**SQLGetDescField**或**SQLGetDescRec**以异步方式运行的函数。  
  
 [5] *DescriptorHandle*自变量为不同于*DescriptorHandle*中的参数**SQLGetDescField**或**SQLGetDescRec**以异步方式运行的函数。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 和 SQLGetDescRec （已准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|-[1]，[2] 或 [3] S11 [2] 和 [x]|-[1]，[2] 或 [3] S11 [x]|  
  
 [1] *DescriptorHandle*参数为 APD 或 ARD。  
  
 [2] *DescriptorHandle*自变量为 IPD。  
  
 [3] *DescriptorHandle*自变量为 IRD。 请注意这些函数始终返回处于状态 S2 SQL_NO_DATA 时*DescriptorHandle*已 IRD。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 该行显示转换时*HandleType* SQL_HANDLE_ENV、 SQL_HANDLE_DBC，或 SQL_HANDLE_DESC。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_STMT。  
  
 [3] **SQLGetDiagField**始终会返回一个错误，在此状态时*DiagIdentifier*是 SQL_DIAG_ROW_COUNT。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|请参阅下一个表|HY010|HY010|  
  
 [1] 的语句属性未 SQL_ATTR_ROW_NUMBER。  
  
 [2] 上，语句属性是 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|-[1] 或 ([v] 和 [2]) 24000 [b] 和 [2] HY109 [i] 和 [2]|-[i] 或 ([v] 和 [2]) 24000 [b] 和 [2] HY109 [1] 和 [2]|  
  
 [1]*属性*参数不是 SQL_ATTR_ROW_NUMBER。  
  
 [2]*属性*自变量为 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-[s] 和 [2] S1 [nf] [np] 和 [4] S2 [nf] [p] 和 [4] S5 [s] 和 [3] S11 [x]|S1 [nf] [np] 和 [4] S3 [nf] [p] 和 [4] S4 [s] 和 [2] S5 [s] 和 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 函数始终在此状态下返回 SQL_NO_DATA。  
  
 [2] 上下, 一个结果是行计数。  
  
 [3] 的下一个结果是一个结果集。  
  
 [4] 当前结果是最后一个结果。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|请参阅下一个表|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData （需要数据状态）  
  
|S8<br /><br /> 需要数据|S9<br /><br /> 必须放置|S10<br /><br /> 可以将|  
|----------------------|---------------------|---------------------|  
|S1 [e] 和 [1] S2 [e]、 [nr] 和 [2] S3 [e]、 [r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S9 [d] S11 [x]|HY010|S1 [e] 和 [1] S2 [e] [nr] 和 [2] S3 [e]、 [r] 和 [2] S4 [s] [nr] 和 ([1] 或 [2]) S5 [s] [r] 和 ([1] 或 [2]) S5 ([s] 或 [e]) 和 [4] S6 ([s] 或 [e]) 和 [5] S7 ([s] 或 [e]) 和 [3] S9 [d] S11 [x]|  
  
 [1] **SQLExecDirect**返回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回 SQL_NEED_DATA。  
  
 [3] **SQLSetPos**必须已从状态 S7 调用并返回 SQL_NEED_DATA。  
  
 [4] **SQLBulkOperations**必须已从状态 S5 调用并返回 SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulkOperations**必须已从状态 S6 调用并返回 SQL_NEED_DATA。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] 和 [nr] S3 [s] 和 [r] S11 [x]|-[s] 或 ([e] 和 [1]) S1 [e] 和 [2] S11 [x]|S1 [e] 和 [3] S2 [s]，[nr] 和 [3] S3 [s]，[r] 和 [3] S11 [x] 和 [3] 24000 [4]|请参阅下一个表|HY010|NS [c] HY010 [o]|  
  
 [1] 所做的准备失败验证该语句的原因 (SQLSTATE 已 HY009 [无效的参数值] 或 HY090 [无效字符串或缓冲区长度])。  
  
 [2] 所做的准备失败验证该语句时 (SQLSTATE 未 HY009 [无效的参数值] 或 HY090 [无效字符串或缓冲区长度])。  
  
 [3] 上，当前结果的上一次或仅结果，或没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 当前结果并不是最后一个结果。  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|请参阅下一个表|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData （需要数据状态）  
  
|S8<br /><br /> 需要数据|S9<br /><br /> 必须放置|S10<br /><br /> 可以将|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 和 [1] S2 [e]、 [nr] 和 [2] S3 [e]、 [r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S10 [s] S11 [x]|-[s] S1 [e] 和 [1] S2 [e]、 [nr] 和 [2] S3 [e]、 [r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect**返回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回 SQL_NEED_DATA。  
  
 [3] **SQLSetPos**必须已从状态 S7 调用并返回 SQL_NEED_DATA。  
  
 [4] **SQLBulkOperations**必须已从状态 S5 调用并返回 SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulkOperations**必须已从状态 S6 调用并返回 SQL_NEED_DATA。  
  
 [6] 一个或多个调用**SQLPutData**单个参数返回 SQL_SUCCESS，然后调用**SQLPutData**出于具有的相同参数*StrLen_or_Ind*设置到 SQL_NULL_DATA。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] 该行显示转换时*属性*连接属性。 有关转换时*属性*已声明属性，请参阅有关的语句转换表**SQLSetStmtAttr**。  
  
 [2]*属性*参数不是 SQL_ATTR_CURRENT_CATALOG。  
  
 [3]*属性*自变量为 SQL_ATTR_CURRENT_CATALOG。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] 该行显示转换其中*DescriptorHandle*自变量是 ARD、 APD、 IPD，或 (对于**SQLSetDescField**) IRD 时*FieldIdentifier*自变量是 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。 它是错误调用**SQLSetDescField**为 IRD 时*FieldIdentifier*是任何其他值。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|请参阅下一个表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos （光标状态）  
  
|S5<br /><br /> 打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] S8 [d] [x] 24000 [b] HY109 S11 [i]|-[s] S8 [d] [x] 24000 [b] HY109 S11 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 分配|S2 – S3<br /><br /> Prepared|S4<br /><br /> 执行|S5 – S7<br /><br /> 游标|S8 – S10<br /><br /> 需要数据|S11 – S12<br /><br /> 异步|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|-[1] HY011 [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|  
  
 [1]*属性*参数不是 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR、 SQL_ATTR_USE_BOOKMARKS、 SQL_ATTR_CURSOR_SCROLLABLE 或 SQL_ATTR_CURSOR_SENSITIVITY。  
  
 [2]*属性*自变量为 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR、 SQL_ATTR_USE_BOOKMARKS、 SQL_ATTR_CURSOR_SCROLLABLE 或 SQL_ATTR_CURSOR_SENSITIVITY。

