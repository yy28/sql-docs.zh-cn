---
title: 语句转换 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302848"
---
# <a name="statement-transitions"></a>语句转换
ODBC 语句具有以下状态。  
  
|状态|描述|  
|-----------|-----------------|  
|S0|未分配的语句。 （连接状态必须为 C4、C5 或 C6。 有关详细信息，请参阅[连接转换](../../../odbc/reference/appendixes/connection-transitions.md)。|  
|S1|已分配的语句。|  
|S2|准备的声明。 不会创建任何结果集。|  
|S3|准备的声明。 将创建（可能为空）结果集。|  
|S4|已执行语句，未创建结果集。|  
|S5|已执行语句并创建（可能为空）结果集。 光标处于打开位置，位于结果集的第一行之前。|  
|S6|使用**SQLFetch**或**SQLFetchScroll**定位的光标。|  
|S7|使用 SQL**扩展获取**定位的光标。|  
|S8|函数需要数据。 尚未调用**SQLParamData。**|  
|S9|函数需要数据。 尚未调用**SQLPutData。**|  
|S10|函数需要数据。 **SQLPutData**已调用。|  
|S11|仍在执行。 异步执行的函数返回SQL_STILL_EXECUTING后，语句将处于此状态。 语句暂时处于此状态，而接受语句句柄的任何函数正在执行。 状态 S11 中的暂住位置不显示在除**SQLCancel**的状态表以外的任何状态表中。 当语句暂时处于状态 S11 时，可以通过从另一个线程调用**SQLCancel**来取消该函数。|  
|S12|异步执行已取消。 在 S12 中，应用程序必须调用已取消的函数，直到它返回SQL_STILL_EXECUTING以外的值。 仅当函数返回SQL_ERROR和 SQLSTATE HY008（操作已取消）时，该函数才成功取消。 如果它返回任何其他值（如SQL_SUCCESS，则取消操作失败，并且函数正常执行。|  
  
 状态 S2 和 S3 称为准备状态，状态 S5 到 S7 作为游标状态，将 S8 到 S10 作为需求数据状态，并将 S11 和 S12 作为异步状态。 在每个组中，仅当转换在组中的每个状态不同时才会单独显示;在大多数情况下，每个组中的每个状态的转换都相同。  
  
 下表显示了每个 ODBC 函数如何影响语句状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV时的过渡。  
  
 [2] 此行显示*HandleType* SQL_HANDLE_DBC时的过渡。  
  
 [3] 此行显示*HandleType* SQL_HANDLE_STMT时的过渡。  
  
 [4] 此行显示*handleType* SQL_HANDLE_DESC时的过渡。  
  
 [5] 使用*OutputHandlePtr*调用**SQLAllocHandle，** 指向一个有效的句柄，该句柄处理时不考虑该句柄的先前内容，并且可能会给 ODBC 驱动程序带来问题。 使用为*\*OutputHandlePtr*定义的相同应用程序变量调用**SQLAllocHandle**两次，而不调用**SQLFreeHandle**以释放句柄，然后再重新分配该句柄，这是不正确的 ODBC 应用程序编程。 以这种方式覆盖 ODBC 句柄可能会导致 ODBC 驱动程序的行为不一致或错误。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowse 连接、SQL 连接和 SQLDriver 连接  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulk 操作  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|请参阅下表|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulk 操作（游标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2 [nr] 和 [2] S3 [r] 和 [2] S5[3] 和 [5] S6（[3] 或 [4]）和 [6] S7[4] 和 [7]|请参阅下表|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLBulk 操作**返回SQL_NEED_DATA。  
  
 [4] **SQLSetPos**返回SQL_NEED_DATA。  
  
 [5] **SQLFetch、SQLFetchScroll**或 SQL**扩展获取**尚未调用。 **SQLFetchScroll**  
  
 [6] **SQLFetch**或**SQLFetchScroll**已调用。  
  
 [7] **SQL 扩展提取**已调用。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQL取消（异步状态）  
  
