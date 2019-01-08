---
title: 核心级别 API 函数 （Oracle ODBC 驱动程序） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0ffb78d301762f9b7edcb78a2ba062db6fe662f6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540016"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心级别 API 函数（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在此级别的函数组成的最低级别的 ODBC 驱动程序的接口一致性。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLAllocConnect**|为连接句柄，分配内存*hdbc*，由标识在环境中*henv*。 驱动程序管理器处理此调用，并调用在驱动程序**SQLAllocConnect**函数每当**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**调用。|  
|**SQLAllocEnv**|显示一个对话框，指定的 Oracle 客户端软件的要求，然后返回 SQL_NULL_HANDLE。 如果未安装 Oracle 客户端软件，此函数分配环境句柄，内存*henv*，并初始化应用程序使用的 ODBC 调用级别接口。|  
|**SQLAllocStmt**|为语句句柄分配内存并将语句句柄与 hdbc 所指定的连接相关联。 驱动程序管理器将传递给驱动程序，后者为 hstmt 结构分配内存的此调用。|  
|**SQLBindCol**|分配结果列的存储空间，并指定结果的类型。|  
|**SQLCancel**|取消语句句柄，hstmt 上的处理。 在某些情况下，Oracle 不允许取消的正在运行的语句。 这意味着将继续运行的语句，直到 Oracle 完成的过程时，Oracle ODBC 驱动程序取消这段时间的语句的结果。|  
|**SQLColAttributes**|在结果集中返回列的描述符信息。 描述符信息返回为字符串、 一个 32 位依赖于描述符的值或一个整数值。|  
|**SQLConnect**|连接到数据源。 若要使用 Oracle 操作系统身份验证，请指定"/"作为*szUID*参数和""作为*szAuthStr*参数。|  
|**SQLDescribeCol**|返回名称、 类型、 精度、 小数位数和给定的结果列的为 null 性。 **注意：****SQLDescribeCol**报告为 SQL_VARCHAR 的计算的列。|  
|**SQLDisconnect**|关闭连接。 如果共享环境中启用连接池和应用程序调用**SQLDisconnect**上在该环境中的连接，连接将返回到连接池，并且仍可用于使用其他组件同一个共享的环境中。|  
|**SQLError**|返回有关最后一个错误的错误或状态信息。 驱动程序保持堆栈或可返回的错误的列表*hstmt*， *hdbc*，并*henv*参数，具体取决于如何在调用**SQLError**进行。 每个语句后刷新错误队列。 通常检索 Oracle 错误消息，否则为空。|  
|**SQLExecDirect**|执行新的、 尚未准备好的 SQL 语句。 如果在语句中存在任何参数，驱动程序将使用参数标记变量的当前值。 如果表、 视图或字段名称包含空格，将名称括在返回引号标记。 例如，如果您的数据库包含名为的表*My Table*和字段*My Field*，括起来的标识符的每个元素如下所示：<br /><br /> 选择\`我的表\`。 \`我 Field1\`，;\`我的表\`。\`我 Field2\` FROM\`我的表|  
|**SQLExecute**|执行已准备的 SQL 语句 (已准备的语句**SQLPrepare**)。 如果在语句中存在任何参数，驱动程序将使用参数标记变量的当前值。|  
|**SQLFetch**|从设置到由以前调用的指定的位置的结果中检索一行**SQLBindCol**。 准备驱动程序用于调用**SQLGetData**未绑定列。|  
|**SQLFreeConnect**|释放连接句柄并释放所有内存分配的句柄。|  
|**SQLFreeEnv**|关闭 Oracle ODBC 驱动程序并释放与该驱动程序相关联的所有内存。|  
|**SQLFreeStmt**|与特定 hstmt 关联的处理将停止、 关闭任何打开的游标与 hstmt 关联、 放弃挂起的结果，和 （可选） 释放与语句句柄关联的所有资源。|  
|**SQLGetCursorName**|返回与给定 hstmt 相关联的游标的名称。|  
|**SQLNumResultCols**|在结果集游标中返回列的数。|  
|**SQLPrepare**|通过规划如何优化并执行语句，准备 SQL 语句。 通过执行编译 SQL 语句**SQLExecDirect**。<br /><br /> 如果表、 视图或字段名称包含空格，将名称括在返回引号标记。 例如，如果您的数据库包含名为的表*My Table*和字段*My Field*，括起来的标识符的每个元素，如下所示：<br /><br /> 选择\`我的表\`。\`My Field\` FROM\`我的表<br /><br /> 有关使用结果集包含作为正式参数的数组的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供任何方法来确定的结果集之前提取的最后一行后，因此会返回-1 中的行数。|  
|**SQLSetCursorName**|将游标名称与活动语句句柄，相关联*hstmt*。|  
|**SQLSetParam**|替换为 SQLBindParameter ODBC 2 中的。*x*。|  
|**SQLTransact**|请求提交或回滚操作上的所有语句句柄 (hstmt) 与连接关联的所有活动操作或与环境句柄，关联的所有连接*henv*。 如果提交失败时在手动模式下，事务将保持活动状态;您可以选择回滚事务，或重试提交操作。 如果提交操作失败时在自动事务模式下，事务将自动回滚;事务不能为非活动状态。|
