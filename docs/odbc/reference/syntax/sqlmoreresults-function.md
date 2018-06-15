---
title: SQLMoreResults 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d156b07358d6430ec52f000ed4bebfe1c5d19d9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923432"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLMoreResults**确定是否可在上找到的语句包含更多结果**选择**，**更新**，**插入**，或**删除**语句，如果是这样，初始化为而处理这些结果。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLMoreResults**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLMoreResults**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|在处理更改为批处理语句属性的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 **SQLMoreResults**已调用函数，并且，它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*. 则**SQLMoreResults**函数上调用了再次*StatementHandle*。<br /><br /> **SQLMoreResults**已调用函数，并且，它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*从多线程应用程序中的不同线程。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLMoreResults**调用函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **选择**语句返回结果集。 **更新**，**插入**，和**删除**语句返回受影响的行的计数。 如果任何这些语句进行批处理，提交包含数组的参数 （按顺序编号以升序参数，它们在批处理中出现的顺序），或在过程中，可以返回多个结果集或行计数。 有关的语句的批处理和参数的数组的信息，请参阅[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 在执行批处理后, 应用程序位于第一个结果集。 应用程序可以调用**SQLBindCol**， **SQLBulkOperations**， **SQLFetch**， **SQLGetData**， **SQLFetchScroll**， **SQLSetPos**，和上的第一个或任何后续的结果集，就像好像有只需单个结果集的所有元数据函数。 在应用程序后使用完毕后第一个结果集，调用**SQLMoreResults**将移到下一个结果集。 如果另一个结果集或计数不可用， **SQLMoreResults**返回 SQL_SUCCESS 并初始化的结果集或以进行其他处理的计数。 如果任何行生成计数 – 语句之间显示结果集生成语句，请它们可以步长越过调用**SQLMoreResults**。在调用**SQLMoreResults**为**更新**，**插入**，或**删除**语句，应用程序可以调用**SQLRowCount**。  
  
 如果没有当前具有的结果集的行会， **SQLMoreResults**将放弃该结果集，并使下一个结果集或对用法计数可用。 如果已处理所有结果， **SQLMoreResults**返回 SQL_NO_DATA。 某些驱动程序，为输出参数和返回值之前将不可用在处理所有结果集和行计数。 对于此类驱动程序，输出参数和返回值可用时**SQLMoreResults**返回 SQL_NO_DATA。  
  
 上面的结果集仍建立任何绑定保持有效。 如果此结果集不同的列结构，然后调用**SQLFetch**或**SQLFetchScroll**可能会导致错误或截断。 若要防止此情况，应用程序调用**SQLBindCol**要明确地根据需要重新绑定 （或通过设置描述符字段来做到）。 或者，应用程序可以调用**SQLFreeStmt**与*选项*的 SQL_UNBIND 以取消绑定所有列缓冲区。  
  
 语句属性，如游标类型、 光标并发、 键集大小或最大长度的值可能会随应用程序的调用定位通过批处理**SQLMoreResults**。 如果发生这种情况， **SQLMoreResults**将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （选项值已更改）。  
  
 调用**SQLCloseCursor**，或**SQLFreeStmt**与*选项*的 SQL_CLOSE，放弃所有结果集和可用的执行结果的行计数批处理。 语句句柄返回为已分配或已准备状态。 调用**SQLCancel**取消异步执行的函数执行批处理和语句句柄中执行，光标定位的或者导致所有都结果集的异步状态，行计数批处理被放弃，如果取消调用已成功生成。 然后该语句返回到已准备或已分配状态。  
  
 如果一批语句或过程，可将混合与其他 SQL 语句**选择**，**更新**，**插入**，和**删除**语句，这些其他语句不会影响**SQLMoreResults**。  
  
 有关详细信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜索的更新、 插入或删除语句中的一批语句不会影响数据源中的任何行**SQLMoreResults**返回 SQL_SUCCESS。 这是不同于搜索更新的大小写、 插入或删除通过执行的语句**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，后者如果它不会影响数据源中的任何行，则返回 SQL_NO_DATA。 如果应用程序调用**SQLRowCount**到调用后检索行计数**SQLMoreResults**不影响任何行， **SQLRowCount**将返回 SQL_NO_DATA。  
  
 有关有效的序列化结果处理功能的其他信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>行计数的可用性  
 当一批包含多个连续的行计数 – 生成语句时，有可能这些行数将累加起来到只在一行计数。 例如，如果批含有五个 insert 语句，则某些数据源将能够返回五个单个行计数。 某些其他数据源返回表示五个单个行计数的总和的只有一个行计数。  
  
 当一批包含的结果集 – 生成和行计数 – 生成语句组合时，行计数可能或可能根本不可用。 在通过调用可用的 SQL_BATCH_ROW_COUNT 信息类型中枚举的行计数的可用性方面驱动程序的行为**SQLGetInfo**。 例如，假设批处理包含**选择**后, 跟两个**插入**s，另一个**选择**。 然后则可能发生以下情况：  
  
-   行计数对应于两个**插入**语句根本不可用。 首次调用**SQLMoreResults**将置于你的第二个结果集**选择**语句。  
  
-   行计数对应于两个**插入**语句是单独可用。 (调用**SQLGetInfo**不返回 SQL_BATCH_ROW_COUNT 信息类型的 SQL_BRC_ROLLED_UP 位。)首次调用**SQLMoreResults**将置于你的第一个行计数**插入**，第二个调用将置于你的第二个行计数和**插入**。 第三个调用**SQLMoreResults**将置于你的第二个结果集**选择**语句。  
  
-   行计数对应于两个**插入**汇总到一个可用的单个行计数。 (调用**SQLGetInfo**返回 SQL_BATCH_ROW_COUNT 信息类型的位 SQL_BRC_ROLLED_UP。)首次调用**SQLMoreResults**将帮助你置于汇总的行计数和第二次调用**SQLMoreResults**将置于你的第二个结果集**选择**.  
  
 某些驱动程序提供行计数仅对于显式批处理而不是针对存储过程。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取部分或全部数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
