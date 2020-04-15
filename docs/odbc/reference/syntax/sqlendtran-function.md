---
title: SQLEndTran 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302738"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLEndTran**请求对与连接关联的所有语句的所有活动操作执行或回滚操作。 **SQLEndTran**还可以请求对与环境关联的所有连接执行提交或回滚操作。  
  
> [!NOTE]  
>  有关驱动程序管理器将此功能映射到 ODBC 3 时的详细信息。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射应用程序向后兼容性的替代函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]句柄类型标识符。 包含SQL_HANDLE_ENV（如果*句柄*是环境句柄）或SQL_HANDLE_DBC（如果*句柄*是连接句柄）。  
  
 *Handle*  
 [输入]句柄，由*HandleType*指示的类型，指示事务的范围。 有关详细信息，请参阅"注释"。  
  
 *完成类型*  
 [输入]以下两个值之一：  
  
 SQL_COMMITSQL_ROLLBACK  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLEndTran**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过使用相应的*句柄类型*和*句柄*调用**SQLGetDiagRec**来获取关联的 SQLSTATE 值。 下表列出了**SQLEndTran**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|（DM）*句柄类型*SQL_HANDLE_DBC，*并且句柄*未处于连接状态。|  
|08007|事务期间连接失败|*HandleType* SQL_HANDLE_DBC，在执行函数期间与*句柄*关联的连接失败，无法确定请求**的 COMMIT**或**ROLLBACK**是否发生在故障之前。|  
|25S01|事务状态未知|*Handle*中的一个或多个连接未能完成指定结果的事务，结果未知。|  
|25S02|事务仍然处于活动状态|驱动程序无法保证全局事务中的所有工作都可以以原子方式完成，并且事务仍然处于活动状态。|  
|25S03|事务回滚|驱动程序无法保证全局事务中的所有工作都可以以原子方式完成，并且*在 Handle*中处于活动状态的事务中的所有工作都回滚。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40002|完整性约束冲突|*完成类型*SQL_COMMIT，更改的承诺导致诚信约束违规。 因此，事务被回滚。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*szMessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|为*连接句柄*启用了异步处理。 调用该函数，并在它完成[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)执行之前在*ConnectHandle*上调用 。 然后在*连接处理*上再次调用该函数。<br /><br /> 调用该函数，并在它执行完**SQLCancelHandle**之前从多线程应用程序中的不同线程调用*了 ConnectHandle。*|  
|HY010|函数序列错误|（DM） 调用了与*ConnectHandle*关联的语句句柄的异步执行函数，并且在调用**SQLEndTran**时仍在执行。<br /><br /> （DM） 为*ConnectHandle*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用一个语句句柄，该句柄与**SQLExecute***连接句柄*相关联并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 为*HandleType*设置为SQL_HANDLE_DBC的*句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用为与*句柄*关联的语句句柄之一，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY012|无效的事务操作代码|（DM） 为参数 *"完成类型"* 指定的值既不是SQL_COMMIT，也不是SQL_ROLLBACK。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY092|无效属性/选项标识符|（DM） 为参数*HandleType*指定的值既不是SQL_HANDLE_ENV，也不是SQL_HANDLE_DBC。|  
|HY115|对于包含启用异步函数执行的连接的环境，不允许 SQLEndTran|（DM） 如果为环境中的连接启用了连接函数的异步执行，则无法将*句柄类型*设置为SQL_HANDLE_ENV。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅本主题的"注释"部分。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持**ROLLBACK**操作。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*连接句柄*关联的驱动程序不支持该功能。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 对于 ODBC 3。*x*驱动程序，如果*HandleType*是SQL_HANDLE_ENV，*并且句柄*是有效的环境句柄，则驱动程序管理器将在与环境关联的每个驱动程序中调用**SQLEndTran。** 对驱动程序的调用的*Handle*参数将是驱动程序的环境句柄。 对于 ODBC 2。*x*驱动程序，如果*HandleType*是SQL_HANDLE_ENV，*并且 Handle*是一个有效的环境句柄，并且该环境中有多个连接处于连接状态，则驱动程序管理器将在驱动程序中为该环境中处于连接状态的每个连接调用**SQLTransact**一次。 每个调用中的*Handle*参数将是连接的句柄。 在这两种情况下，驱动程序将尝试提交或回滚事务，具体取决于 *"完成类型"* 的值，该环境中处于连接状态的所有连接。 非活动连接不会影响事务。  
  
> [!NOTE]  
>  **SQLEndTran**不能用于在共享环境中提交或回滚事务。 如果**SQLEndTran 调用 SQLEndTran，** 将返回 SQLSTATE HY092（无效属性/选项标识符），将返回到*将句柄*设置为共享环境的句柄或共享环境中的连接句柄。  
  
 仅当驱动程序管理器收到每个连接的SQL_SUCCESS时，才会返回SQL_SUCCESS。 如果驱动程序管理器在一个或多个连接上接收SQL_ERROR，它将返回SQL_ERROR到应用程序，并将诊断信息放置在环境的诊断数据结构中。 要确定在提交或回滚操作期间失败的连接或连接，应用程序可以为每个连接调用**SQLGetDiagRec。**  
  
