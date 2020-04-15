---
title: SQL取消处理功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299662"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数
**一致性**  
 版本介绍： ODBC 3.8  
  
 标准合规性：无  
  
 预计大多数 ODBC 3.8（以及更高版本）驱动程序将实现此功能。 如果驱动程序没有，则调用**SQLCancelHandle**与*句柄*参数中的连接句柄将返回SQL_ERROR，其中 SQLSTATE 为 IM001，消息"驱动程序不支持此功能";对**SQLCancelHandle**的调用具有语句句柄，因为*句柄*参数将映射到驱动程序管理器对**SQLCancel**的调用，如果驱动程序实现**SQLCancel，** 则可以进行处理。 应用程序可以使用**SQLGet 函数**来确定驱动程序是否支持**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**取消连接或语句上的处理。 当*处理类型*SQL_HANDLE_STMT时，驱动程序管理器将**SQLCancelHandle**的呼叫映射到**SQLCancel**的调用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要处理的句柄的类型。 有效值SQL_HANDLE_DBC或SQL_HANDLE_STMT。  
  
 *Handle*  
 [输入]要取消处理的句柄。  
  
 如果*句柄*不是*HandleType*指定的类型的有效句柄 **，SQLCancelHandle**将返回SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCancelHandle**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和语句*句柄*或SQL_HANDLE_DBC的处理*类型*和连接*句柄句柄*。  
  
 下表列出了**SQLCancelHandle**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)在参数*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|对于与*句柄*关联的语句句柄之一，调用了异步执行语句相关的函数，并且*HandleType*设置为SQL_HANDLE_DBC。 调用**SQLCancelHandle**时，异步函数仍在执行。<br /><br /> （DM）*句柄类型*参数SQL_HANDLE_STMT;在关联的连接句柄上调用了异步执行函数;调用此函数时，该函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用，其中一个语句句柄与*句柄*和*句柄类型*相关联，设置为SQL_HANDLE_DBC，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> **SQLBrowseConnect**被调用为*连接句柄*，并返回SQL_NEED_DATA。 在浏览过程完成之前调用此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY092|无效属性/选项标识符|*句柄类型*设置为SQL_HANDLE_ENV或SQL_HANDLE_DESC。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*句柄*关联的驱动程序不支持该功能。|  
  
 如果**SQLCancelHandle**调用的*句柄设置为*SQL_HANDLE_STMT，它可以返回函数**SQLCancel**可以返回的任何 SQLSTATE。  
  
## <a name="comments"></a>注释  
 此功能类似于**SQLCancel，** 但可以将连接或语句句柄作为参数，而不仅仅是语句句柄。 当*处理类型*SQL_HANDLE_STMT时，驱动程序管理器将**SQLCancelHandle**的呼叫映射到**SQLCancel**的调用。 这允许应用程序使用**SQLCancelHandle**取消语句操作，即使驱动程序未实现**SQLCancelHandle**。  
  
 有关取消语句操作的详细信息，请参阅[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果*处理***SQLCancelHandle**的调用没有正在进行的操作，则不起作用。  
  
 **连接句柄上的 SQLCancelHandle**可以取消以下类型的处理：  
  
-   在连接上异步运行的函数。  
  
-   在另一个线程的连接句柄上运行的函数。  
  
 当调用 SQLCancelHandle 以取消在连接中异步运行的函数时 **，SQLCancelHandle**发布的诊断记录将追加到被取消的操作返回的那些记录中;如果调用**SQLCancelHandle，** 则将 SQLCancelHandle 发布的诊断记录追加到已取消的操作返回的那些记录中。但是，当取消在另一个线程上的连接上运行的函数时 **，SQLCancelHandle**不会返回诊断记录。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能会将连接置于挂起状态。 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  有关如何在将部署在 Windows 操作系统早于 Windows 7 的 Windows 操作系统上的应用程序中使用**SQLCancelHandle**的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>取消连接相关的异步处理  
 如果函数返回SQL_STILL_EXECUTING，应用程序可以调用**SQLCancelHandle**取消该操作。 如果取消请求成功 **，SQLCancelHandle**将返回SQL_SUCCESS。 这并不意味着原始函数已取消;因此，它未取消原始函数。它表示已处理取消请求。 驱动程序和数据源确定何时取消操作或是否取消操作。 应用程序必须继续调用原始函数，直到返回代码不SQL_STILL_EXECUTING。 如果原始函数已取消，则返回代码SQL_ERROR SQLSTATE HY008（操作已取消）。 如果原始函数完成其正常处理（未取消），则返回代码SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，或SQL_ERROR和 SQLSTATE 以外的 HY008（操作已取消），如果原始函数失败。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>取消在另一个线程上执行的函数  
 在多线程应用程序中，应用程序可以取消在另一个线程上运行的操作。 要取消该操作，应用程序调用**SQLCancelHandle，** 该句柄由函数使用，但调用其他线程。 驱动程序和操作系统确定如何取消操作。 **SQLCancelHandle**返回代码指示驱动程序是处理请求，返回SQL_SUCCESS或SQL_ERROR（不返回任何诊断信息）。 如果取消对原始函数的处理，则原始函数将返回SQL_ERROR和 SQLSTATE HY008（操作已取消）。  
  
 如果在调用另一个线程上调用**SQLCancelHandle**来取消该函数时正在执行函数，则函数可以成功并返回SQL_SUCCESS，然后取消才能生效。 如果**SQLCancelHandle**之前的操作已完成，则对**SQLCancelHandle**的调用不起作用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|取消在语句句柄上异步运行的函数，取消需要数据的语句上的函数，或取消在另一个线程上运行语句上的函数。|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
