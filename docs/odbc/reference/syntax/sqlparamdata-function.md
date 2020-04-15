---
title: SQLParamData 功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306918"
---
# <a name="sqlparamdata-function"></a>SQLParamData 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLParamData**与**SQLPutData**一起使用，在语句执行时提供参数数据，并与**SQLGetData**一起检索流式输出参数数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *价值PtrPtr*  
 [输出]指向用于返回**SQLBind参数**中指定的*参数ValuePtr*缓冲区的地址（用于参数数据）或**SQLBindCol**中指定的*TargetValuePtr*缓冲区的地址（对于列数据）的缓冲区的指针，SQL_DESC_DATA_PTR描述符记录字段中所包含。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLParamData**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLParamData**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|绑定参数的**SQLBind 参数**中*的值类型*参数标识的数据值无法转换为**SQLBind 参数**中的*参数类型*参数标识的数据类型。<br /><br /> 返回为SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT绑定的参数的数据值无法转换为**SQLBind 参数**中*ValueType*参数标识的数据类型。<br /><br /> （如果无法转换一个或多个行的数据值，但成功返回一个或多个行，则此函数将返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22026|字符串数据，长度不匹配|**SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN信息类型为"Y"，对于长参数（数据类型为SQL_LONGVARCHAR、SQL_LONGVARBINARY或长数据源特定数据类型）发送的数据少于**SQLBind 参数**中*StrLen_or_IndPtr*参数中指定的数据。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN信息类型为"Y"，对于长列（数据类型SQL_LONGVARCHAR、SQL_LONGVARBINARY或长数据源特定数据类型）发送的数据比在与使用**SQLBulk 操作**添加或更新或使用**SQLSetPos**更新的数据行中的列对应的长度缓冲区中指定的数据较少。|  
|40001|序列化失败|由于资源与另一个事务死锁，事务被回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*;然后，在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 以前的函数调用不是对 SQLExecDirect、SQLExecute、SQLBulk**操作**或**SQLSetPos**的调用，其中返回代码SQL_NEED_DATA，或者以前的函数调用是对**SQLExecDirect****SQLPutData**的调用。 **SQLExecute**<br /><br /> 前面的函数调用是对**SQLParamData**的调用。<br /><br /> （DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLParamData**函数时，此异步函数仍在执行。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> **SQLExecute**SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于*语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** **SQLCancel**是在为执行时的所有数据参数或列发送数据之前调用的。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 对应于*语句句柄*的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
 如果在 SQL 语句中为参数发送数据时调用**SQLParamData，** 它可以返回调用执行语句 **（SQLExecute**或**SQLExecDirect）** 的函数可以返回的任何 SQLSTATE。 如果在发送使用**SQLBulk 操作**更新或添加的列的数据或使用**SQLSetPos**更新时调用它，则可以返回**SQLBulk 操作**或**SQLSetPos**可以返回的任何 SQLSTATE。  
  
## <a name="comments"></a>注释  
 **SQLParamData**可以调用提供执行时的数据，用于两个用途：参数数据，用于 SQLExecute 或**SQLExecDirect**的**SQLExecDirect**调用，或者列数据，这些数据将在调用**SQLBulk 操作**或通过调用**SQLSetPos**更新或更新行时使用。 在执行时 **，SQLParamData**会向应用程序返回驱动程序所需的数据的指示器。  
  
 当应用程序调用**SQLExecute**SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**时，驱动程序在需要执行数据的数据时返回SQL_NEED_DATA。 **SQLExecDirect** 然后，应用程序调用**SQLParamData**以确定要发送的数据。 如果驱动程序需要参数数据，驱动程序在*\*ValuePtrPtr*输出缓冲区中返回应用程序在行集缓冲区中放置的值。 应用程序可以使用此值来确定驱动程序请求的参数数据。 如果驱动程序需要列数据，驱动程序将返回*\*ValuePtrPtr*缓冲区中该列最初绑定到的地址，如下所示：  
  
 *绑定地址* + *绑定偏移*量 = （（*行号*- 1） x*元素大小*）  
  
 其中变量定义如下表所示。  
  
|变量|描述|  
|--------------|-----------------|  
|*绑定地址*|在**SQLBindCol**中使用*TargetValuePtr*参数指定的地址。|  
|*绑定偏移*|存储在使用SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性指定的地址的值。|  
|*Row Number*|行集中的行的 1 个基于的编号。 对于默认的单行提取，这是 1。|  
|*元素大小*|数据和长度/指标缓冲区SQL_ATTR_ROW_BIND_TYPE语句属性的值。|  
  
 它还返回SQL_NEED_DATA，这是应用程序应调用**SQLPutData**发送数据的指示器。  
  
 应用程序根据需要多次调用**SQLPutData**以发送列或参数的执行数据。 为列或参数发送所有数据后，应用程序将再次调用**SQLParamData。** 如果**SQLParamData**再次返回SQL_NEED_DATA，则必须为另一个参数或列发送数据。 因此，应用程序再次调用**SQLPutData**。 如果已为所有参数或列发送了所有执行数据数据，则**SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，*\*则 ValuePtrPtr*中的值未定义，可以执行 SQL 语句或处理**SQLBulk 操作**或**SQLSetPos**调用。  
  
 如果**SQLParamData**为搜索的更新或删除语句提供参数数据，而该语句不会影响数据源上的任何行，则对**SQLParamData**的调用将返回SQL_NO_DATA。  
  
 有关如何在语句执行时传递数据执行时参数数据的详细信息，请参阅[SQLBind 参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)中的"传递参数值"和["发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)"。 有关如何更新或添加数据执行列数据的详细信息，请参阅 SQLSetPos 中的"使用[SQLSetPos"](../../../odbc/reference/syntax/sqlsetpos-function.md)部分[、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的"使用书签执行批量更新"以及[长数据和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)节。  
  
 可以调用**SQLParamData**来检索流式输出参数。 当**SQLMore 结果****、SQLExecute、SQLGetData**或**SQLExecDirect**返回SQL_PARAM_DATA_AVAILABLE时，调用**SQLParamData**以确定哪个参数具有可用的值。 **SQLGetData** 有关SQL_PARAM_DATA_AVAILABLE和流式输出参数的详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回语句中有关参数的信息|[SQLDescribeParam 函数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
