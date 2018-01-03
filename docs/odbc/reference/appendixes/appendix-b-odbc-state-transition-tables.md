---
title: "附录 b: ODBC 状态转换表 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2dabd364fb0a7415a4cf05035d06f5a1dd5838e5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附录 b: ODBC 状态转换表
本附录中的表显示如何 ODBC 函数导致的环境、 连接、 语句和描述符状态的转换。 通常，环境、 连接、 语句或描述符的状态决定使用句柄 （环境、 连接、 语句或描述符） 的相应类型的函数可以调用时。 环境、 连接、 语句中，和描述符状态重叠大致如下图中所示。 例如，连接的确切重叠状态 C5，C6 并且语句说明了通过 S12 S1 是数据源而定，因为在不同的数据源，在不同时间开始事务，描述符状态 D1i （隐式已分配的描述符） 依赖描述符与之关联的语句的状态，在状态 D1e （显式已分配的描述符） 时不依赖于状态的任何语句。 有关每个状态的说明，请参阅[环境转换](../../../odbc/reference/appendixes/environment-transitions.md)，[连接转换](../../../odbc/reference/appendixes/connection-transitions.md)，[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)，和[描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)、 本附录内容更高版本。  
  
 环境和连接状态重叠，如下所示：  
  
 ![环境和连接状态重叠](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 连接和语句状态重叠，如下所示：  
  
 ![连接和语句状态重叠](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 语句和描述符状态重叠，如下所示：  
  
 ![语句和描述符状态重叠](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 连接和描述符状态重叠，如下所示：  
  
 ![连接和描述符状态重叠](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 转换表中的每个条目可以是以下值之一：  
  
-   **--**-状态执行函数后保持不变。  
  
-   **E**  
     ***n*** **C*n***，  **S*n***，或**D*n** *-环境、 连接、 语句或描述符状态将更改为指定的状态。  
  
-   **(IH)** -向函数传递了无效的句柄。 如果句柄是句柄为空或已错误类型的有效句柄 — 例如，传递了语句句柄时所需的连接句柄，该函数将返回 SQL_INVALID_HANDLE;否则，该行为是未定义和可能严重。 仅当它是调用该函数中指定的状态的唯一可能的结果时，会显示此错误。 此错误不会更改状态，并由括号始终检测到的驱动程序管理器中。  
  
-   **NS** -下一个状态。 就像该语句必须不经历的异步状态，语句转换都是相同的。 例如，假设创建结果集的语句在因为从状态 S1 进入状态 S11 **SQLExecDirect**返回 SQL_STILL_EXECUTING。 处于状态 S11 NS 表示法意味着语句转换为相同状态 S1 中的语句来创建结果集。 如果**SQLExecDirect**会返回一个错误，该语句保留在 S1 状态; 如果成功，该语句将移动以状态 S5; 如果它需要数据时，该语句将移动以状态 S8; 并且如果仍在执行，它仍然处于状态 S11。  
  
-   ***XXXXX***或 **(*XXXXX*) * *-向转换表; 相关的 SQLSTATE检测到的驱动程序管理器的 SQLSTATEs 将括在括号中。 该函数返回 SQL_ERROR 和指定的 SQLSTATE，但状态不会更改。 例如，如果**SQLExecute**之前调用**SQLPrepare**，它将返回 SQLSTATE HY010 （函数序列错误）。  
  
> [!NOTE]  
>  表不显示且不与不更改的状态转换表相关的错误。 例如，当**SQLAllocHandle**在环境状态 E1 中调用，并返回 SQLSTATE HY001 （内存分配错误），环境将保持状态 E1; 的环境转换表中未显示这一点**SQLAllocHandle**。  
  
 如果环境、 连接、 语句或描述符可以将移动到多个状态，显示每个可能的状态，并且一个或多个脚注解释在其下每个转换发生的条件。 以下脚注可能出现在任何表。  
  
|脚注|含义|  
|--------------|-------------|  
|b|之前或之后。 早于开始日期的结果集或结果集的末尾之后已定位光标。|  
|c|当前函数。 当前函数在以异步方式执行。|  
|d|需要数据。 该函数返回 SQL_NEED_DATA。|  
|e|错误。 该函数返回 SQL_ERROR。|  
|i|无效的行。 光标在结果中的行组和任一行具有已删除或在该行上操作中出现错误。 如果已存在的行状态数组，行的行状态数组中的值将为 SQL_ROW_DELETED 或 SQL_ROW_ERROR。 （行状态数组被指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。）|  
|nf|找不到。 该函数返回 SQL_NO_DATA。 这不适用于时**SQLExecDirect**， **SQLExecute**，或**SQLParamData**返回 SQL_NO_DATA 后执行搜索更新或删除语句。|  
|np|未准备好。 不准备该语句。|  
|nr|任何结果。 该语句将不会或未创建结果集。|  
|o|其他函数。 以异步方式执行的另一个函数。|  
|p|准备。 已准备该语句。|  
|r|结果。 此语句将或未创建 （可能为空） 的结果集。|  
|s|成功。 该函数返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|v|有效的行。 光标定位在结果集中的行和插入的行具有已成功，已成功更新，或在该行上的另一个操作已经成功完成。 如果已存在的行状态数组，行的行状态数组中的值将为 SQL_ROW_ADDED、 SQL_ROW_SUCCESS 或 SQL_ROW_UPDATED。 （行状态数组被指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。）|  
|x|正在执行。 该函数返回 SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此示例中，环境状态转换中的行表**SQLFreeHandle**时*HandleType*是 SQL_HANDLE_ENV，如下所示。  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 如果**SQLFreeHandle**环境作出响应 E0 中称为*HandleType*设置为 SQL_HANDLE_ENV，驱动程序管理器返回 SQL_INVALID_HANDLE。 如果调用中使用的 E1 状态*HandleType*设置为 SQL_HANDLE_ENV，环境移动，以便状态 E0，如果该函数成功，并保留在状态 E1，如果函数失败。 如果调用中使用的 E2 状态*HandleType*设置为 SQL_HANDLE_ENV，驱动程序管理器始终返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误），并且，环境保持状态 E2。  
  
 若要了解状态转换表，它有必要了解它们到引用的哪一项 （环境、 连接、 语句或描述符）。 假设函数接受一个类型 X 的项的句柄。该函数的 X 状态转换表介绍了如何调用该函数，与某一项的类型为 X，句柄影响该项目。 例如， **SQLDisconnect**接受连接句柄。 有关的连接状态转换表**SQLDisconnect**描述如何**SQLDisconnect**影响为调用连接的状态。  
  
 假设函数接受的句柄类型 Y 的项不等于 X Y。该函数的 X 状态转换表介绍对影响的方式调用具有与类型 Y 的项关联的类型为 X 的句柄的函数类型 Y 的项。例如，语句状态转换表的**SQLDisconnect**描述如何**SQLDisconnect**影响语句时使用与其连接的句柄调用的状态语句是关联。  
  
 本附录包含以下主题。  
  
-   [环境转换](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [连接转换](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [语句转换](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)
