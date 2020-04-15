---
title: SQLMore 结果函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304738"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLMore结果**确定在包含**SELECT、UPDATE、****插入**或**SELECT** **DELETE**语句的语句上是否提供更多结果，如果是，则初始化这些结果的处理。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLMore 结果**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLMore 结果**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|处理批处理时，语句属性的值已更改。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 **SQLMore结果**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句句柄*上再次调用**SQLMore 结果**函数。<br /><br /> **SQLMore结果**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**从多线程应用程序中的不同线程调用了*语句处理*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLMore结果**函数时，此异步函数仍在执行。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **选择**语句返回结果集。 **更新**、**插入**和**删除**语句返回受影响的行的计数。 如果对这些语句中的任何一个进行批处理，并且使用参数数组（按增加参数顺序编号、按批处理中显示的顺序）或过程中提交，它们可以返回多个结果集或行计数。 有关参数的语句和数组的批处理的信息，请参阅 SQL[语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[参数值数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 执行批处理后，应用程序将定位在第一个结果集中。 该应用程序可以在第一个或任何后续结果集中调用**SQLBindCol、SQLBulk****操作**、SQLFetch、SQLGetData、SQLFetchScroll、SQLSetPos 和所有元数据函数，就像只有单个结果集一样。 **SQLFetch** **SQLGetData** **SQLFetchScroll** **SQLSetPos** 使用第一个结果集完成后，应用程序将调用**SQLMoreResult**移动到下一个结果集。 如果另一个结果集或计数可用 **，SQLMoreResult**将返回SQL_SUCCESS并初始化结果集或计数以进行其他处理。 如果任何行计数生成语句出现在结果集生成语句之间，则可以通过调用**SQLMoreResult**来逐步结束这些语句。调用**SQLMore 结果**进行**更新**、**插入**或**删除**语句后，应用程序可以调用**SQLRowCount**。  
  
 如果存在当前结果集，其中行未提取 **，SQLMoreResult**将丢弃该结果集，并使下一个结果集或计数可用。 如果处理了所有结果 **，SQLMore 结果**将返回SQL_NO_DATA。 对于某些驱动程序，在处理了所有结果集和行计数之前，输出参数和返回值不可用。 对于此类驱动程序，当**SQLMore 结果**返回SQL_NO_DATA时，输出参数和返回值将可用。  
  
 为上一个结果集建立的任何绑定仍然有效。 如果此结果集的列结构不同，则调用**SQLFetch**或**SQLFetchScroll**可能会导致错误或截断。 为了防止这种情况，应用程序必须调用**SQLBindCol**以根据需要显式重新绑定（或者通过设置描述符字段来执行此操作）。 或者，应用程序可以使用SQL_UNBIND*选项*调用**SQLFreeStmt**以取消绑定所有列缓冲区。  
  
 语句属性的值（如游标类型、游标并发、键集大小或最大长度）可能会随着应用程序通过调用**SQLMore结果**在批处理中导航而更改。 如果发生这种情况 **，SQLMore结果**将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02（选项值已更改）。  
  
 调用**SQLCloseCursor**或*Option***SQLFreeStmt**的选项SQL_CLOSE，将丢弃执行批处理后可用的所有结果集和行计数。 语句句柄返回到已分配或准备的状态。 调用**SQLCancel**以在已执行批处理且语句句柄处于执行、游标定位或异步状态时取消异步执行功能，这将导致在取消调用成功时丢弃的批处理生成的所有结果集和行计数。 然后，语句返回到已准备或分配的状态。  
  
 如果一批语句或过程将其他 SQL 语句与**SELECT、****更新**、**插入**和**DELETE**语句混合在一起，则这些其他语句不会影响**SQLMore结果**。  
  
 有关详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜索的更新、插入或删除一批语句中的语句不会影响数据源中的任何行 **，SQLMore结果**将返回SQL_SUCCESS。 这与通过**SQLExecDirect、SQLExecute**或**SQLParamData**执行的搜索更新、插入或删除**SQLExecute**语句的情况不同，如果该语句不影响数据源上的任何行，则返回SQL_NO_DATA。 如果应用程序调用**SQLRowCount**以检索对**SQLMore 结果**的调用后检索行计数，则**SQLRowCount**将返回SQL_NO_DATA。  
  
 有关结果处理函数的有效排序的其他信息，请参阅[附录 B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关SQL_PARAM_DATA_AVAILABLE和流式输出参数的详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>行计数的可用性  
 当批处理包含多个连续行计数生成语句时，这些行计数可能仅汇总到一行计数中。 例如，如果批处理有五个插入语句，则某些数据源能够返回五个单独的行计数。 某些其他数据源仅返回一个表示五个单独行计数总和的行计数。  
  
 当批处理包含结果集生成语句和行计数生成语句的组合时，行计数可能根本不可用，也可能不可用。 驱动程序在行计数可用性方面的行为在通过调用**SQLGetInfo**提供的SQL_BATCH_ROW_COUNT信息类型中枚举。 例如，假设批处理包含**SELECT**，后跟两个**INSERT**和另一个**SELECT**。 然后，以下情况是可能的：  
  
-   与两个**INSERT**语句对应的行计数根本不可用。 对**SQLMore 结果**的第一次调用将您定位在第二个**SELECT**语句的结果集中。  
  
-   对应于两个**INSERT**语句的行计数单独可用。 （对**SQLGetInfo**的调用不会返回SQL_BATCH_ROW_COUNT信息类型的SQL_BRC_ROLLED_UP位。对**SQLMore 结果**的第一个调用将定位您在第一个**INSERT**的行计数上，第二个调用将您定位在第二个**INSERT**的行计数上。 对**SQLMore 结果**的第三次调用将定位您在第二个**SELECT**语句的结果集中。  
  
-   对应于两个**INSERT 的**行计数将汇总为一个可用的行计数。 （对**SQLGetInfo**的调用返回SQL_BATCH_ROW_COUNT信息类型的SQL_BRC_ROLLED_UP位。对**SQLMore 结果**的第一个调用将您定位在汇总行计数上，而对**SQLMore 结果**的第二个调用将您定位在第二个**SELECT**的结果集中。  
  
 某些驱动程序使行计数仅适用于显式批处理，而不适用于存储过程。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据列的一部分或全部|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