|S11<br /><br /> 仍在执行|S12<br /><br /> 异步已取消|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] 语句在执行函数时暂时处于状态 S11。 **SQLCancel**是从不同的线程调用的。  
  
 [2] 语句处于状态 S11，因为称为异步返回的函数SQL_STILL_EXECUTING。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|请参阅下表|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLCol属性（准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- S11 x|  
  
 [1]*字段标识符*SQL_DESC_COUNT。  
  
 [2]*字段标识符*未SQL_DESC_COUNT。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumn 特权、SQLColumn、SQL 外键、SQLGetTypeInfo、SQL 主键、SQL过程列、SQL 过程程序、SQL 特殊列、SQLStatistics、SQLTable 特权和 SQLTables  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] 和 [1] S5 [s] 和 [1] S11 [x] 和 [1] 24000 [2]|请参阅下表|HY010|NS [c] HY010 o|  
  
 [1] 当前结果是最后或唯一的结果，或者没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 当前结果不是最后的结果。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumn 特权、SQLColumn、SQL 外键、SQLGetTypeInfo、SQL 主键、SQL过程列、SQL 过程程序、SQL 特殊列、SQLStatistics、SQLTable 特权和 SQLTables（游标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
|IH[2]|HY010|请参阅下表|24000|-- S11 x|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
  
 [1] 当*SourceDescHandle*参数为 ARD、APD 或 IPD 时，此行显示过渡。  
  
 [2] 当*SourceDescHandle*参数是 IRD 时，此行显示过渡。  
  
 [3] *SourceDescHandle*和*TargetDescHandle*参数与以异步方式运行的**SQLCopyDesc**函数中相同。  
  
 [4] *SourceDescHandle*参数或*TargetDescHandle*参数（或两者）都与以异步方式运行的**SQLCopyDesc**函数不同。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc（准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1]此行显示 *"源DescHandle"* 参数为 IRD 时的过渡。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLData 源和 SQL 驱动程序  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|请参阅下表|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol（准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQL 断开  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|（HY010）|（HY010）|  
  
 {1} 调用**SQLDisconnect**释放与连接关联的所有语句。 此外，这将连接状态返回到 C2;在语句状态为 S0 之前，连接状态必须为 C4。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] 或[3] S1[1]|--[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S2 [p] 和 [2]|--[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S3 [p] 和 [2]|（HY010）|（HY010）|  
  
 {1}*完成类型*参数**SQL_COMMIT，SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR信息类型的SQL_CB_DELETE，或者 *"完成类型"* 参数SQL_ROLLBACK，SQLGetInfo 返回SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型的SQL_CB_DELETE。 **SQLGetInfo**  
  
 [2]*完成类型*参数**SQL_COMMIT，SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR信息类型的SQL_CB_CLOSE，或者 *"完成类型"* 参数SQL_ROLLBACK，SQLGetInfo 返回SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型的SQL_CB_CLOSE。 **SQLGetInfo**  
  
 [3]*完成类型*参数**SQL_COMMIT，SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR信息类型的SQL_CB_PRESERVE，或者 *"完成类型"* 参数SQL_ROLLBACK，SQLGetInfo 返回SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型的SQL_CB_PRESERVE。 **SQLGetInfo**  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|-- [e] 和 [1] S1 [e] 和 [2] S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|-- [e]、[1]和[3]S1 [e]、[2]和[3]S4 [s]、[nr]和[3] S5 [s]、[r]和[3]S8 [d] 和 [3] S11 [x] 和 [3] 24000 [4]|请参阅下表|HY010|NS [c] HY010 [o]|  
  
 [1] 驱动程序管理器返回错误。  
  
 [2] 驱动程序管理器未返回错误。  
  
 [3] 当前结果是最后一个或唯一的结果，或者没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 当前结果不是最后的结果。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**返回SQL_NO_DATA，则驱动程序将返回此错误。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|（HY010）|请参阅下表|S2 [e]、p 和 [1] S4 [s]、[p]、[nr] 和 [1] S5 [s]、[p]、[r] 和 [1] S8 [d]、[p] 和 [1] S11 [x]、[p] 和 [1] 24000 [p] 和 [2] HY010 [np]|请参阅游标状态表|HY010|NS [c] HY010 [o]|  
  
 [1] 当前结果是最后或唯一的结果，或者没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 当前结果不是最后的结果。  
  
## <a name="sqlexecute-prepared-states"></a>SQL 执行（就绪状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQL 执行（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]， [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**返回SQL_NO_DATA，则驱动程序将返回此错误。  
  
## <a name="sqlextendedfetch"></a>SQL 扩展获取  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010|S1010|24000|请参阅下表|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQL 扩展获取（游标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 或 [nf] S11 [x]|S1010|-- [s] 或 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 和 SQLFetchScroll  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|请参阅下表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQL提取和 SQLFetchScroll（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 或 [nf] S11 [x]|-- [s] 或 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV或SQL_HANDLE_DBC时的过渡。  
  
 [2] 此行显示*handleType* SQL_HANDLE_STMT时的过渡。  
  
 [3] 此行显示*HandleType* SQL_HANDLE_DESC并显式分配描述符时的过渡。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] 此行显示*选项*SQL_CLOSE时的过渡。  
  
 [2] 此行显示*选项*SQL_UNBIND或SQL_RESET_PARAMS时的过渡。 如果*Option*参数SQL_DROP并且基础驱动程序是 ODBC 3 *.x*驱动程序，则驱动程序管理器将此参数映射到**SQLFreeHandle**的调用，*其中句柄类型*设置为SQL_HANDLE_STMT。 有关详细信息，请参阅[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)的过渡表。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|请参阅下表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGet数据（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] 或 [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] 或 [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] 或 [2] HY010 [3]|请参阅下表|-- [1] 或 [2] 24000 [3]|-- [1]、[2]或[3] S11 [3] 和 [x]|HY010|NS [c] 或 [4] HY010 [o] 和 [5]|  
  
 [1]*描述符句柄*参数是 APD 或 ARD。  
  
 [2]*描述符句柄*参数是 IPD。  
  
 [3]*描述符处理*参数是 IRD。  
  
 [4]*描述符处理*参数与**SQLGetDescfield**或**SQLGetDescrec**函数中以异步方式运行的描述*符处理*参数相同。  
  
 [5]*描述符处理*参数不同于**SQLGetDescfield**或**SQLGetDescrec**函数中异步运行的描述*符处理*参数。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 和 SQLGetDescRec（准备状态）  
  
