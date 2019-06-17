---
title: SQLParamData 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0d92abe17128bff382d4b291fa9d20fe5c4fa77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536641"
---
# <a name="sqlparamdata-function"></a>SQLParamData 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLParamData**使用连同**SQLPutData**提供参数数据在语句执行时，且**SQLGetData**检索流式处理的输出参数数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ValuePtrPtr*  
 [输出]指向要返回的地址在其中的缓冲区*ParameterValuePtr*中指定的缓冲区**SQLBindParameter** （适用于参数数据） 或地址*TargetValuePtr*中指定的缓冲区**SQLBindCol** （适用于列数据），如 SQL_DESC_DATA_PTR 描述符记录字段中包含。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLParamData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLParamData** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|标识的数据值*ValueType*中的参数**SQLBindParameter**无法为数据类型由标识转换绑定的参数为*ParameterType*中的参数**SQLBindParameter**。<br /><br /> 参数绑定为 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 不无法转换为标识的数据类型返回的数据值*ValueType*中的参数**SQLBindParameter**。<br /><br /> （如果无法转换为一个或多个行的数据值，但没有成功返回一个或多个行，此函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22026|字符串数据，长度不匹配|中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo** "Y"，不是指定了较少的数据已发送长参数 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源特定的数据类型）与*StrLen_or_IndPtr*中的参数**SQLBindParameter**。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**为"Y"，而且比中指定了较少的数据已发送长列 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源特定的数据类型）对应于已添加或使用更新的数据行中的列长度的缓冲区**SQLBulkOperations**或更新，它**SQLSetPos**。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*; 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 以前的函数调用不是调用**SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**，或者**SQLSetPos**其中返回代码为 SQL_NEED_DATA，或上一个函数调用已调用**SQLPutData**。<br /><br /> 上一个函数调用已调用**SQLParamData**。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLParamData**调用函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*和返回的 SQL_NEED_DATA。 **SQLCancel**数据已发送的所有执行时数据参数或列之前调用。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
 如果**SQLParamData**调用时发送参数数据中的 SQL 语句，它可以返回任何可由函数调用以执行该语句返回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果发送数据的列时调用正在进行更新或添加具有**SQLBulkOperations**或使用更新**SQLSetPos**，它可以返回任何可由返回的 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>注释  
 **SQLParamData**可以调用来提供这两种用法的数据执行时数据： 将对的调用中使用的参数数据**SQLExecute**或**SQLExecDirect**，或将列数据时使用更新或通过调用添加行**SQLBulkOperations**或通过调用更新**SQLSetPos**。 在执行时， **SQLParamData**返回到应用程序驱动程序需要使用哪些数据的指示器。  
  
 当应用程序调用**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**，驱动程序返回 SQL_NEED_如果它需要执行时数据的数据的数据。 随后，应用程序调用**SQLParamData**来确定要发送的数据。 如果该驱动程序需要参数的数据，驱动程序将返回在 *\*ValuePtrPtr*输出缓冲区的应用程序放在行集的缓冲区中的值。 应用程序可以使用此值以确定驱动程序正在请求的参数数据。 如果该驱动程序需要列数据，驱动程序将返回在 *\*ValuePtrPtr*缓冲区列最初已按如下所示绑定到的地址：  
  
 *绑定地址* + *绑定偏移量*+ ((*行号*-1) x*元素大小*)  
  
 其中变量定义下表中所示。  
  
|变量|Description|  
|--------------|-----------------|  
|*绑定地址*|使用指定的地址*TargetValuePtr*中的参数**SQLBindCol**。|  
|*绑定偏移量*|存储与 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性指定的地址的值。|  
|*行号*|从 1 开始的行集中的行数。 对于单行提取操作，这是默认值，这是 1。|  
|*元素大小*|数据和长度/指示器缓冲区将 SQL_ATTR_ROW_BIND_TYPE 语句属性的值。|  
  
 它还会返回 SQL_NEED_DATA，这是一个指示符，则应调用的应用程序**SQLPutData**发送数据。  
  
 应用程序调用**SQLPutData**尽可能多地需要发送的列或参数的数据执行时数据。 列或参数发送的所有数据后，应用程序调用**SQLParamData**试。 如果**SQLParamData**再次返回 SQL_NEED_DATA，必须将数据发送另一个参数或列。 因此，再次将应用程序调用**SQLPutData**。 如果执行时数据的所有数据已都发送的所有参数或列，然后**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 中的值 *\*ValuePtrPtr*未定义，和可执行 SQL 语句或**SQLBulkOperations**或**SQLSetPos**调用可以进行处理。  
  
 如果**SQLParamData**提供，数量参数的数据搜索 update 或 delete 语句，但不影响任何行在数据源，调用**SQLParamData**返回 sql_no_data 为止。  
  
 在语句执行时传递有关如何执行时的数据参数数据的详细信息，请参阅"传递参数值"中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)并[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。 对于更新或添加有关如何执行时的数据列数据的详细信息，请参阅"使用 SQLSetPos"一节中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，"执行大容量更新使用中的书签" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，并[Long 数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
 **SQLParamData**可以调用以检索经过流处理的输出参数。 当**SQLMoreResults**， **SQLExecute**， **SQLGetData**，或者**SQLExecDirect**返回 SQL_PARAM_DATA_AVAILABLE，调用**SQLParamData**以确定哪些参数的可用值。 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
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
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
