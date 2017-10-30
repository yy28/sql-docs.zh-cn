---
title: "核心级别 API 函数 （适用于 Oracle 的 ODBC 驱动程序） |Microsoft 文档"
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
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3bc36063659da3cf0cd6b2b837be0c4fce46c6f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心级别 API 函数 （适用于 Oracle 的 ODBC 驱动程序）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在此级别的函数构成的最低级别的 ODBC 驱动程序接口一致性。  
  
|API 函数|说明|  
|------------------|-----------|  
|**SQLAllocConnect**|连接句柄，分配内存*hdbc*，由标识环境中*henv*。 驱动程序管理器处理此调用，并调用驱动程序的**SQLAllocConnect**每当函数**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**调用。|  
|**SQLAllocEnv**|显示对话框中指定的 Oracle 客户端软件的要求，然后返回 SQL_NULL_HANDLE。 如果未安装 Oracle 客户端软件，此函数会分配的内存环境句柄， *henv*，并使用 ODBC 调用级接口初始化应用程序。|  
|**SQLAllocStmt**|为语句句柄分配内存并将语句句柄与 hdbc 所指定的连接相关联。 驱动程序管理器将传递对驱动程序，为 hstmt 结构分配内存的调用。|  
|**SQLBindCol**|分配的结果列的存储空间，并指定结果的类型。|  
|**SQLCancel**|取消语句句柄，hstmt 上的处理。 在某些情况下，Oracle 不允许取消正在运行的语句。 这意味着正在运行的语句将继续，直到 Oracle 完成此过程中，用于 Oracle 的 ODBC 驱动程序取消这段时间的语句的结果。|  
|**SQLColAttributes**|返回结果集中的列的描述符信息。 描述符信息作为字符串、 32 位依赖于描述符的值或一个整数值返回。|  
|**SQLConnect**|连接到数据源。 若要使用 Oracle 操作系统身份验证，指定"/"作为*szUID*参数和""作为*szAuthStr*参数。|  
|**SQLDescribeCol**|返回名称、 类型、 精度、 小数位数和给定的结果列的为空性。 **注意：****SQLDescribeCol**报告为 SQL_VARCHAR 的计算的列。  |  
|**SQLDisconnect**|关闭连接。 如果共享环境的情况下启用连接池和应用程序调用**SQLDisconnect**在该环境中连接时，该连接返回到连接池，仍可供使用的其他组件相同的共享的环境中。|  
|**SQLError**|返回有关上一个错误的错误或状态信息。 驱动程序保持堆栈或可以为返回的错误的列表*hstmt*， *hdbc*，和*henv*自变量，具体取决于如何在调用**SQLError**进行。 每个语句后刷新错误队列。 通常检索 Oracle 错误消息，否则为空。|  
|**SQLExecDirect**|执行新、 未准备好的 SQL 语句。 如果语句中存在任何参数，驱动程序将使用的参数标记变量的当前值。 如果你的表、 视图或字段名称包含空格，将名称括在返回引号标记。 例如，如果你的数据库包含名为的表*我表*和字段*My Field*，括起标识符的每个元素如下所示：<br /><br /> 选择\`我表\`。 \`我 Field1\`，;\`我表\`。\`我 Field2\` FROM\`我表|  
|**SQLExecute**|执行已准备的 SQL 语句 (已准备的语句**SQLPrepare**)。 如果语句中存在任何参数，驱动程序将使用的参数标记变量的当前值。|  
|**SQLFetch**|从结果集中到由以前的调用的指定的位置检索一行**SQLBindCol**。 准备针对调用该驱动程序**SQLGetData**未绑定列。|  
|**SQLFreeConnect**|释放连接句柄并释放所有内存分配的句柄。|  
|**SQLFreeEnv**|关闭用于 Oracle 的 ODBC 驱动程序并释放与该驱动程序相关联的所有内存。|  
|**SQLFreeStmt**|停止与特定 hstmt 关联的处理、 关闭任何打开的游标与 hstmt 关联、 放弃挂起的结果，和根据需要释放与该语句句柄关联的所有资源。|  
|**SQLGetCursorName**|返回与给定 hstmt 光标的名称。|  
|**SQLNumResultCols**|返回结果集游标中的列数。|  
|**SQLPrepare**|通过规划如何优化并执行语句准备 SQL 语句。 通过执行编译 SQL 语句**SQLExecDirect**。<br /><br /> 如果你的表、 视图或字段名称包含空格，将名称括在返回引号标记。 例如，如果你的数据库包含名为的表*我表*和字段*My Field*，括起标识符的每个元素，如下所示：<br /><br /> 选择\`我表\`。\`我字段\`FROM\`我表<br /><br /> 有关使用包含的正式参数作为数组的结果集的信息，请参阅[从存储过程返回数组参数](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供任何方法来确定的结果集之前提取的最后一行后，因此它将返回 – 1 中的行数。|  
|**SQLSetCursorName**|将游标名称相关联与活动语句句柄， *hstmt*。|  
|**SQLSetParam**|替换为 SQLBindParameter ODBC 2 中。*x*。|  
|**SQLTransact**|请求提交或回滚操作中，为对所有语句句柄 (hstmts) 与连接关联的所有活动操作或与环境句柄，关联的所有连接*henv*。 如果提交失败时在手动模式下，则事务会保持活动状态，则你可以选择回滚事务，或重试提交操作。 如果在自动事务模式下，提交操作失败，事务将自动回滚;事务不能为非活动状态。|

