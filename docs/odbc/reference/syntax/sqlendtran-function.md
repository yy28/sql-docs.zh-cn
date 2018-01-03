---
title: "SQLEndTran 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLEndTran
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLEndTran
helpviewer_keywords: SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
caps.latest.revision: "29"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15ba9ff7d28101201842071929b34dfa7ec1d455
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlendtran-function"></a>SQLEndTran 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLEndTran**请求与连接相关联的所有语句上的所有活动操作的提交或回滚操作。 **SQLEndTran**还可以请求提交或回滚操作将执行的与环境相关的所有连接。  
  
> [!NOTE]  
>  有关详细信息有关哪些驱动程序管理器时，将映射此函数可对 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射用于向后兼容性的应用程序的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]句柄类型标识符。 包含任一 SQL_HANDLE_ENV (如果*处理*环境句柄) 或 SQL_HANDLE_DBC (如果*处理*是连接句柄)。  
  
 *Handle*  
 [输入]该句柄，指出的类型的*HandleType*，，该值指示在事务范围。 有关详细信息，请参阅"注释"。  
  
 *CompletionType*  
 [输入]以下两个值之一：  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLEndTran**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**使用相应*HandleType*和*处理*。 下表列出了通常返回的 SQLSTATE 值**SQLEndTran**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) *HandleType*已 SQL_HANDLE_DBC，和*处理*当时不处于已连接状态。|  
