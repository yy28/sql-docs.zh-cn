---
title: ODBC 功能摘要 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10cc7880cf941a1490f963e21e8b44bc91db215
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298918"
---
# <a name="odbc-function-summary"></a>ODBC 函数摘要
下表列出了 ODBC 函数，按任务类型分组，并包括符合性指定和每个函数用途的简要说明。 有关符合性名称的详细信息，请参阅[ODBC 和标准 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)。 有关每个函数的语法和语义的详细信息，请参阅[ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 应用程序可以调用**SQLGetInfo**函数来获取有关驱动程序的一致性信息。 要获取有关驱动程序中特定函数的支持的信息，应用程序可以调用**SQLGet函数**。  
  
|任务|函数名称|一致性|目标|  
|----------|-------------------|-----------------|-------------|  
|连接到数据源|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|获取环境、连接、语句或描述符句柄。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|按数据源名称、用户 ID 和密码连接到特定驱动程序。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|通过连接字符串连接到特定驱动程序，或请求驱动程序管理器和驱动程序显示用户的连接对话框。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|返回连接属性和有效属性值的连续级别。 为每个连接属性指定值后，连接到数据源。|  
|获取有关驱动程序和数据源的信息|[SQLData源](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|返回可用数据源的列表。<br /><br /> 返回已安装驱动程序的列表及其属性。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|返回有关特定驱动程序和数据源的信息。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|返回支持的驱动程序函数。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|返回有关受支持数据类型的信息。|  
|设置和检索驱动程序属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|设置连接属性。<br /><br /> 返回连接属性的值。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|设置环境属性。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|返回环境属性的值。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|设置语句属性。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|返回语句属性的值。|  
|设置和检索描述符字段|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|返回单个描述符字段的值。<br /><br /> 返回多个描述符字段的值。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|设置单个描述符字段。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|设置多个描述符字段。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|将描述符信息从一个描述符句柄复制到另一个描述符句柄。|  
|准备 SQL 请求|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|准备 SQL 语句供以后执行。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|在 SQL 语句中为参数分配存储。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|返回与语句句柄关联的游标名称。|  
||[SQLSetCursor 名称](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|指定游标名称。|  
||[SQLSetScroll 选项](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|设置控制游标行为的选项。|  
|提交请求|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|执行已准备的语句。<br /><br /> 执行语句。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|返回驱动程序翻译的 SQL 语句的文本。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|返回语句中特定参数的说明。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|返回语句中的参数数。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|与**SQLPutData**结合使用，在执行时提供参数数据。 （对于长数据值很有用。|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|发送参数的全部或部分数据值。 （对于长数据值很有用。|  
|检索结果和结果信息|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|返回受插入、更新或删除请求影响的行数。<br /><br /> 返回结果集中的列数。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|描述结果集中的列。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|描述结果集中列的属性。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|为结果列分配存储并指定数据类型。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|返回多个结果行。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|返回可滚动的结果行。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|返回结果集一行的一列的一部分或全部。 （对于长数据值很有用。|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|将游标定位在提取的数据块中，并允许应用程序刷新行集中的数据或更新或删除结果集中的数据。|  
||[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|执行批量插入和批量书签操作，包括按书签更新、删除和提取。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|确定是否有更多可用的结果集，如果是，则初始化下一个结果集的处理。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|返回其他诊断信息（诊断数据结构的单个字段）。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|返回其他诊断信息（诊断数据结构的多个字段）。|  
|获取有关数据源的系统表（目录函数）的信息|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 打开组|返回一个或多个表的列和关联权限的列表。<br /><br /> 返回指定表中的列名称列表。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|返回构成外键的列名称的列表（如果它们存在于指定的表）。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|返回构成表主键的列名称的列表。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|返回输入和输出参数的列表，以及构成指定过程的结果集的列。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|返回存储在特定数据源中的过程名称列表。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|打开组|返回有关唯一标识指定表中的行的最佳列集的信息，或者当事务更新行中的任何值时自动更新的列的信息。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|返回有关单个表的统计信息以及与表关联的索引列表。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|返回表列表以及与每个表关联的权限。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|打开组|返回存储在特定数据源中的表名称的列表。|  
|终止语句|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|结束语句处理，丢弃挂起的结果，并且（可选）释放与语句句柄关联的所有资源。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|关闭已在语句句柄上打开的游标。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|取消对语句的处理。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|取消对语句或连接的处理。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|提交或回滚事务。|  
|终止连接|[SQL 断开](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|关闭连接。<br /><br /> 释放环境、连接、语句或描述符句柄。|
