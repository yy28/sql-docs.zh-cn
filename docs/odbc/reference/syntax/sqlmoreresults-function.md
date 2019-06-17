---
title: SQLMoreResults 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd3569425a862efd662c894c6839eb6df0f767e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536511"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLMoreResults**确定是否可在上一个语句，其中包含更多结果**选择**，**更新**，**插入**，或**删除**语句而如果是这样，初始化处理这些结果。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLMoreResults**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLMoreResults** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|正在处理更改与批处理语句属性的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 **SQLMoreResults**调用函数时，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*. 然后**SQLMoreResults**上再次调用函数*StatementHandle*。<br /><br /> **SQLMoreResults**调用函数时，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*从多线程应用程序中不同的线程。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLMoreResults**调用函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **选择**语句返回结果集。 **更新**，**插入**，和**删除**语句返回受影响的行计数。 如果任何这些语句进行批处理，提交的包含数组的参数 （编号参数按，它们在批处理中出现的顺序升序排列），或在过程中，它们可以返回多个结果集或行计数。 有关语句的批处理和参数的数组的信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)并[参数值数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 执行批处理后, 应用程序位于第一个结果集。 应用程序可以调用**SQLBindCol**， **SQLBulkOperations**， **SQLFetch**， **SQLGetData**， **SQLFetchScroll**， **SQLSetPos**，和上的第一个或任何后续结果集，就像没有只是单个结果集的所有元数据函数。 一旦完成了第一个结果集，应用程序调用**SQLMoreResults**将移到下一个结果集。 如果可用，另一个结果集或计数**SQLMoreResults**返回 SQL_SUCCESS 和初始化的结果集或进行其他处理的计数。 如果任何行计数生成语句之间显示结果集生成语句，请在可以转移调用踩**SQLMoreResults**。在调用**SQLMoreResults**有关**更新**，**插入**，或者**删除**语句，应用程序可以调用**SQLRowCount**。  
  
 如果有一个当前结果集的行会，其中**SQLMoreResults**将放弃该结果集，并使下一个结果集或计数可用。 如果已处理了所有结果，则**SQLMoreResults**返回 sql_no_data 为止。 对于某些驱动程序，输出参数和返回值之前将不可用在处理所有结果集和行计数。 对于此类驱动程序，输出参数和返回值时可用**SQLMoreResults**返回 sql_no_data 为止。  
  
 上面的结果集仍已建立任何绑定仍将有效。 如果此结果集不同的列结构，然后调用**SQLFetch**或**SQLFetchScroll**可能会导致错误或截断。 若要防止此情况，应用程序必须调用**SQLBindCol**要明确地根据需要重新绑定 （或通过设置描述符字段）。 或者，应用程序可以调用**SQLFreeStmt**与*选项*SQL_UNBIND 取消绑定所有列缓冲区。  
  
 语句属性，例如游标类型、 游标并发、 由键集大小或最大长度的值可能会随应用程序导航到调用批处理**SQLMoreResults**。 如果发生这种情况， **SQLMoreResults**将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。  
  
 调用**SQLCloseCursor**，或**SQLFreeStmt**与*选项*的 SQL_CLOSE，放弃所有结果集和可用的执行结果的行计数批处理。 语句句柄返回到已分配或已准备状态。 调用**SQLCancel**取消异步执行函数时执行批处理和光标定位在所执行的是语句句柄或导致所有都结果集的异步状态和行计数如果已成功取消调用被放弃批处理生成。 然后该语句返回到已准备好或已分配状态。  
  
 如果一批语句或过程混合使用与其他 SQL 语句**选择**，**更新**，**插入**，以及**删除**语句，这些其他语句不会影响**SQLMoreResults**。  
  
 有关详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜索更新、 插入或删除语句在批语句不会影响任何行在数据源**SQLMoreResults**返回 SQL_SUCCESS。 这与不同的搜索更新的大小写、 insert 或 delete 语句，通过执行**SQLExecDirect**， **SQLExecute**，或**SQLParamData**、 哪些如果它不会影响任何行在数据源，返回 sql_no_data 为止。 如果应用程序调用**SQLRowCount**之后的调用中检索行计数**SQLMoreResults**不影响任何行**SQLRowCount**将返回 sql_no_data 为止。  
  
 有关有效的序列化结果处理功能的其他信息，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>行计数的可用性  
 当批处理包含多个连续的行计数生成语句时，就可以，这些行计数都会计入一个行计数。 例如，如果批含有五个 insert 语句，则某些数据源是能够返回五个单独的行计数。 某些其他数据源返回表示五个单独行计数之和的只有一个行计数。  
  
 当一批中包含的结果集生成和行计数生成语句组合时，行计数，可能会或可能根本不可用。 行计数的可用性方面的驱动程序的行为 SQL_BATCH_ROW_COUNT 信息类型可通过调用中枚举**SQLGetInfo**。 例如，假设批处理包含**选择**后, 跟两个**插入**s，另一个**选择**。 然后则可能发生以下情况：  
  
-   与这两个相对应的行计数**插入**根本不语句。 首次调用**SQLMoreResults**将在第二个结果集上进行定位**选择**语句。  
  
-   与这两个相对应的行计数**插入**语句是单独提供。 (调用**SQLGetInfo**不返回 SQL_BATCH_ROW_COUNT 信息类型的 SQL_BRC_ROLLED_UP 位。)首次调用**SQLMoreResults**帮助您在第一个行计数**插入**，并将第二次调用将置于您在第二个行计数**插入**。 第三个调用**SQLMoreResults**将在第二个结果集上进行定位**选择**语句。  
  
-   与这两个相对应的行计数**插入**汇总到一个可用的单个行计数。 (调用**SQLGetInfo**返回 SQL_BRC_ROLLED_UP 位 SQL_BATCH_ROW_COUNT 信息类型。)首次调用**SQLMoreResults**帮助您汇总的行计数和第二次调用**SQLMoreResults**将在第二个结果集上进行定位**选择**.  
  
 某些驱动程序提供行计数仅为显式批处理而不是针对存储过程。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|正在提取部分或全部的数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
