---
title: SQLParamData 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 936a45822c06eb530be077f4a43249579ac42c86
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlparamdata-function"></a>SQLParamData 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLParamData**连同使用**SQLPutData**提供参数数据在语句执行时，与**SQLGetData**检索流式处理的输出参数数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ValuePtrPtr*  
 [输出]指向要返回的地址在其中的缓冲区指针*ParameterValuePtr*中指定的缓冲区**SQLBindParameter** （用于参数数据） 或地址*TargetValuePtr*中指定的缓冲区**SQLBindCol** （适用于列数据），如 SQL_DESC_DATA_PTR 描述符记录字段中包含。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLParamData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLParamData**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|由标识的数据值*ValueType*中的参数**SQLBindParameter**对于无法转换的绑定的参数，标识的数据类型为*ParameterType*中的参数**SQLBindParameter**。<br /><br /> 绑定 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 不无法转换为标识的数据类型的参数返回的数据值*ValueType*中的参数**SQLBindParameter**。<br /><br /> （如果无法转换一个或多个行的数据值，但没有成功返回一个或多个行，此函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22026|字符串数据，长度不匹配|中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**被"Y"，并更少的数据已发送 （数据类型不 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源 – 特定数据类型） 的长参数不是指定与*StrLen_or_IndPtr*中的参数**SQLBindParameter**。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**被"Y"，并不是中已指定，较少的数据已发送长列 （数据类型不 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源 – 特定数据类型）对应于已添加或更新的数据的行中的列的长度缓冲区**SQLBulkOperations**或更新与**SQLSetPos**。|  
|40001|序列化失败|事务已回滚，由于资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*; 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 前面的函数调用不是调用**SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**，或**SQLSetPos**其中返回代码为 SQL_NEED_DATA，或以前的函数调用已调用**SQLPutData**。<br /><br /> 以前的函数调用已调用**SQLParamData**。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLParamData**调用函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*和返回的 SQL_NEED_DATA。 **SQLCancel**之前的所有数据在执行参数或列已发送数据时调用。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 的驱动程序对应于*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
 如果**SQLParamData**称为时发送 SQL 语句中的参数的数据，它可能会返回任何可通过调用执行语句的函数返回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果发送的列的数据时调用正在更新或添加与**SQLBulkOperations**或与正在更新**SQLSetPos**，它可返回可以由任何 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>注释  
 **SQLParamData**可以调用以进行提供两种用法的数据在执行数据： 将对的调用中使用的参数数据**SQLExecute**或**SQLExecDirect**，或将列数据时使用更新或通过调用添加某行**SQLBulkOperations**或通过调用更新**SQLSetPos**。 在执行时， **SQLParamData**将返回到应用程序驱动程序需要使用哪些数据的指示符。  
  
 在应用程序调用**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**，驱动程序返回 SQL_NEED_如果它需要数据在执行数据的数据。 应用程序然后调用**SQLParamData**来确定要发送的数据。 如果驱动程序需要参数的数据，该驱动程序将返回在 *\*ValuePtrPtr*输出缓冲区的应用程序放置在行集的缓冲区中的值。 应用程序可以使用此值以确定该驱动程序正在请求的参数数据。 如果该驱动程序需要列数据，该驱动程序返回中 *\*ValuePtrPtr*缓冲列最初已，如下所示绑定到的地址：  
  
 *绑定地址* + *绑定偏移量*+ ((*行号*– 1) x*元素大小*)  
  
 其中按下表中所示定义变量。  
  
|变量|Description|  
|--------------|-----------------|  
|*绑定地址*|使用指定的地址*TargetValuePtr*中的参数**SQLBindCol**。|  
|*绑定偏移量*|存储与 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性指定的地址处的值。|  
|*行号*|基于 1 的行集中的行数。 对于单行更行提取，这是默认安全设置，这是 1。|  
|*元素大小*|数据和长度/指示器缓冲区 SQL_ATTR_ROW_BIND_TYPE 语句属性的值。|  
  
 它还返回 SQL_NEED_DATA，是对应用程序应调用指示器**SQLPutData**发送数据。  
  
 应用程序调用**SQLPutData**进行发送的列或参数的数据在执行数据所需的多次。 所有数据均已都发送的列或参数后，应用程序会调用**SQLParamData**试。 如果**SQLParamData**再次返回 SQL_NEED_DATA，必须将数据发送另一个参数或列。 因此，再次将应用程序调用**SQLPutData**。 如果所有数据在执行数据均已都发送的所有参数或列，然后**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 中的值 *\*ValuePtrPtr*未定义，并可执行 SQL 语句或**SQLBulkOperations**或**SQLSetPos**可处理调用。  
  
 如果**SQLParamData**提供参数的数据搜索更新或删除语句，但不影响数据源，对的调用中的任何行**SQLParamData**返回 SQL_NO_DATA。  
  
 在语句执行时传递数据在执行参数数据有关的详细信息，请参阅"将传递参数值"中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[发送长整型数据](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或添加有关数据在执行列数据的详细信息，请参阅"使用 SQLSetPos"一节中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，"执行大容量更新使用中的书签" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[长数据、 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
 **SQLParamData**可以调用以检索经过流处理的输出参数。 当**SQLMoreResults**， **SQLExecute**， **SQLGetData**，或**SQLExecDirect**返回 SQL_PARAM_DATA_AVAILABLE，调用**SQLParamData**以确定哪个参数的可用值。 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在语句中返回有关参数的信息|[SQLDescribeParam 函数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在执行时发送的参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
