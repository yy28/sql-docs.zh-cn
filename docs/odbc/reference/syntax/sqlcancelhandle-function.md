---
title: SQLCancelHandle 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f572e9e76f77b0c535cd57ff4ed6cd091aec0f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537551"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数
**符合性**  
 版本引入了：ODBC 3.8  
  
 标准符合性：None  
  
 应大多数 ODBC 3.8 （及更高版本） 驱动程序将实现此函数。 如果驱动程序不是，请调用**SQLCancelHandle**具有连接以处理*处理*参数将返回 SQL_ERROR SQLSTATE IM001 和消息驱动程序不支持此函数调用向**SQLCancelHandle**与语句一起处理作为*处理*参数将映射到调用**SQLCancel**由驱动程序管理器，并且如果可以处理该驱动程序实现**SQLCancel**。 应用程序可以使用**SQLGetFunctions**若要确定驱动程序是否支持**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**取消连接或语句的处理。 驱动程序管理器将映射到调用**SQLCancelHandle**的调用**SQLCancel**时*HandleType*为 SQL_HANDLE_STMT。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]Cacel 处理其上的句柄的类型。 有效值为 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [输入]要对其取消处理句柄。  
  
 如果*处理*不是由指定类型的有效句柄*HandleType*， **SQLCancelHandle**返回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCancelHandle**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个语句句柄*处理*或*HandleType* SQL_HANDLE_DBC 和连接句柄*处理*。  
  
 下表列出了通常返回的 SQLSTATE 值**SQLCancelHandle** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)参数中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|以异步方式执行的语句相关的函数调用与相关联的语句句柄之一*处理*，并*HandleType*已设置为 SQL_HANDLE_DBC。 异步函数仍在执行时**SQLCancelHandle**调用。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT; 关联的连接句柄; 上调用异步执行的函数和函数仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*处理*并*HandleType*已设置为 SQL_HANDLE_DBC，并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> **SQLBrowseConnect**曾为调用*ConnectionHandle*，并返回 SQL_NEED_DATA。 在浏览过程完成之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY092|属性/选项标识符无效|*HandleType*已设置为 SQL_HANDLE_ENV 或 SQL_HANDLE_DESC。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*处理*不支持该函数。|  
  
 如果**SQLCancelHandle**使用调用*HandleType*设置为 SQL_HANDLE_STMT，它可以返回任何可由该函数返回的 SQLSTATE **SQLCancel**。  
  
## <a name="comments"></a>注释  
 此函数是类似于**SQLCancel**但可能需要连接或语句句柄作为参数，而不是语句句柄。 驱动程序管理器将映射到调用**SQLCancelHandle**的调用**SQLCancel**时*HandleType*为 SQL_HANDLE_STMT。 这允许应用程序使用**SQLCancelHandle**取消语句的操作，即使该驱动程序不实现**SQLCancelHandle**。  
  
 正在取消语句操作的详细信息，请参阅[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果在没有任何正在进行中的操作*处理*调用**SQLCancelHandle**不起作用。  
  
 **SQLCancelHandle**连接句柄可以取消以下类型的处理：  
  
-   在连接上以异步方式运行的函数。  
  
-   在另一个线程上的连接句柄上运行的函数。  
  
 当**SQLCancelHandle**调用来取消在连接发布者的诊断记录以异步方式运行的函数**SQLCancelHandle**追加到返回的操作正在已取消;**SQLCancelHandle**不返回诊断记录，但是，在取消另一个线程上的连接上运行的函数时。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能使连接处于挂起状态。 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  有关如何使用信息**SQLCancelHandle**中将部署在 Windows 操作系统早于 Windows 7 的应用程序，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>正在取消连接相关的异步处理  
 如果某个函数返回 SQL_STILL_EXECUTING，应用程序可以调用**SQLCancelHandle**取消该操作。 如果成功，取消请求**SQLCancelHandle**返回 SQL_SUCCESS。 这并不意味着，已取消原始函数;它指示已处理取消请求。 驱动程序和数据源确定时，或者将取消该操作。 应用程序必须继续调用原始函数，直到返回代码不是 SQL_STILL_EXECUTING。 如果原始函数已被取消，则返回代码是 SQL_ERROR 并且 SQLSTATE HY008 （已取消的操作）。 如果原始函数完成其正常处理 （未被取消），返回代码是 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 并且以外 HY008 SQLSTATE （已取消的操作），如果原始函数失败。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>正在取消其他线程上执行的函数  
 在多线程应用程序中，应用程序可以取消在另一个线程运行的操作。 若要取消操作，应用程序调用**SQLCancelHandle**与由该函数，而另一个线程上使用句柄。 驱动程序和操作系统确定如何将取消该操作。 **SQLCancelHandle**返回代码指示驱动程序是否处理请求，返回 SQL_SUCCESS 或 SQL_ERROR （未返回任何诊断信息）。 如果在原始函数上的处理已取消，原始函数将返回 SQL_ERROR 并且 SQLSTATE HY008 （已取消的操作）。  
  
 如果一个函数正在执行时**SQLCancelHandle**称为上取消该函数的另一个线程，很可能成功并返回 SQL_SUCCESS，才能取消生效的函数。 调用**SQLCancelHandle**如果在操作完成之前不起作用**SQLCancelHandle**能够取消操作。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|正在取消对语句句柄，取消需要数据，一个语句上的函数或取消的语句，另一个线程上运行的函数以异步方式运行的函数。|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
