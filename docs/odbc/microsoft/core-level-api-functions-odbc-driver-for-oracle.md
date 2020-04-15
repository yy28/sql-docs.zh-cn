---
title: 核心级 API 功能（Oracle 的 ODBC 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281017"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心级别 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的功能包括 ODBC 驱动程序的最小接口一致性级别。  
  
|API 功能|说明|  
|------------------|-----------|  
|**SQLAlloc连接**|在*henv*标识的环境中为连接句柄*hdbc*分配内存。 驱动程序管理器处理此调用，并在调用**SQLConnect、SQLBrowseConnect**或**SQLConnect****SQLDriverConnect**时调用驱动程序的**SQLAllocConnect**函数。|  
|**SQLAllocEnv**|显示一个对话框，指定 Oracle 客户端软件的要求，然后返回SQL_NULL_HANDLE。 如果未安装 Oracle 客户端软件，此函数将内存分配给环境句柄*henv，* 并初始化 ODBC 调用级接口供应用程序使用。|  
|**SQLAllocStmt**|为语句句柄分配内存，并将语句句柄与 hdbc 指定的连接关联。 驱动程序管理器将此调用传递给驱动程序，驱动程序为 hstmt 结构分配内存。|  
|**SQLBindCol**|为结果列分配存储空间并指定结果的类型。|  
|**SQLCancel**|取消语句句柄上的处理，hstmt。 在某些情况下，Oracle 不允许取消正在运行的语句。 这意味着运行语句将继续，直到 Oracle 完成该过程，此时来自语句的结果将由 Oracle 的 ODBC 驱动程序取消。|  
|**SQLColattributes**|返回结果集中列的描述符信息。 描述符信息将作为字符串、32 位描述符相关值或整数值返回。|  
|**SQLConnect**|连接到数据源。 要使用 Oracle 操作系统身份验证，请指定"/"作为*szUID*参数，"""作为*szAuthStr 参数*。|  
|**SQLDescribeCol**|返回给定结果列的名称、类型、精度、比例和空度。 **注意：SQLDescribeCol**将计算的列报告为SQL_VARCHAR。|  
|**SQL 断开**|关闭连接。 如果为共享环境启用了连接池，并且应用程序在该环境中的连接上调用**SQLDisconnect，** 则连接将返回到连接池，并且仍然可用于使用相同的共享环境的其他组件。|  
|**SQLError**|返回有关上次错误的错误或状态信息。 驱动程序维护一个堆栈或错误列表，这些错误可以返回*用于 hstmt、hdbc*和*henv*参数，具体取决于对**SQLError**的调用方式。 *hdbc* 在每个语句之后刷新错误队列。 通常检索 Oracle 错误消息，否则为空。|  
|**SQLExecDirect**|执行新的、未准备好的 SQL 语句。 如果语句中存在任何参数，驱动程序将使用参数标记变量的当前值。 如果表、视图或字段名称包含空格，请将名称包含在回引号中。 例如，如果数据库包含名为 *"我的表"的表*和字段 *"我的字段"，* 则将标识符的每个元素都包含在内，如下所示：<br /><br /> 选择\`我的表\`。 \`我的字段1，;\`\`我的桌子\`。\`我的字段2\`从我的\`表\`|  
|**SQLExecute**|执行准备好的 SQL 语句（由**SQLPrepare**编写的语句）。 如果语句中存在任何参数，驱动程序将使用参数标记变量的当前值。|  
|**SQLFetch**|从结果集中检索到以前调用**SQLBindCol**指定的位置中的一行。 为调用**SQLGetData**为未绑定列准备驱动程序。|  
|**SQLFreeConnect**|释放连接句柄并释放为该句柄分配的所有内存。|  
|**SQLFreeEnv**|关闭 Oracle 的 ODBC 驱动程序并释放与驱动程序关联的所有内存。|  
|**SQLFreeStmt**|停止与特定 hstmt 关联的处理，关闭与 hstmt 关联的任何打开的游标，丢弃挂起的结果，并可以选择释放与语句句柄关联的所有资源。|  
|**SQLGetCursorName**|返回与给定 hstmt 关联的游标的名称。|  
|**SQLNumResultCols**|返回结果集游标中的列数。|  
|**SQLPrepare**|通过规划如何优化和执行该语句来准备 SQL 语句。 SQL 语句编译供**SQLExecDirect**执行。<br /><br /> 如果表、视图或字段名称包含空格，请将名称包含在回引号中。 例如，如果数据库包含名为 *"我的表*"的表和字段 *"我的字段"，* 则将标识符的每个元素包含如下：<br /><br /> 选择\`我的表\`。\`我的字段\`从我的\`表\`<br /><br /> 有关使用包含数组作为正式参数的结果集的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供一种方法来确定结果集中的行数，直到提取最后一行之后，因此返回 -1。|  
|**SQLSetCursor 名称**|将游标名称与活动语句句柄*hstmt*关联。|  
|**SQLSetParam**|在 ODBC 2 中替换为 SQLBind 参数。*x*. .|  
|**SQLTransact**|请求所有与连接关联的语句句柄 （hstmts） 或与环境句柄关联的所有连接*henv*的所有活动操作的提交或回滚操作。 如果在手动模式下提交失败，则事务将保持活动状态;如果提交处于手动模式下，则事务将保持活动状态。您可以选择回滚事务或重试提交操作。 如果在自动事务模式下提交操作失败，则事务将自动回滚;事务不能处于非活动状态。|
