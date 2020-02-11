---
title: 核心级 API 函数（Oracle ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc95ec17dc221cb77bd94fc3378af483aeee92dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081972"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心级别 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 此级别的功能包含 ODBC 驱动程序的最小接口一致性级别。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLAllocConnect**|为*henv*标识的环境中的连接句柄*hdbc*分配内存。 每当调用**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**时，驱动程序管理器就会处理此调用并调用驱动程序的**SQLAllocConnect**函数。|  
|**SQLAllocEnv**|显示一个对话框，该对话框指定 Oracle 客户端软件的要求，然后返回 SQL_NULL_HANDLE。 如果未安装 Oracle 客户端软件，则此函数将为环境句柄*henv*分配内存，并初始化 ODBC 调用级别接口以供应用程序使用。|  
|**SQLAllocStmt**|为语句句柄分配内存，并将语句句柄与 hdbc 指定的连接关联。 驱动程序管理器将此调用传递给驱动程序，后者为 hstmt 结构分配内存。|  
|**SQLBindCol**|为结果列分配存储空间，并指定结果的类型。|  
|**SQLCancel**|取消对语句句柄 hstmt 的处理。 在某些情况下，Oracle 不允许取消正在运行的语句。 这意味着正在运行的语句将继续执行，直到 Oracle 完成该过程，此时由 ODBC Driver for Oracle 取消语句的结果。|  
|**SQLColAttributes**|返回结果集中列的描述符信息。 说明符信息以字符串、32位说明符相关值或整数值的形式返回。|  
|**SQLConnect**|连接到数据源。 若要使用 Oracle 操作系统身份验证，请将 "/" 指定为*szUID*参数，将 "" 指定为*szAuthStr*参数。|  
|**SQLDescribeCol**|返回给定结果列的名称、类型、精度、小数位数和可为 null 性。 **注意： SQLDescribeCol**报告计算列 SQL_VARCHAR。|  
|**SQLDisconnect**|关闭连接。 如果为共享环境启用了连接池，并且应用程序对该环境中的连接调用**SQLDisconnect** ，则连接将返回到连接池，并且仍可用于使用相同共享环境的其他组件。|  
|**SQLError**|返回有关上一个错误的错误或状态信息。 驱动程序将维护一个堆栈或可为*hstmt*、 *hdbc*和*henv*参数返回的错误列表，具体取决于对**SQLError**的调用的方式。 在每个语句后刷新错误队列。 通常检索 Oracle 错误消息，否则为空。|  
|**SQLExecDirect**|执行不准备的新 SQL 语句。 如果语句中存在任何参数，则驱动程序将使用参数标记变量的当前值。 如果表、视图或字段的名称包含空格，则用引号将名称括起来。 例如，如果您的数据库中包含一个名为 *"我的表*" 和 "*我*的字段" 字段，则将标识符的每个元素括起来，如下所示：<br /><br /> 选择\`"我\`的表"。 \`我的\`Field1，;\`我的\`表。\`我的\`表\`中的 Field2\`|  
|**SQLExecute**|执行已准备的 SQL 语句（已由**SQLPrepare**准备的语句）。 如果语句中存在任何参数，则驱动程序将使用参数标记变量的当前值。|  
|**SQLFetch**|从结果集中检索一行，并将其放入之前对**SQLBindCol**的调用指定的位置。 准备驱动程序，以便为未绑定的列调用**SQLGetData** 。|  
|**SQLFreeConnect**|释放连接句柄，释放分配给该句柄的所有内存。|  
|**SQLFreeEnv**|关闭 Oracle 的 ODBC 驱动程序并释放与该驱动程序关联的所有内存。|  
|**SQLFreeStmt**|停止与特定 hstmt 关联的处理，关闭与 hstmt 关联的任何打开的游标，放弃挂起的结果，并选择性地释放与该语句句柄关联的所有资源。|  
|**SQLGetCursorName**|返回与给定 hstmt 关联的游标的名称。|  
|**SQLNumResultCols**|返回结果集游标中的列数。|  
|**SQLPrepare**|通过计划如何优化和执行语句来准备 SQL 语句。 为执行**SQLExecDirect**编译 SQL 语句。<br /><br /> 如果表、视图或字段的名称包含空格，则用引号将名称括起来。 例如，如果您的数据库包含名为 *"我的表*" 和 "*我*的字段" 字段的表，则将标识符的每个元素括起来，如下所示：<br /><br /> 选择\`"我\`的表"。\`我的\`表\`中的字段\`<br /><br /> 有关使用包含数组作为形参的结果集的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|在提取最后一行后，Oracle 不提供确定结果集中的行数的方法，因此返回-1。|  
|**SQLSetCursorName**|将游标名称与活动语句句柄*hstmt*关联。|  
|**SQLSetParam**|替换为 ODBC 2 中的 SQLBindParameter。*x*。|  
|**SQLTransact**|对于与连接关联的所有语句句柄（hstmt）或与环境句柄*henv*关联的所有连接，请求提交或回滚操作。 如果在手动模式下提交失败，则事务将保持活动状态;您可以选择回滚事务或重试提交操作。 如果在自动事务模式下提交操作失败，则将自动回滚事务;该事务不能处于非活动状态。|