|S2<br /><br /> 无结果|S3<br /><br /> 结果|  
|-----------------------|--------------------|  
|--[1]、[2]或[3]S11[2]和[x]|--[1]、[2]或[3] S11 [x]|  
  
 [1]*描述符句柄*参数是 APD 或 ARD。  
  
 [2]*描述符句柄*参数是 IPD。  
  
 [3]*描述符处理*参数是 IRD。 请注意，当*描述符句柄*是 IRD 时，这些函数始终在状态 S2 中返回SQL_NO_DATA。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV、SQL_HANDLE_DBC 或SQL_HANDLE_DESC时的过渡。  
  
 [2] 此行显示*handleType* SQL_HANDLE_STMT时的过渡。  
  
 [3] 当*Diag标识符*SQL_DIAG_ROW_COUNT时 **，SQLGetDiagField**总是返回此状态下的错误。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|请参阅下表|HY010|HY010|  
  
 [1] 语句属性未SQL_ATTR_ROW_NUMBER。  
  
 [2] 语句属性SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] 或 （[v] 和 [2] 24000 [b] 和 [2] HY109 [i] 和 [2]|-- [i] 或 （[v] 和 [2] 2] 24000 [b] 和 [2] HY109 [1] 和 [2]|  
  
 [1]*属性*参数未SQL_ATTR_ROW_NUMBER。  
  
 [2]*属性*参数SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|--[1]|--[1]|-- [s] 和 [2] S1 [nf]、[np]和 [4] S2 [nf]、[p]和 [4] S5 [s] 和 [3] S11 [x]|S1 [nf]、[np]和 [4] S3 [nf]、[p] 和 [4] S4 [s] 和 [2] S5 [s] 和 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 函数始终返回SQL_NO_DATA处于此状态。  
  
 [2] 下一个结果是行计数。  
  
 [3] 下一个结果是结果集。  
  
 [4] 当前结果是最后的结果。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|请参阅下表|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData（需要数据状态）  
  
