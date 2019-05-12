---
title: SQLEndTran 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16b4bcfec2640c0dbd55d43be9df2391ed1f66c0
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538039"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLEndTran**请求与连接关联的所有语句上的所有活动操作的提交或回滚操作。 **SQLEndTran**还可以请求与环境相关联的所有连接执行的提交或回滚操作。  
  
> [!NOTE]  
>  有关哪些驱动程序管理器的详细信息将时 ODBC 3 映射到此函数。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[向后兼容性的应用程序映射替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]句柄类型标识符。 包含任一 SQL_HANDLE_ENV (如果*处理*是环境的句柄) 或 SQL_HANDLE_DBC (如果*处理*是连接句柄)。  
  
 *Handle*  
 [输入]所指示的类型的句柄*HandleType*，指示事务的范围。 有关详细信息，请参阅"注释"。  
  
 *CompletionType*  
 [输入]以下两个值之一：  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLEndTran**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**具有相应*HandleType*并*处理*。 下表列出了通常返回的 SQLSTATE 值**SQLEndTran** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|（数据挖掘） *HandleType*已 SQL_HANDLE_DBC，并*处理*当时不处于连接状态。|  
|08007|事务期间连接出错|*HandleType*已 SQL_HANDLE_DBC，并与连接相关联*处理*函数，在执行期间失败且不能确定是否请求**提交**或**回滚**故障之前出现。|  
|25S01|事务状态未知|一个或多个中的连接*处理*未指定，结果与完成事务，并且结果为未知。|  
|25S02|事务仍处于活动状态|该驱动程序无法保证无法以原子方式，完成全局事务中的所有工作，并在事务仍处于活动状态。|  
|25S03|事务回滚|该驱动程序无法保证无法以原子方式，完成全局事务中的所有工作，并在事务中处于活动状态中的所有工作*处理*已回滚。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40002|完整性约束冲突|*CompletionType*已 SQL_COMMIT，并提交更改导致完整性约束冲突。 因此，该事务已回滚。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*szMessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*ConnectionHandle*。 调用该函数，和之前完成执行[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*。 然后在再次调用该函数*ConnectionHandle*。<br /><br /> 调用该函数，和之前完成执行**SQLCancelHandle**上调用了*ConnectionHandle*从多线程应用程序中不同的线程。|  
|HY010|函数序列错误|(DM) 为关联的语句句柄调用以异步方式执行的函数*ConnectionHandle*和仍在执行时**SQLEndTran**调用。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *ConnectionHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**与语句句柄关联调用*ConnectionHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似）*处理*与*HandleType*设置为 SQL_HANDLE_DBC 且仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*处理*和返回的 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY012|事务操作代码无效|(DM) 的参数指定的值*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK 既不是。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY092|属性/选项标识符无效|(DM) 的参数指定的值*HandleType* SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 都不是。|  
|HY115|包含与异步函数执行启用连接的环境不允许使用 SQLEndTran|（数据挖掘） *HandleType*不能设置为 SQL_HANDLE_ENV，如果在环境中的连接启用的连接函数的异步执行。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅本主题的注释部分。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持**回滚**操作。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*ConnectionHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 对于 ODBC 3。*x*驱动程序，如果*HandleType*为 SQL_HANDLE_ENV 并*处理*是有效的环境句柄，则驱动程序管理器将调用**SQLEndTran**中每个驱动程序与环境相关联。 *处理*到驱动程序调用的参数将为驱动程序的环境句柄。 适用于 ODBC 2。*x*驱动程序，如果*HandleType*为 SQL_HANDLE_ENV 并*处理*是有效的环境句柄，并且没有在该环境中，连接状态中的多个连接然后驱动程序管理器将调用**SQLTransact**中一次在该环境中连接状态的每个连接的驱动程序。 *处理*中每个调用的参数将为连接的句柄。 在任一情况下，该驱动程序将尝试提交或回滚事务，具体取决于值*CompletionType*，处于连接状态在该环境的所有连接。 处于非活动状态的连接不会影响该事务。  
  
> [!NOTE]  
>  **SQLEndTran**不能用于提交或回滚在共享环境中的事务。 SQLSTATE HY092 将返回 （属性/选项标识符无效），如果**SQLEndTran**使用调用*处理*设置为共享环境中的任一句柄或上共享的连接的句柄环境。  
  
 仅当它收到的每个连接 SQL_SUCCESS，驱动程序管理器将返回 SQL_SUCCESS。 如果驱动程序管理器在一个或多个连接上接收 SQL_ERROR，它返回 SQL_ERROR 应用程序，并将诊断信息置于环境的诊断数据结构。 若要确定哪个连接失败在提交或回滚操作期间，应用程序可以调用**SQLGetDiagRec**为每个连接。  
  
> [!NOTE]  
>  驱动程序管理器不模拟全局事务跨所有连接，因此不会使用两阶段提交协议。  
  
 如果*CompletionType*是 SQL_COMMIT， **SQLEndTran**发出的受影响连接相关联的任何语句上的所有活动操作的提交请求。 如果*CompletionType*是 SQL_ROLLBACK， **SQLEndTran**发出的受影响连接相关联的任何语句上的所有活动操作的回滚请求。 如果没有事务处于活动状态， **SQLEndTran**与不会影响任何数据源都将返回 SQL_SUCCESS。 有关详细信息，请参阅[Committing 和滚动交易记录](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果在手动提交模式下的驱动程序 (通过调用**SQLSetConnectAttr**与 SQL_ATTR_AUTOCOMMIT 属性设置为 SQL_AUTOCOMMIT_OFF)，可以包含在 SQL 语句时，隐式启动新事务对当前数据源执行事务。 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 若要确定事务操作如何影响游标，应用程序调用**SQLGetInfo** SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 选项。 有关详细信息，请参阅以下各段和另请参阅[效果的事务对游标和 Prepared Statements](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_DELETE， **SQLEndTran**关闭和删除与该连接关联的所有语句上所有打开的游标并放弃所有挂起结果。 **SQLEndTran**离开任何语句中已分配 （未准备好） 状态，则存在该应用程序可以将其重复用于后续 SQL 请求也可以调用**SQLFreeStmt**或**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_STMT 以释放它们。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_CLOSE， **SQLEndTran**关闭所有打开的游标与连接关联的所有语句。 **SQLEndTran**离开准备就绪的状态; 中存在的任何语句应用程序可以调用**SQLExecute**与该连接而无需第一个调用关联语句**SQLPrepare**。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等于 SQL_CB_PRESERVE， **SQLEndTran**不会影响与连接关联的打开的游标。 游标会保留在指向调用之前的行**SQLEndTran**。  
  
 支持事务，调用的驱动程序和数据源**SQLEndTran**使用 SQL_COMMIT 或 SQL_ROLLBACK 没有事务处于活动状态时返回 SQL_SUCCESS （指示已没有要提交或回滚）和对数据源没有影响。  
  
 自动提交模式驱动程序时，驱动程序管理器不会调用**SQLEndTran**驱动程序中。 **SQLEndTran**而不考虑是否使用调用将始终返回 SQL_SUCCESS *CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。  
  
 不支持事务的驱动程序或数据源 (**SQLGetInfo** *选项*SQL_TXN_CAPABLE 是 SQL_TC_NONE) 有效地始终处于自动提交模式，因此始终返回 SQL_SUCCESS 为**SQLEndTran**该值指示是否使用调用*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。 此类驱动程序和数据源不实际回滚事务时，请求执行。  
  
## <a name="suspended-state"></a>挂起的状态  
 在 Windows 7 之前发布的驱动程序管理器，在一个事务处于活动状态如果**SQLEndTran**从驱动程序返回 SQL_ERROR。 但是，很可能该事务已成功提交的服务器上，但客户端上的驱动程序必须尚未通知 （例如，因为出现网络错误）。 这会将连接置于错误的状态。 从 Windows 7 开始时**SQLEndTran**返回 SQL_ERROR，连接可能处于挂起状态。 处于挂起状态，则可以调用只读函数。 最终，应用程序应调用**SQLDisconnect**上挂起的连接，以释放资源。  
  
 如果所有以下条件都为 true，连接将会处于挂起状态：  
  
-   驱动程序将返回从 SQL_ERROR **SQLEndTran**。  
  
-   该驱动程序是 ODBC 3.8，或更高版本。  
  
-   应用程序版本是 3.8 或更高版本;或重新编译的 ODBC 2.x 或 3.x 应用程序已成功取消**SQLEndTran**函数通过**SQLCancelHandle**。  
  
-   该驱动程序未返回确认事务未完成的以下消息之一：  
  
    -   25S03:事务回滚  
  
    -   40001:序列化失败  
  
    -   40002:完整性约束  
  
    -   HYC00:未实现的可选功能  
  
 如果**SQLEndTran**调用了上一个环境句柄，它的连接的另一个满足上述条件，连接到相同的驱动程序的所有连接将会都处于挂起状态。  
  
 应用程序调用后**SQLDisconnect**挂起连接时，可以使用连接重新连接到另一个数据源或相同的数据源。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|正在取消连接句柄上以异步方式运行的函数。|[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|释放语句句柄|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