> [!NOTE]  
>  驱动程序管理器不模拟跨所有连接的全局事务，因此不使用两阶段提交协议。  
  
 如果 *"完成类型*"SQL_COMMIT，SQLEndTran 会针对与受影响的连接关联的任何语句发出所有活动操作的提交请求。 **SQLEndTran** 如果*完成类型***SQL_ROLLBACK，SQLEndTran**会针对与受影响的连接关联的任何语句的所有活动操作发出回滚请求。 如果没有事务处于活动状态 **，SQLEndTran**将返回SQL_SUCCESS，对任何数据源没有影响。 有关详细信息，请参阅[提交和回滚事务](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驱动程序处于手动提交模式（通过调用**SQLSetConnectAttr，** 将SQL_ATTR_AUTOCOMMIT属性设置为SQL_AUTOCOMMIT_OFF），则当对当前数据源执行可包含在事务中的 SQL 语句时，将隐式启动新事务。 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 要确定事务操作如何影响游标，应用程序使用SQL_CURSOR_ROLLBACK_BEHAVIOR和SQL_CURSOR_COMMIT_BEHAVIOR选项调用**SQLGetInfo。** 有关详细信息，请参阅以下段落，并查看[事务对游标和准备语句的影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等于**SQL_CB_DELETE，SQLEndTran**将关闭并删除与连接关联的所有语句上的所有打开的游标，并丢弃所有挂起的结果。 **SQLEndTran**将任何语句保留在已分配（未准备）状态中;应用程序可以将它们重用为后续 SQL 请求，也可以调用**SQLFreeStmt**或**SQLFreeHandle，** 并带有*SQL_HANDLE_STMT的句柄类型*来解调它们。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等于**SQL_CB_CLOSE，SQLEndTran**将关闭与连接关联的所有语句上的所有打开游标。 **SQLEndTran**将任何语句保留在准备状态中;应用程序可以调用**SQLExecute**以执行与连接关联的语句，而无需首先调用**SQLPrepare**。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等于SQL_CB_PRESERVE，则**SQLEndTran**不会影响与连接关联的打开游标。 光标停留在调用**SQLEndTran**之前指向的行中。  
  
 对于支持事务的驱动程序和数据源，在没有任何事务处于活动状态时使用SQL_COMMIT或SQL_ROLLBACK调用**SQLEndTran**返回SQL_SUCCESS（指示没有要提交或回滚的工作），并且对数据源没有影响。  
  
 当驱动程序处于自动提交模式时，驱动程序管理器不会在驱动程序中调用**SQLEndTran。** **SQLEndTran**始终返回SQL_SUCCESS，无论它是使用 SQL_COMMIT 的*完成类型*还是SQL_ROLLBACK调用。  
  
 不支持事务的驱动程序或数据源 **（SQLGetInfo** *选项*SQL_TXN_CAPABLESQL_TC_NONE）实际上始终处于自动提交模式，因此无论是否使用完成*类型*SQL_COMMIT或SQL_ROLLBACK调用它们，始终返回**SQLEndTran** SQL_SUCCESS。 此类驱动程序和数据源实际上不会在请求时回滚事务。  
  
## <a name="suspended-state"></a>挂起状态  
 在 Windows 7 之前发布的驱动程序管理器中，如果**SQLEndTran**从驱动程序返回SQL_ERROR，则事务处于活动状态。 但是，事务可能在服务器上成功提交，但客户端上的驱动程序尚未收到通知（例如，因为发生了网络错误）。 这将使连接处于不良状态。 从 Windows 7 开始，当**SQLEndTran**返回SQL_ERROR时，连接可能处于挂起状态。 在挂起状态下，可以调用只读函数。 最终，应用程序应在挂起的连接上调用**SQLDisconnect**以释放资源。  
  
 如果以下所有条件都为 true，则连接将置于挂起状态：  
  
-   驱动程序从**SQLEndTran**返回SQL_ERROR。  
  
-   驱动程序为 ODBC 版本 3.8 或更高版本。  
  
-   应用程序版本为 3.8 或更高版本;或重新编译的 ODBC 2.x 或 3.x 应用程序通过**SQLCancelHandle**成功取消**SQLEndTran**函数。  
  
-   驱动程序未返回以下消息之一，这些消息确认事务未完成：  
  
    -   25S03： 事务回滚  
  
    -   40001： 序列化失败  
  
    -   40002： 完整性约束  
  
    -   HYC00：未实现可选功能  
  
 如果在环境句柄上调用**SQLEndTran，** 并且其连接之一满足上述条件，则连接到同一驱动程序的所有连接都将置于挂起状态。  
  
 应用程序在挂起的连接上调用**SQLDisconnect**后，该连接可用于重新连接到其他数据源或同一数据源。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|取消在连接句柄上异步运行的函数。|[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|释放手柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|释放语句句柄|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
