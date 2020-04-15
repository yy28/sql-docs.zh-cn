---
title: SQLGetCursor 名称函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285545"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetCursorName**返回与指定语句关联的游标名称。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *光标名称*  
 [输出]指向要返回游标名称的缓冲区的指针。  
  
 如果*CursorName 名称*为 NULL，NameLengthPtr 仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*NameLengthPtr**CursorName*指向的缓冲区中返回。  
  
 *缓冲区长度*  
 [输入]\**光标名称*的长度 ，以字符表示。 如果*\*CursorName*中的值是 Unicode 字符串（在调用**SQLGetCursorNameW**时），*则缓冲区长度*参数必须是偶数。  
  
 *名称长度 Ptr*  
 [输出]指向返回在\**CursorName*中返回的字符总数（不包括空终止字符）的内存的指针。 如果可供返回的字符数大于或等于*BufferLength，* 则\**CursorName*中的游标名称将截断为 *"缓冲区长度*"减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetCursorName**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLGetCursorName**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *CursorName*不够大，无法返回整个游标名称，因此游标名称被截断。 未压缩的游标名称的长度在 #*NameLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLGetCursorName**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY015|没有可用的游标名称|（DM） 驱动程序是 ODBC 2 *.x*驱动程序，语句上没有打开的游标，并且没有使用**SQLSetCursorName**设置游标名称。|  
|HY090|无效的字符串或缓冲区长度|（DM） 参数*缓冲区长度*中指定的值小于 0。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 游标名称仅用于定位的更新和删除语句（例如，**更新**_表名_...**其中游**_标名称_的当前 。 有关详细信息，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果应用程序不调用**SQLSetCursorName**来定义游标名称，则驱动程序将生成一个名称。 此名称以字母SQL_CUR开头。  
  
> [!NOTE]
>  在 ODBC 2 *.x*中，当没有打开的游标，并且没有通过调用**SQLSetCursorName**设置名称时，对**SQLGetCursorName 的**调用返回 SQLSTATE HY015（没有可用的游标名称）。 在 ODBC 3 .x 中，这不再正确;在 ODBC 3 *.x*中，这不再正确。无论何时调用**SQLGetCursorName，** 驱动程序都会返回游标名称。  
  
 **SQLGetCursorName**返回游标的名称，无论该名称是显式还是隐式创建。 如果未调用**SQLSetCursorName，** 则隐式生成游标名称。 只要游标处于已分配或准备状态，就可以调用**SQLSetCursorName**在语句上重命名游标。  
  
 显式设置或隐式设置的游标名称将保持设置，直到删除与其关联的*语句句柄*，使用**带有** *SQL_HANDLE_STMT的句柄类型*。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|准备执行语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
