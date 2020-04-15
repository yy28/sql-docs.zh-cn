---
title: SQLData源函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301177"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLDataSource**返回有关数据源的信息。 此函数仅由驱动程序管理器实现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>参数  
 *环境处理*  
 [输入]环境句柄。  
  
 *方向*  
 [输入]确定驱动程序管理器返回的信息源。 可以是：  
  
 SQL_FETCH_NEXT（获取列表中的下一个数据源名称）、SQL_FETCH_FIRST（从列表开头提取）、SQL_FETCH_FIRST_USER（获取第一个用户 DSN）或SQL_FETCH_FIRST_SYSTEM（获取第一个系统 DSN）。  
  
 当*方向*设置为SQL_FETCH_FIRST时，后续对**SQLDataSources***的调用*设置为SQL_FETCH_NEXT返回用户和系统 DSN。 当*方向*设置为SQL_FETCH_FIRST_USER时，所有后续对**SQLDataSources***的调用*，方向设置为SQL_FETCH_NEXT仅返回用户 DSN。 当*方向*设置为SQL_FETCH_FIRST_SYSTEM时，所有后续对**SQLDataSources**的调用（*方向*设置为SQL_FETCH_NEXT仅返回系统 DSN。  
  
 *ServerName*  
 [输出]指向要返回数据源名称的缓冲区的指针。  
  
 如果*服务器名称*为*NULL，NameLength1Ptr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*服务器名称*指向的缓冲区中返回。  
  
 *缓冲区长度1*  
 [输入]**服务器名称*缓冲区的长度（以字符表示）;这不需要超过SQL_MAX_DSN_LENGTH加上 null 终止字符。  
  
 *名称长度1Ptr*  
 [输出]指向缓冲区的指针，其中返回可在\**ServerName*中返回的字符总数（不包括空终止字符）。 如果可供返回的字符数大于或等于*BufferLength1，* 则\**ServerName*中的数据源名称将截断为*BufferLength1*减去空终止字符的长度。  
  
 *说明*  
 [输出]指向缓冲区的指针，用于返回与数据源关联的驱动程序的说明。 例如，dBASE 或 SQL 服务器。  
  
 如果*描述*为*NULL，NameLength2Ptr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*描述*指向的缓冲区中返回。  
  
 *缓冲区长度2*  
 [输入]**描述*缓冲区的字符的长度。  
  
 *名称 长度2Ptr*  
 [输出]指向缓冲区的指针，其中返回可在\**"描述"* 中返回的字符总数（不包括空终止字符）。 如果可返回的字符数大于或等于*BufferLength2，* 则\**"描述"* 中的驱动程序描述将截断为*BufferLength2*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDataSources**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_ENV*Handle*的*句柄类型*和环境*句柄*句柄。 下表列出了**SQLDataSources**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|（DM） 特定于驱动程序管理器的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|（DM） 缓冲区\**服务器名称*不够大，无法返回完整的数据源名称。 因此，名称被截断。 整个数据源名称的长度在\**NameLength1Ptr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> （DM） 缓冲区\**描述*不够大，无法返回完整的驱动程序说明。 因此，描述被截断。 未压缩的数据源描述的长度在 #*NameLength2Ptr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|（DM） 发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|（DM） 驱动程序管理器无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength1*指定的值小于 0。<br /><br /> （DM） 为参数*BufferLength2*指定的值小于 0。|  
|HY103|无效检索代码|（DM） 为参数*方向*指定的值不等于SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM 或SQL_FETCH_NEXT。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>注释  
 由于**SQLDataSources**是在驱动程序管理器中实现的，因此无论特定驱动程序的标准符合性如何，它都支持所有驱动程序。  
  
 应用程序可以多次调用**SQLDataSource**来检索所有数据源名称。 驱动程序管理器从系统信息中检索此信息。 当不再有数据源名称时，驱动程序管理器将返回SQL_NO_DATA。 如果在**SQLDataSource**返回SQL_NO_DATA后立即用 SQL_FETCH_NEXT 调用它，它将返回第一个数据源名称。 有关应用程序如何使用**SQLDataSource**返回的信息的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果SQL_FETCH_NEXT在第一次调用时传递给**SQLDataSource，** 它将返回第一个数据源名称。  
  
 驱动程序确定数据源名称如何映射到实际数据源。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|发现并列出连接到数据源所需的值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回驱动程序描述和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
