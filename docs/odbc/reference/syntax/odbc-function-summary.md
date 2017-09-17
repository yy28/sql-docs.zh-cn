---
title: "ODBC 函数摘要 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9441a955eaa4a9001b7acd655f7753e32f49e68e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-function-summary"></a>ODBC 函数摘要
下表列出 ODBC 函数，按类型的任务，分组，并包含所指定的一致性和每个函数的用途的简要概述。 有关一致性指定内容的详细信息，请参阅[ODBC 和标准 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)。 有关语法和语义为每个函数的详细信息，请参阅[ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 应用程序可以调用**SQLGetInfo**函数来获取有关驱动程序的一致性信息。 若要获取有关驱动程序中的特定函数支持的信息，请应用程序可以调用**SQLGetFunctions**。  
  
|任务|函数名称|一致性|用途|  
|----------|-------------------|-----------------|-------------|  
|连接到数据源|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|获取一个环境、 连接、 语句或描述符句柄。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|连接到特定的驱动程序的数据源名称、 用户 ID 和密码。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|通过连接字符串或请求的驱动程序管理器和驱动程序显示用户的连接对话框连接到特定的驱动程序。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|返回连接属性和有效的属性值的连续级别。 当已为每个连接属性指定的值时，连接到数据源。|  
|获取有关驱动程序和数据源的信息|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|返回可用数据源的列表。<br /><br /> 返回已安装的驱动程序及其特性的列表。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|返回有关特定的驱动程序和数据源的信息。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|返回受支持的驱动程序函数。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|返回有关受支持的数据类型的信息。|  
|设置和检索驱动程序属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|设置连接属性。<br /><br /> 返回连接属性的值。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|设置环境属性。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|返回环境属性的值。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|设置语句属性。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|返回语句属性的值。|  
|设置和检索描述符字段|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|返回单个描述符字段的值。<br /><br /> 返回多个描述符字段的值。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|设置单个描述符字段。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|设置多个描述符字段。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|将描述符信息从一个描述符句柄复制到另一个。|  
|正在准备 SQL 请求|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|准备供以后执行 SQL 语句。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|将分配中的 SQL 语句的参数的存储。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|返回与语句句柄关联的游标名称。|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|指定游标名称。|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|设置控制的游标行为的选项。|  
|提交请求|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|执行已准备的语句。<br /><br /> 执行语句。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|返回转换由驱动程序的 SQL 语句的文本。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|在语句中返回特定参数的说明。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|在语句中返回参数的数目。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|结合使用**SQLPutData**提供在执行时的参数数据。 （long 数据值很有用。）|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|将发送部分或全部参数的数据值。 （long 数据值很有用。）|  
|检索的结果以及有关结果的信息|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|返回受 insert、 update 或 delete 请求的行数。<br /><br /> 返回结果集中的列数。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|在结果集中的列的说明。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|描述在结果集中的列的特性。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|分配的结果列的存储，并指定的数据类型。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|返回多个结果行。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|返回可滚动的结果行。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|返回部分或全部的结果的一个行的一列设置。 （long 数据值很有用。）|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|定位游标中提取的数据块，并允许应用程序刷新行集中的数据或更新或删除在结果集中的数据。|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|执行大容量插入和大容量书签操作，包括更新、 删除和提取由书签。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|确定是否有多个结果集可用，并如果是这样，初始化下一个结果集的处理。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|返回其他诊断信息 （诊断数据结构的单个字段）。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|返回其他诊断信息 （多个字段的诊断数据结构）。|  
|获取有关数据源的系统表 （目录函数） 的信息|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 打开组|返回列和一个或多个表的关联的权限的列表。<br /><br /> 在指定的表中返回的列名称的列表。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|如果指定的表存在，请返回构成外键的列名称的列表。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|返回构成表的主键的列名称的列表。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|返回输入和输出参数，以及构成的指定过程的结果集的列的列表。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|返回特定数据源中存储的过程名称的列表。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|打开组|返回有关的优化集或由事务更新行中的任何值时将自动更新列的唯一标识中指定表的行的列的信息。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|返回有关单个表和索引与表相关联的列表的统计信息。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|返回表，以及与每个表相关联的权限的列表。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|打开组|返回特定数据源中存储的表名称的列表。|  
|终止语句|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|结束语句处理、 放弃挂起的结果，并 （可选） 释放与该语句句柄关联的所有资源。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|关闭已打开的语句句柄的游标。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|取消语句上的处理。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|取消语句或连接上的处理。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|提交或回滚事务。|  
|终止连接|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|关闭连接。<br /><br /> 释放环境、 连接、 语句或描述符句柄。|
