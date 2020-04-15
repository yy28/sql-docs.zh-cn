---
title: 附录 B：ODBC 状态过渡表 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302881"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附录 B：ODBC 状态转换表
本附录中的表显示了 ODBC 函数如何导致环境、连接、语句和描述符状态的转换。 环境、连接、语句或描述符的状态通常规定何时可以调用使用相应句柄类型的函数（环境、连接、语句或描述符）。 环境、连接、语句和描述符状态大致重叠，如下图所示。 例如，连接状态 C5 和 C6 以及语句的准确重叠状态 S1 到 S12 依赖于数据源，因为事务在不同的数据源上从不同时间开始，并且描述符状态 D1i（隐式分配的描述符）取决于与描述符关联的语句的状态，而状态 D1e（显式分配的描述符）独立于任何语句的状态。 有关每种状态的说明，请参阅本附录后面的[环境转换](../../../odbc/reference/appendixes/environment-transitions.md)、[连接转换](../../../odbc/reference/appendixes/connection-transitions.md)、[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)和[描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)。  
  
 环境和连接状态重叠如下：  
  
 ![环境和连接状态重叠](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 连接和语句状态重叠如下：  
  
 ![连接和语句状态重叠](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 语句和描述符状态重叠如下：  
  
 ![语句和描述符状态重叠](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 连接和描述符状态重叠如下：  
  
 ![连接和描述符状态重叠](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 过渡表中的每个条目可以是以下值之一：  
  
-   **--**-执行函数后状态保持不变。  
  
-   **E**  

     **_n_** n、C_n_、S_n_ 或**D_n_** - 环境、连接、语句或描述符状态移动到指定状态。 **C_n_** **S_n_**  
 
-   **（IH）** - 将无效句柄传递给函数。 如果句柄是空句柄或错误类型的有效句柄（例如，在需要语句句柄时传递连接句柄）函数返回SQL_INVALID_HANDLE;否则，行为是未定义的，可能是致命的。 仅当此错误是以指定状态调用函数的唯一可能结果时，才会显示此错误。 此错误不会更改状态，并且始终由驱动程序管理器检测到，如括号所示。  
  
-   **NS** - 下一个州。 语句转换与语句未通过异步状态相同。 例如，假设创建结果集的语句从状态 S1 进入状态 S11，因为**SQLExecDirect**返回SQL_STILL_EXECUTING。 状态 S11 中的 NS 表示法意味着语句的转换与创建结果集的状态 S1 中的语句的转换相同。 如果 SQLExecDirect 返回错误，则语句将保持状态为 S1;如果**SQLExecDirect**返回错误，则语句将保持在状态 S1 状态。如果成功，语句将移动到状态 S5;如果成功，则语句将移动到"S5"状态。如果需要数据，语句将移动到状态 S8;如果需要数据，则语句将移动到"S8"状态。如果它仍在执行，它将保持在状态 S11。  

-   **_XXXXX_** 或 **（*XXXXX*）** - 与转换表相关的 SQLSTATE;驱动程序管理器检测到的 SQLSTAT 包含在括号中。 函数返回SQL_ERROR和指定的 SQLSTATE，但状态不会更改。 例如，如果在**SQLPrepare**之前调用**SQLExecute，** 它将返回 SQLSTATE HY010（函数序列错误）。  

> [!NOTE]  
>  这些表不显示与不更改状态的过渡表无关的错误。 例如，当**SQLAllocHandle**在环境状态 E1 中调用并返回 SQLSTATE HY001（内存分配错误）时，环境将保持在状态 E1;当 SQLAllocHandle 在环境状态 E1 中调用时，环境将保持在 E1 状态中。这未显示在**SQLAllocHandle**的环境转换表中。  
  
 如果环境、连接、语句或描述符可以移动到多个状态，则显示每个可能的状态，并且一个或多个脚注解释每次转换发生的条件。 以下脚注可能出现在任何表中。  
  
|脚注|含义|  
|--------------|-------------|  
|b|之前或之后。 光标位于结果集开始之前或结果集结束之后。|  
|c|当前函数。 当前函数以异步方式执行。|  
|d|需要数据。 函数返回SQL_NEED_DATA。|  
|e|错误。 函数返回SQL_ERROR。|  
|i|无效行。 光标位于结果集中的一行上，该行已被删除，或者该行的操作中发生错误。 如果存在行状态数组，则该行行状态数组中的值SQL_ROW_DELETED或SQL_ROW_ERROR。 （行状态数组由SQL_ATTR_ROW_STATUS_PTR语句属性指向。|  
|nf|未找到。 函数返回SQL_NO_DATA。 当**SQLExecDirect、SQLExecute****SQLExecute**或**SQLParamData**在执行搜索的更新或删除语句后返回SQL_NO_DATA时，这不适用。|  
|np|未准备好。 声明没有编写。|  
|nr|没有结果。 语句不会或未创建结果集。|  
|o|其他函数。 另一个函数正在异步执行。|  
|p|准备。 声明是编写的。|  
|r|结果。 语句将创建或确实创建一个（可能为空）结果集。|  
|s|成功。 函数返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS。|  
|v|有效行。 光标位于结果集中的一行上，并且该行已成功插入、成功更新，或者该行上的另一个操作已成功完成。 如果存在行状态数组，则该行行状态数组中的值SQL_ROW_ADDED、SQL_ROW_SUCCESS或SQL_ROW_UPDATED。 （行状态数组由SQL_ATTR_ROW_STATUS_PTR语句属性指向。|  
|x|正在执行。 函数返回SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此示例中，当*HandleType* SQL_HANDLE_ENV时 **，SQLFreeHandle**的环境状态转换表中的行如下所示。  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）|E0|（HY010）|  
  
 如果**SQLFreeHandle**在环境状态 E0 中调用，*句柄类型*设置为SQL_HANDLE_ENV，则驱动程序管理器将返回SQL_INVALID_HANDLE。 如果在状态 E1 中调用它，*并且 HandleType*设置为SQL_HANDLE_ENV，则如果函数成功，环境将移动到状态 E0，如果函数失败，则环境将移动到状态 E0，并在函数失败时保持状态 E1。 如果在状态 E2 中调用，*句柄类型*设置为SQL_HANDLE_ENV，则驱动程序管理器始终返回SQL_ERROR和 SQLSTATE HY010（函数序列错误），并且环境保持状态为 E2。  
  
 要了解状态转换表，必须了解它们引用的项（环境、连接、语句或描述符）。 假设函数接受 X 型项的句柄。该函数的 X 状态转换表描述使用类型 X 项的句柄调用函数如何影响该项。 例如 **，SQLDisconnect**接受连接句柄。 **SQLDisconnect**的连接状态转换表描述了**SQLDISCONNECT**如何影响调用它的连接的状态。  
  
 假设函数接受 Y 类型的项的句柄，其中 Y 不等于 X。该函数的 X 状态转换表描述调用函数（具有与 Y 类型的项关联的 X 类型的句柄）如何影响 Y 类型的项。例如 **，SQLDisconnect**的语句状态转换表描述了 SQLDisconnect 与语句关联的连接句柄调用时**SQLDisconnect**如何影响语句的状态。  
  
 本附录包含以下主题。  
  
-   [环境转换](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [连接转换](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [语句转换](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述符转换](../../../odbc/reference/appendixes/descriptor-transitions.md)
