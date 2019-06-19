---
title: 附录 B：状态转换表 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82c19931073aa96eb045f574e8670068f3d3c659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026923"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附录 B：ODBC 状态转换表
本附录中的表显示如何 ODBC 函数导致的环境、 连接、 语句和描述符状态转换。 环境、 连接、 语句或描述符的状态通常决定了可以使用相应类型的句柄 （环境、 连接、 语句或描述符） 的函数可以调用时。 环境、 连接、 语句和描述符状态重叠大致下图中所示。 例如，连接的确切重叠状态 C5，C6 和语句状态 S1 到 S12 是数据源决定的因为事务在不同时间开始对不同的数据源和描述符状态 D1i （隐式已分配的描述符） 取决于描述符与之关联的语句的状态，状态 D1e （显式已分配的描述符） 时不依赖于状态的任何语句。 每个状态的说明，请参阅[环境转换](../../../odbc/reference/appendixes/environment-transitions.md)，[连接转换](../../../odbc/reference/appendixes/connection-transitions.md)，[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)，和[描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)、 本附录中更高版本。  
  
 环境和连接状态重叠，如下所示：  
  
 ![环境和连接状态重叠](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 连接和语句状态重叠，如下所示：  
  
 ![连接和语句状态重叠](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 语句和描述符状态重叠，如下所示：  
  
 ![语句和描述符状态重叠](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 连接和描述符状态重叠，如下所示：  
  
 ![连接和描述符状态重叠](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 转换表中的每个条目可以是下列值之一：  
  
-   **--** 的执行该函数后保持状态不变。  
  
-   **E**  

     **_n_**  ， **C_n_** ， **S_n_** ，或者**D_n_** -环境、 连接、 语句或描述符状态将更改为指定的状态。  
 
-   **(IH)** -无效的句柄传递给函数。 如果句柄是句柄为空或已有效句柄的类型不正确-例如，连接句柄时传递语句句柄所需-该函数返回 SQL_INVALID_HANDLE;否则，该行为是未定义并可能严重。 仅当其是处于指定状态调用函数的唯一可能的结果时，会显示此错误。 此错误不会更改状态，始终检测由驱动程序管理器中，由括号。  
  
-   **NS** -下一步的状态。 就像通过异步状态不已经过该语句，语句转换都是相同的。 例如，假设创建结果集的语句将由于从 S1 状态进入状态 S11 **SQLExecDirect**返回 SQL_STILL_EXECUTING。 处于状态 S11 NS 表示法表示语句转换的创建结果集的那些状态 S1 中的语句的相同。 如果**SQLExecDirect**返回错误，该语句将保留在 S1 状态; 如果成功，将该语句设置为状态 S5; 如果它需要数据时，将该语句设置为状态 S8; 并且如果仍在执行，它保持状态 S11。  

-   **_XXXXX_** 或 **(*XXXXX*)** -的 SQLSTATE 相关向转换表;检测到由驱动程序管理器的 SQLSTATEs 被括在括号中。 该函数返回 SQL_ERROR 并且指定的 SQLSTATE，但状态不会更改。 例如，如果**SQLExecute**之前，调用**SQLPrepare**，它将返回 SQLSTATE HY010 （函数序列错误）。  

> [!NOTE]  
>  表不会显示与不会更改状态的转换表不相关的错误。 例如，当**SQLAllocHandle**环境状态 E1 中调用，并返回 SQLSTATE HY001 （内存分配错误），环境将保持状态 E1; 的环境转换表中未显示这**SQLAllocHandle**。  
  
 如果环境、 连接、 语句或描述符可以移动到多个状态，显示每个可能的状态和一个或多个脚注解释在其下的每个转换发生的条件。 以下脚注可能出现在任何表。  
  
|脚注|含义|  
|--------------|-------------|  
|b|之前或之后。 游标已定位的结果集或结果集的末尾之后在开始之前。|  
|c|当前函数。 以异步方式执行的当前函数。|  
|d|需要数据。 该函数返回 SQL_NEED_DATA。|  
|e|错误。 该函数返回 SQL_ERROR。|  
|i|无效的行。 游标已定位在结果中的行集和任一行已删除或在该行上操作中发生错误一样。 如果已存在行状态数组，行的行状态数组中的值为 SQL_ROW_DELETED 或 SQL_ROW_ERROR。 （行状态数组是由指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。）|  
|nf|找不到。 该函数返回 sql_no_data 为止。 这不适用于何时**SQLExecDirect**， **SQLExecute**，或**SQLParamData**执行搜索后的返回 SQL_NO_DATA update 或 delete 语句。|  
|np|未准备好。 不被准备的语句。|  
|nr|无结果。 该语句将不会或未创建结果集。|  
|o|其他函数。 以异步方式执行的另一个函数。|  
|p|准备好。 被准备的语句。|  
|r|结果。 该语句将或未创建 （可能为空） 的结果集。|  
|s|成功。 该函数返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|v|有效的行。 游标已定位在结果集中的行和插入的行必须已成功，已成功更新，或在该行上的另一个操作已经成功完成。 如果已存在行状态数组，行的行状态数组中的值是 SQL_ROW_ADDED、 SQL_ROW_SUCCESS 或 SQL_ROW_UPDATED。 （行状态数组是由指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。）|  
|x|正在执行。 该函数返回 SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此示例中，行中的环境状态转换表**SQLFreeHandle**时*HandleType*为 SQL_HANDLE_ENV 如下所示。  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 如果**SQLFreeHandle**调用中环境状态 E0 与*HandleType*设置为 SQL_HANDLE_ENV，驱动程序管理器返回 SQL_INVALID_HANDLE。 如果调用中使用的 E1 状态*HandleType*设置为 SQL_HANDLE_ENV，环境移动，以便状态 E0，如果该函数成功，并保持状态 E1，如果函数失败。 如果调用中使用的 E2 状态*HandleType*设置为 SQL_HANDLE_ENV，驱动程序管理器始终返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误） 和环境保持状态 E2。  
  
 若要了解状态转换表，它是必须了解哪一项 （环境、 连接、 语句或描述符） 它们引用。 假设一个函数接受类型为 X 的项的句柄。该函数的 X 状态转换表介绍了如何调用该函数，与某一项的类型为 X，句柄影响该项目。 例如， **SQLDisconnect**接受连接句柄。 有关的连接状态转换表**SQLDisconnect**介绍了如何**SQLDisconnect**会影响为调用连接的状态。  
  
 假设一个函数接受的句柄类型 Y 的项不等于 X Y。该函数的 X 状态转换表介绍了如何调用函数，使用的类型为 X 与 Y，类型的项相关联的句柄影响类型 Y 的项。例如，语句状态转换表**SQLDisconnect**介绍了如何**SQLDisconnect**影响语句使用与其连接的句柄调用时的状态语句都相关联。  
  
 本附录包含的以下主题。  
  
-   [环境转换](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [连接转换](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [语句转换](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)