|S8<br /><br /> 需要数据|S9<br /><br /> 必须把|S10<br /><br /> 可以放|  
|----------------------|---------------------|---------------------|  
|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S9 [d] S11 [x]|HY010|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]， [r]和[2] S4 [s]、[nr]和（[1]或[2]）S5 [s]、[r]和（[1]或[2]）S5（[s] 或[e]）和[4]S6（[s]或[e]）和[5]S7（[s]或[e]）和[3]S9[s]|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLSetPos**是从状态 S7 调用并返回SQL_NEED_DATA。  
  
 [4] **SQLBulk操作**从状态 S5 调用并返回SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulk 操作**从状态 S6 调用并返回SQL_NEED_DATA。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|S2 [s] 和 [nr] S3 [s] 和 [r] S11 [x]|-- [s] 或 （[e] 和 [1]） S1 [e] 和 [2] S11 [x]|S1 [e] 和 [3] S2 [s]、[nr] 和 [3] S3 [s] 、[r] 和 [3] S11 [x] 和 [3] 24000 [4]|请参阅下表|HY010|NS [c] HY010 [o]|  
  
 [1] 准备失败的原因除验证语句（SQLSTATE 是 HY009 [无效参数值] 或 HY090 [无效字符串或缓冲区长度]）。  
  
 [2] 验证语句时准备失败（SQLSTATE 不是 HY009 [无效参数值]或 HY090 [无效字符串或缓冲区长度]）。  
  
 [3] 当前结果是最后一个或唯一的结果，或者没有当前结果。 有关多个结果的详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 当前结果不是最后的结果。  
  
## <a name="sqlprepare-cursor-states"></a>SQL准备（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|请参阅下表|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData（需要数据状态）  
  
|S8<br /><br /> 需要数据|S9<br /><br /> 必须把|S10<br /><br /> 可以放|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S10 [s] S11 [x]|-- [s] S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLSetPos**是从状态 S7 调用并返回SQL_NEED_DATA。  
  
 [4] **SQLBulk操作**从状态 S5 调用并返回SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulk 操作**从状态 S6 调用并返回SQL_NEED_DATA。  
  
 [6] 对**SQLPutData**的单个参数返回的一个或多个调用SQL_SUCCESS，**然后对同**一参数进行了调用 *，StrLen_or_Ind*设置为SQL_NULL_DATA。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|（IH）|（HY010）|（HY010）|--|--|（HY010）|（HY010）|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] 此行显示*属性*为连接属性时的过渡。 有关*属性*为语句属性时的过渡，请参阅**SQLSetStmtAttr 的**语句转换表。  
  
 [2]*属性*参数未SQL_ATTR_CURRENT_CATALOG。  
  
 [3]*属性*参数SQL_ATTR_CURRENT_CATALOG。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursor 名称  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] 当*字段标识符*参数SQL_DESC_ARRAY_STATUS_PTR或SQL_DESC_ROWS_PROCESSED_PTR时，此行显示*描述符处理*参数为 ARD、APD、IPD 或 （对于**SQLSetDescField）** IRD 的过渡。 当*字段标识符*是任何其他值时，为 IRD 调用**SQLSetDescField**是错误的。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|请参阅下表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos（光标状态）  
  
|S5<br /><br /> 已打开|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 扩展获取|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未分配|S1<br /><br /> 已分配|S2-S3<br /><br /> Prepared|S4<br /><br /> 执行|S5-S7<br /><br /> 游标|S8-S10<br /><br /> 需要数据|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|  
  
 [1]*属性*参数不SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE或SQL_ATTR_CURSOR_SENSITIVITY。  
  
 [2]*属性*参数是SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE或SQL_ATTR_CURSOR_SENSITIVITY。