|08007|事务期间连接出错|*HandleType*已 SQL_HANDLE_DBC，以及与连接关联*处理*函数，在执行期间失败且不能确定是否请求**提交**或**回滚**故障之前出现。|  
|25S01|事务状态未知|一个或多个中的连接*处理*失败，结果指定，完成事务，并且结果为未知。|  
|25S02|事务仍处于活动状态|该驱动程序无法保证在全局事务中的所有工作都无法以原子方式，都完成并事务仍处于活动状态。|  
|25S03|事务回滚|该驱动程序无法保证无法以原子方式，完成全局事务中的所有工作，都适用于中的活动事务*处理*已回滚。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40002|完整性约束冲突|*CompletionType* SQL_COMMIT，并引起完整性约束冲突的更改的承诺。 因此，事务已回滚。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*szMessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*ConnectionHandle*。 已调用函数，和之前完成执行[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*。 然后在再次调用该函数*ConnectionHandle*。<br /><br /> 已调用函数，和之前完成执行**SQLCancelHandle**上调用了*ConnectionHandle*从多线程应用程序中的不同线程。|  
|HY010|函数序列错误|(DM) 为与关联的语句句柄调用以异步方式执行的函数*ConnectionHandle*和仍在执行时**SQLEndTran**调用。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*ConnectionHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**调用了与语句句柄关联*ConnectionHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*处理*与*HandleType*设置为 SQL_HANDLE_DBC 和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**与关联的语句句柄之一调用*处理*和返回的 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY012|事务操作代码无效|(DM) 值的参数的指定*CompletionType* SQL_COMMIT 和 SQL_ROLLBACK 都不是。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY092|属性/选项标识符无效|(DM) 值的参数的指定*HandleType* SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 都不是。|  
|HY115|包含与异步函数执行启用连接的环境不允许 SQLEndTran|(DM) *HandleType*不能设置为 SQL_HANDLE_ENV，如果在环境中的连接为启用了连接函数的异步执行。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅本主题的注释部分。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持**回滚**操作。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*ConnectionHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 适用于 ODBC 3。*x*驱动程序，如果*HandleType*是 SQL_HANDLE_ENV 和*处理*是有效的环境句柄，则驱动程序管理器将调用**SQLEndTran**中与该环境关联的每个驱动程序。 *处理*驱动程序调用的参数将为驱动程序的环境句柄。 适用于 ODBC 2。*x*驱动程序，如果*HandleType*是 SQL_HANDLE_ENV 和*处理*是有效的环境句柄，并且有多个连接中在该环境中，已连接状态然后驱动程序管理器将调用**SQLTransact**一次在该环境中已连接状态的每个连接的驱动程序中。 *处理*在每次调用的参数将为连接的句柄。 在任一情况下，该驱动程序将尝试提交或回滚事务，具体取决于值*CompletionType*，对在已连接状态对该环境中的所有连接。 未处于活动状态的连接不会影响事务。  
  
> [!NOTE]  
>  **SQLEndTran**不用于提交或回滚在共享环境事务。 SQLSTATE HY092 将返回 （无效的属性/选项标识符），如果**SQLEndTran**使用调用*处理*设置为共享环境的任一句柄或上共享的连接的句柄环境。  
  
 仅当它为每个连接接收 SQL_SUCCESS，驱动程序管理器将返回 SQL_SUCCESS。 如果驱动程序管理器在一个或多个连接上接收 SQL_ERROR，它将返回 SQL_ERROR 应用程序，并将诊断信息置于环境的诊断数据结构。 若要确定哪个连接失败提交或回滚操作期间，应用程序可以调用**SQLGetDiagRec**为每个连接。  
  
> [!NOTE]  
>  驱动程序管理器不模拟全局事务跨所有连接，因此不会使用两阶段提交协议。  
  
 如果*CompletionType*是 SQL_COMMIT， **SQLEndTran**发出的任何与受影响的连接关联的语句上的所有活动操作的提交请求。 如果*CompletionType*是 SQL_ROLLBACK， **SQLEndTran**发出的任何与受影响的连接关联的语句上的所有活动操作的回滚请求。 如果没有事务处于活动状态， **SQLEndTran** SQL_SUCCESS 返回对任何数据源没有影响。 有关详细信息，请参阅[Committing 和滚动交易记录](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果该驱动程序处于手动提交模式 (通过调用**SQLSetConnectAttr**与 SQL_ATTR_AUTOCOMMIT 属性设置为 SQL_AUTOCOMMIT_OFF)，可以包含在 SQL 语句时，隐式启动新事务事务是针对当前的数据源执行的。 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 若要确定事务操作如何影响游标，应用程序调用**SQLGetInfo**使用 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 选项。 有关详细信息，请参阅以下各段并还会看到[游标和准备的语句上的事务影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_DELETE， **SQLEndTran**关闭和删除与连接关联的所有语句上的所有打开的游标并放弃所有挂起结果。 **SQLEndTran**离开已分配的 （未准备好） 状态; 中存在任何语句应用程序可以重复使用它们的后续 SQL 请求中，也可以调用**SQLFreeStmt**或**SQLFreeHandle**与*HandleType* SQL_HANDLE_STMT 解除分配。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_CLOSE， **SQLEndTran**关闭所有打开的游标上与连接关联的所有语句。 **SQLEndTran**离开准备好的状态; 中存在任何语句应用程序可以调用**SQLExecute**为与连接，而第一个调用无关联的语句**SQLPrepare**.  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_PRESERVE， **SQLEndTran**不会影响与连接关联的打开的游标。 游标会保留在它们之前调用了指向行**SQLEndTran**。  
  
 支持事务，调用的驱动程序和数据源**SQLEndTran**与 SQL_COMMIT 或 SQL_ROLLBACK 没有事务处于活动状态时返回 SQL_SUCCESS （指示没有要提交或回滚工作）和数据源没有影响。  
  
 在自动模式下驱动程序时，驱动程序管理器不会调用**SQLEndTran**驱动程序中。 **SQLEndTran**始终返回而不考虑是否使用调用的 SQL_SUCCESS *CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。  
  
 不支持事务的驱动程序或数据源 (**SQLGetInfo** *选项*SQL_TXN_CAPABLE 是 SQL_TC_NONE) 可以有效地始终自动提交模式并且因此始终返回有关 SQL_SUCCESS**SQLEndTran**是否使用调用*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。 此类驱动程序和数据源不实际回滚事务时，请求执行。  
  
## <a name="suspended-state"></a>挂起的状态  
 在 Windows 7 之前发布的驱动程序管理器中事务处于活动状态如果**SQLEndTran**返回 SQL_ERROR 从驱动程序。 但是，很可能会在服务器上，，具有已成功提交事务，但客户端上的驱动程序具有尚未通知 （例如，因为出现网络错误）。 这将使连接处于错误的状态。 从 Windows 7 开始时**SQLEndTran**返回 SQL_ERROR，连接可能处于挂起状态。 处于挂起状态，则可以调用只读函数。 最终，应用程序应调用**SQLDisconnect**上的挂起的连接，以释放资源。  
  
 如果满足所有以下条件，连接将会处于挂起状态：  
  
-   驱动程序返回从 SQL_ERROR **SQLEndTran**。  
  
-   驱动程序是 ODBC 3.8，或更高版本。  
  
-   应用程序版本为 3.8 或更高版本;或重新编译的 ODBC 2.x 或 3.x 应用程序已成功取消**SQLEndTran**函数通过**SQLCancelHandle**。  
  
-   该驱动程序未返回以下消息，确认事务未完成之一：  
  
    -   25S03： 事务回滚  
  
    -   40001： 序列化失败  
  
    -   40002： 完整性约束  
  
    -   HYC00： 未实现的可选功能  
  
 如果**SQLEndTran**调用在该环境句柄和其连接之一满足上述条件，连接到相同的驱动程序的所有连接将会都处于挂起状态。  
  
 应用程序调用后**SQLDisconnect**挂起连接时，可以使用连接重新连接到另一个数据源或同一数据源。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|取消连接句柄上以异步方式运行的函数。|[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|返回有关的驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|释放语句句柄|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
