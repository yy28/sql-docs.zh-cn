---
title: SQLDataSources 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9055fa6c277ebcbeccae909ddd397d39d62cf04
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846055"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函数
**符合性**  
 版本引入了： ODBC 1.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLDataSources**返回有关数据源的信息。 执行此函数仅由驱动程序管理器。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *EnvironmentHandle*  
 [输入]环境句柄。  
  
 *方向*  
 [输入]确定哪些数据源驱动程序管理器将返回有关信息。 可以是：  
  
 SQL_FETCH_NEXT （若要提取列表中的下一个数据源名称）、 SQL_FETCH_FIRST （若要从列表开头提取）、 SQL_FETCH_FIRST_USER （到提取第一个用户 DSN） 或 SQL_FETCH_FIRST_SYSTEM （若要提取的第一个系统 DSN）。  
  
 当*方向*设置为 SQL_FETCH_FIRST 后, 面对**SQLDataSources**与*方向*设置为 SQL_FETCH_NEXT 返回用户和系统 Dsn。 当*方向*设置为 SQL_FETCH_FIRST_USER，对所有后续调用**SQLDataSources**与*方向*设置为 SQL_FETCH_NEXT 返回仅用户 Dsn。 当*方向*设置为 SQL_FETCH_FIRST_SYSTEM，对所有后续调用**SQLDataSources**与*方向*设置为 SQL_FETCH_NEXT 返回仅系统 Dsn。  
  
 *ServerName*  
 [输出]指向用于返回数据源名称的缓冲区。  
  
 如果*ServerName*为 NULL， *NameLength1Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回通过指向的缓冲区中*ServerName*。  
  
 *BufferLength1*  
 [输入]长度 **ServerName*缓冲区，以字符为单位; 这不需要为超过 SQL_MAX_DSN_LENGTH 再加上 null 终止字符。  
  
 *NameLength1Ptr*  
 [输出]指向用于返回的字符 （不包括 null 终止字符） 总数的缓冲区可用于在中返回\* *ServerName*。 可用于返回的字符数是否大于或等于*BufferLength1*中的数据源名称\* *ServerName*截断为*BufferLength1*减去 null 终止字符的长度。  
  
 *说明*  
 [输出]指向用于返回与数据源关联的驱动程序的说明的缓冲区。 例如，dBASE 或 SQL Server。  
  
 如果*描述*为 NULL， *NameLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回通过指向的缓冲区中*说明*。  
  
 *BufferLength2*  
 [输入]以字符为单位的长度 **说明*缓冲区。  
  
 *NameLength2Ptr*  
 [输出]指向用于返回的字符 （不包括 null 终止字符） 总数的缓冲区可用于在中返回\**说明*。 可用于返回的字符数是否大于或等于*BufferLength2*，驱动程序中的描述\**说明*截断为*BufferLength2*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDataSources**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设为 SQL_HANDLE_ENV 和一个*处理*的*EnvironmentHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLDataSources** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|(DM) 特定于驱动程序管理器的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|(DM) 缓冲区\* *ServerName*是否不足够大以返回完整的数据源名称。 因此，名称已被截断。 在中返回整个数据源名称的长度\* *NameLength1Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> (DM) 缓冲区\**说明*是否不足够大以返回完成驱动程序的描述。 因此，说明已被截断。 在返回未截断的数据源说明的长度 **NameLength2Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|(DM) 发生了错误，其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|(DM) 的驱动程序管理器无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*BufferLength1*小于 0。<br /><br /> (DM) 为参数指定的值*BufferLength2*小于 0。|  
|HY103|检索代码无效|(DM) 的参数指定的值*方向*不是等于 SQL_FETCH_FIRST、 SQL_FETCH_FIRST_USER、 SQL_FETCH_FIRST_SYSTEM 或 SQL_FETCH_NEXT。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>注释  
 因为**SQLDataSources**实现在驱动程序管理器中，支持它而不考虑特定驱动程序的标准符合性的所有驱动程序。  
  
 应用程序可以调用**SQLDataSources**多次来检索所有数据源名称。 驱动程序管理器中的系统信息中检索此信息。 如果没有更多的数据源名称，则驱动程序管理器返回 sql_no_data 为止。 如果**SQLDataSources** SQL_FETCH_NEXT 被调用，立即返回 sql_no_data 指示到达后，它将返回第一个数据源名称。 有关如何应用程序使用返回的信息**SQLDataSources**，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果 SQL_FETCH_NEXT 传递给**SQLDataSources**第一次调用时，它将返回第一个数据源名称。  
  
 该驱动程序确定如何将数据源名称映射到实际数据源。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|发现和列出连接到数据源所需值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回驱动程序说明和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
