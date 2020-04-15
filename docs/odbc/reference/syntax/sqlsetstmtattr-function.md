---
title: SQLSetStmtAttr 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetStmtAttr
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfbd2144e677d053f6154dfb3a1df1f6c25d9da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287258"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**设置与语句相关的属性。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC *3.x*应用程序使用 ODBC *2.x*驱动程序时的详细信息，请参阅[映射应用程序向后兼容性的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *特性*  
 [输入]选项设置，列在"注释" 中。  
  
 *ValuePtr*  
 [输入]要与*属性*关联的值。 根据*属性*的值 *，ValuePtr*将是以下之一：  
  
-   ODBC 描述符句柄。  
  
-   SQLUINTEGER 值。  
  
-   SQLULEN 值。  
  
-   指向下列之一的指针：  
  
    -   null 终止字符串。  
  
    -   二进制缓冲区。  
  
    -   SQLLEN、SQLULEN 或 SQLUSMALLINT 类型的值或数组。  
  
    -   驱动程序定义的值。  
  
 如果*属性*参数是特定于驱动程序的值 *，ValuePtr*可能是一个签名整数。  
  
 *字符串长度*  
 [输入]如果*属性*是 ODBC 定义的属性 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为\**ValuePtr*的长度。 如果*属性*是 ODBC 定义的属性 *，ValuePtr*是整数，则忽略*字符串长度*。  
  
 如果*属性*是驱动程序定义的属性，则应用程序通过设置*StringLength*参数指示该属性对驱动程序管理器的性质。 *字符串长度*可以具有以下值：  
  
-   如果*ValuePtr*是指向字符串的指针，则*StringLength*是字符串的长度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*StringLength 中*。 这将在*字符串长度*中放置负值。  
  
-   如果*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*StringLength*应具有该值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定长度值，则*StringLength*会根据需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetStmtAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLSetStmtAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持*ValuePtr*中指定的值，或者*ValuePtr*中指定的值由于实现工作条件而无效，因此驱动程序替换了类似的值。 （可以调用**SQLGetStmtAttr**以确定临时替换的值。替换值对*语句处理*有效，直到游标关闭，此时语句属性将还原到其上一个值。 可以更改的语句属性包括：<br /><br /> SQL_ATTR_ROW_ARRAY_SIZE ATTR_MAX_ROWS SQL_ SQL_ ATTR_KEYSET_SIZE ATTR_CURSOR_TYPE ATTR_CONCURRENCY SQL_ SQL_SQL_ATTR_QUERY_TIMEOUTSQL_SQL_SQL_SQL_SQL_SQL_SQL_ATTR_MAX_LENGTHSQL_SQL_SQL_SQL_SQL_SQL_SQL_ATTR_SIMULATE_CURSOR<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|*属性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 或SQL_ATTR_USE_BOOKMARKS，并且光标已打开。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY009|无效使用空指针|*属性*参数标识了需要字符串属性的语句属性 *，ValuePtr*参数为空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLSetStmtAttr**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY011|无法立即设置属性|*属性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR或SQL_ATTR_USE_BOOKMARKS，并编写了该声明。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY017|自动分配的描述符句柄的无效使用|（DM）*属性*参数SQL_ATTR_IMP_ROW_DESC或SQL_ATTR_IMP_PARAM_DESC。<br /><br /> （DM）*属性*参数SQL_ATTR_APP_ROW_DESC或*SQL_ATTR_APP_PARAM_DESC，ValuePtr*中的值是隐式分配的描述符句柄，而不是最初为 ARD 或 APD 分配的句柄。|  
|HY024|无效属性值|给定指定的*属性*值，在*ValuePtr*中指定了无效值。 （驱动程序管理器仅对接受一组离散值（如SQL_ATTR_ACCESS_MODE或SQL_ATTR_ASYNC_ENABLE）的连接和语句属性返回此 SQLSTATE。 对于所有其他连接和语句属性，驱动程序必须验证*ValuePtr*中指定的值 。<br /><br /> *属性*参数SQL_ATTR_APP_ROW_DESC或*SQL_ATTR_APP_PARAM_DESC，ValuePtr*是显式分配的描述符句柄，与*语句句柄*参数的连接不相同。|  
|HY090|无效的字符串或缓冲区长度|（DM） * \*ValuePtr*是一个字符串，*字符串长度*参数小于 0，但不是SQL_NTS。|  
|HY092|无效属性/选项标识符|（DM） 为参数*属性*指定的值对驱动程序支持的 ODBC 版本无效。<br /><br /> （DM） 为参数*属性*指定的值是只读属性。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 语句属性，但驱动程序不支持该属性。<br /><br /> *属性*参数SQL_ATTR_ASYNC_ENABLE，并且对**SQLGetInfo**的调用（带有SQL_ASYNC_MODE*的信息类型*返回SQL_AM_CONNECTION。<br /><br /> *属性*参数SQL_ATTR_ENABLE_AUTO_IPD，连接属性SQL_ATTR_AUTO_IPD的值SQL_FALSE。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|S1118|驱动程序不支持异步通知|如果调用 SQLSetStmtAttr 设置为设置SQL_ATTR_ASYNC_STMT_EVENT;如果调用**SQLSetStmtAttr**以设置SQL_ATTR_ASYNC_STMT_EVENT驱动程序不支持异步通知。|  
  
## <a name="comments"></a>注释  
 语句的语句属性保持有效，直到它们被另一个调用**SQLSetStmtAttr**更改，或者直到通过调用**SQLFreeHandle**删除语句。 使用SQL_CLOSE、SQL_UNBIND或SQL_RESET_PARAMS选项调用**SQLFreeStmt**不会重置语句属性。  
  
 如果数据源不支持*ValuePtr*中指定的值，则某些语句属性支持替换类似的值。 在这种情况下，驱动程序返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02（选项值已更改）。 例如，如果*属性*为*SQL_ATTR_CONCURRENCY，ValuePtr*是SQL_CONCUR_ROWVER，并且数据源不支持此功能，则驱动程序将替换SQL_CONCUR_VALUES并返回SQL_SUCCESS_WITH_INFO。 要确定替换值，应用程序调用**SQLGetStmtAttr**。  
  
 使用*ValuePtr*设置的信息集的格式取决于指定的*属性*。 **SQLSetStmtAttr**以两种不同格式之一接受属性信息：字符串或整数值。 每个格式在属性的说明中注明。 此格式适用于**SQLGetStmtAttr**中每个属性返回的信息。 **SQLSetStmtAttr**的*ValuePtr*参数指向的字符串的长度为*字符串长度*。  
  
> [!NOTE]
>  通过调用**SQLSetConnectAttr**在连接级别设置语句属性的能力已在 ODBC *3.x*中被弃用。 ODBC *3.x*应用程序绝不应在连接级别设置语句属性。 ODBC *3.x*语句属性无法在连接级别设置，SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE属性除外，这些属性既是连接属性，也是语句属性，可以在连接级别或语句级别进行设置。  
> 
> [!NOTE]
>  ODBC *3.x*驱动程序仅需要支持此功能，如果它们应与在连接级别设置 ODBC *2.x*语句选项的 ODBC *2.x*应用程序配合使用。 有关详细信息，请参阅附录 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)下的"在连接级别设置语句选项"：向后兼容性的驱动程序指南。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>设置描述符字段的语句属性  
 许多语句属性对应于描述符的标头字段。 设置这些属性实际上会导致设置描述符字段。 通过调用**SQLSetStmtAttr**而不是**SQLSetDescField**设置字段的优点是，不需要为函数调用获取描述符句柄。  
  
> [!CAUTION]  
>  为一个语句调用**SQLSetStmtAttr**可能会影响其他语句。 当显式分配与语句关联的 APD 或 ARD 并与其他语句关联时，将发生这种情况。 由于**SQLSetStmtAttr**修改 APD 或 ARD，因此修改将应用于与此描述符关联的所有语句。 如果这不是必需的行为，应用程序应在再次调用**SQLStmtAttr**之前将此描述符与其他语句（通过调用**SQLSetStmtAttr**将SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC字段设置为其他描述符句柄）分离。  
  
 当描述符字段设置为正在设置的相应语句属性的结果时，该字段仅针对当前与*语句句柄*参数标识的语句关联的适用描述符设置，并且属性设置不会影响将来可能与该语句关联的任何描述符。 当一个也是语句属性的描述符字段由对**SQLSetDescField**的调用设置时，将设置相应的语句属性。 如果显式分配的描述符与语句分离，则对应于标头字段的语句属性将恢复为隐式分配的描述符中的字段的值。  
  
 分配语句时（请参阅[SQLAllocHandle），](../../../odbc/reference/syntax/sqlallochandle-function.md)四个描述符句柄将自动分配并与语句关联。 显式分配的描述符句柄可以通过调用**SQLAllocHandle**与*SQL_HANDLE_DESCfHandleType*进行关联，以分配描述符句柄，然后调用**SQLSetStmtAttr**将描述符句柄与语句相关联。  
  
 下表中的语句属性对应于描述符标头字段。  
  
|语句属性|标题字段|德克|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|阿尔德|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|阿尔德|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|阿尔德|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|阿尔德|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|税务局|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|税务局|  
  
## <a name="statement-attributes"></a>语句属性  
 当前定义的属性及其引入的 ODBC 版本显示在下表中;预计驱动程序将定义更多属性，以利用不同的数据源。 ODBC 保留一系列属性;驱动程序开发人员必须从 Open Group 为其特定于驱动程序使用保留值。 有关详细信息，请参阅[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|特性|*价值 Ptr*内容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC （ODBC 3.0）|APD 的句柄，用于后续调用语句句柄上的**SQLExecute**和**SQLExecDirect。** 此属性的初始值是最初分配语句时隐式分配的描述符。 如果此属性的值设置为SQL_NULL_DESC或最初为描述符分配的句柄，则以前与语句句柄关联的显式分配的 APD 句柄将与其分离，并且语句句柄将还原到隐式分配的 APD 句柄。<br /><br /> 此属性不能设置为隐式分配给另一个语句或在同一语句上隐式设置的另一个描述符句柄;隐式分配的描述符句柄不能与多个语句或描述符句柄关联。|  
|SQL_ATTR_APP_ROW_DESC （ODBC 3.0）|语句句柄上的 ARD 句柄，用于后续提取。 此属性的初始值是最初分配语句时隐式分配的描述符。 如果此属性的值设置为SQL_NULL_DESC或最初为描述符分配的句柄，则以前与语句句柄关联的显式分配的 ARD 句柄将与其分离，并且语句句柄将还原到隐式分配的 ARD 句柄。<br /><br /> 此属性不能设置为隐式分配给另一个语句或在同一语句上隐式设置的另一个描述符句柄;隐式分配的描述符句柄不能与多个语句或描述符句柄关联。|  
|SQL_ATTR_ASYNC_ENABLE （ODBC 1.0）|SQLULEN 值，用于指定调用的函数是否异步执行：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用语句级别的异步执行支持（默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 启用语句级异步执行支持。<br /><br /> 有关详细信息，请参阅[异步执行（轮询方法）。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)<br /><br /> 对于具有语句级异步执行支持的驱动程序，语句属性SQL_ATTR_ASYNC_ENABLE只读取。 其值与分配语句句柄时具有相同名称的连接级别属性的值相同。<br /><br /> 调用**SQLSetStmtAttr**以在SQL_ASYNC_MODE*信息类型*返回SQL_AM_CONNECTION返回 SQLSTATE HYC00（未实现可选功能）时设置SQL_ATTR_ASYNC_ENABLE。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)了解更多信息。|  
|SQL_ATTR_ASYNC_STMT_EVENT （ODBC 3.8）|作为事件句柄的 SQLPOINTER 值。<br /><br /> 通过调用**SQLSetStmtAttr**来设置**SQL_ATTR_ASYNC_STMT_EVENT**属性并指定事件句柄，从而启用异步函数的完成通知。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK （ODBC 3.8）|异步回调函数的 SQLPOINTER。<br /><br /> 只有驱动程序管理器可以使用此属性调用驱动程序的**SQLSetStmtAttr**函数。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT （ODBC 3.8）|上下文结构的 SQLPOINTER<br /><br /> 只有驱动程序管理器可以使用此属性调用驱动程序的**SQLSetStmtAttr**函数。|  
|SQL_ATTR_CONCURRENCY （ODBC 2.0）|指定游标并发的 SQLULEN 值：<br /><br /> SQL_CONCUR_READ_ONLY = 光标是只读的。 不允许更新。<br /><br /> SQL_CONCUR_LOCK = Cursor 使用尽可能低的锁定级别来确保可以更新行。<br /><br /> SQL_CONCUR_ROWVER = 光标使用乐观并发控制，比较行版本，如 SQLBase ROWID 或 Sybase TIMESTAMP。<br /><br /> SQL_CONCUR_VALUES = 光标使用乐观并发控制，比较值。<br /><br /> SQL_ATTR_CONCURRENCY的默认值为SQL_CONCUR_READ_ONLY。<br /><br /> 无法为打开的游标指定此属性。 有关详细信息，请参阅[并发类型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果SQL_ATTR_CURSOR_TYPE*属性*更改为不支持当前值SQL_ATTR_CONCURRENCY的类型，则在执行时将更改SQL_ATTR_CONCURRENCY值，并在调用**SQLExecDirect**或**SQLPrepare**时发出警告。<br /><br /> 如果驱动程序支持**选择更新**语句，并且在将SQL_ATTR_CONCURRENCY的值设置为SQL_CONCUR_READ_ONLY时执行此类语句，则将返回错误。 如果SQL_ATTR_CONCURRENCY的值更改为驱动程序支持的值，该值为 SQL_ATTR_CURSOR_TYPE，而不是当前值 SQL_ATTR_CURSOR_TYPE，则在执行时将更改SQL_ATTR_CURSOR_TYPE值，并在调用**SQLExecDirect**或**SQLPrepare**时发出 SQLSTATE 01S02（选项值已更改）的值。<br /><br /> 如果数据源不支持指定的并发，驱动程序将替换不同的并发并发并返回 SQLSTATE 01S02（选项值已更改）。 对于SQL_CONCUR_VALUES，驱动程序替换SQL_CONCUR_ROWVER，反之亦然。 对于SQL_CONCUR_LOCK，驾驶员按顺序替换SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 直到执行时间，才会检查替换值的有效性。<br /><br /> 有关SQL_ATTR_CONCURRENCY与其他游标属性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE （ODBC 3.0）|指定应用程序所需的支持级别的 SQLULEN 值。 设置此属性会影响对**SQLExecDirect**和**SQLExecute 的**后续调用。<br /><br /> SQL_NONSCROLLABLE = 语句句柄不需要可滚动游标。 如果应用程序在此句柄上调用**SQLFetchScroll，** 则*提取方向*的唯一有效值SQL_FETCH_NEXT。 这是默认值。<br /><br /> SQL_SCROLLABLE = 语句句柄上需要可滚动的游标。 调用**SQLFetchScroll**时，应用程序可以指定任何有效的*Fetch 方向*值，从而在顺序模式以外的模式中实现光标定位。<br /><br /> 有关可滚动游标的详细信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关SQL_ATTR_CURSOR_SCROLLABLE与其他游标属性之间的关系的详细信息，请参阅[光标特征和光标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY （ODBC 3.0）|SQLULEN 值，用于指定语句句柄上的游标是否使另一个游标对结果集所做的更改可见。 设置此属性会影响对**SQLExecDirect**和**SQLExecute 的**后续调用。 应用程序可以读取此属性的值，以获取应用程序最近设置的初始状态或其状态。<br /><br /> SQL_UNSPECIFIED = 未指定游标类型，以及语句句柄上的游标是否使另一个游标对结果集所做的更改可见。 语句句柄上的光标可能使任何、某些或所有此类更改都变得可见。 这是默认值。<br /><br /> SQL_INSENSITIVE = 语句句柄上的所有游标都显示结果集，而不反映任何其他游标对它所做的任何更改。 不敏感的游标是只读的。 这对应于静态游标，该静态游标具有只读的并发。<br /><br /> SQL_SENSITIVE = 语句句柄上的所有游标都使另一个游标对结果集所做的所有更改都可见。<br /><br /> 有关SQL_ATTR_CURSOR_SENSITIVITY与其他游标属性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE （ODBC 2.0）|指定游标类型的 SQLULEN 值：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 光标仅向前滚动。<br /><br /> SQL_CURSOR_STATIC = 结果集中的数据是静态的。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 驱动程序保存并使用键SQL_ATTR_KEYSET_SIZE语句属性中指定的行数。<br /><br /> SQL_CURSOR_DYNAMIC = 驱动程序仅保存和使用行集中行的键。<br /><br /> 默认值为SQL_CURSOR_FORWARD_ONLY。 在准备 SQL 语句后，无法指定此属性。<br /><br /> 如果数据源不支持指定的游标类型，驱动程序将替换不同的游标类型并返回 SQLSTATE 01S02（选项值已更改）。 对于混合或动态游标，驱动程序按顺序替换按键集驱动的或静态游标。 对于键集驱动的游标，驱动程序将替换静态游标。<br /><br /> 有关可滚动光标类型的详细信息，请参阅[可滚动光标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 有关SQL_ATTR_CURSOR_TYPE与其他游标属性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD （ODBC 3.0）|指定是否执行 IPD 的自动填充的 SQLULEN 值：<br /><br /> SQL_TRUE = 调用**SQLPrepare**后打开 IPD 的自动填充。 SQL_FALSE = 调用**SQLPrepare**后关闭 IPD 的自动填充。 （如果支持，应用程序仍可以通过调用**SQLDescribeParam**来获取 IPD 字段信息。语句属性SQL_ATTR_ENABLE_AUTO_IPD的默认值为SQL_FALSE。 有关详细信息，请参阅[IPD 的自动填充](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR （ODBC 3.0）|指向二进制\*书签值的 SQLLEN。 当**SQLFetchScroll**调用*fFetch 方向*等于SQL_FETCH_BOOKMARK时，驱动程序将从此字段拾取书签值。 此字段默认为空指针。 有关详细信息，请参阅[按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 此字段指向的值不用于按书签删除、按书签更新或按**SQLBulk 操作**中的书签操作提取，该操作使用在行集缓冲区中缓存的书签。|  
|SQL_ATTR_IMP_PARAM_DESC （ODBC 3.0）|IPD 的句柄。 此属性的值是最初分配语句时分配的描述符。 应用程序无法设置此属性。<br /><br /> 此属性可以通过对**SQLGetStmtAttr**的调用检索，但不能通过调用**SQLSetStmtAttr**来设置。|  
|SQL_ATTR_IMP_ROW_DESC （ODBC 3.0）|IRD 的句柄。 此属性的值是最初分配语句时分配的描述符。 应用程序无法设置此属性。<br /><br /> 此属性可以通过对**SQLGetStmtAttr**的调用检索，但不能通过调用**SQLSetStmtAttr**来设置。|  
|SQL_ATTR_KEYSET_SIZE （ODBC 2.0）|一个 SQLULEN，用于指定键集驱动的游标的键集中的行数。 如果键集大小为 0（默认值），则光标为完全键集驱动。 如果键集大小大于 0，则游标是混合的（键集中内键集驱动，键集外部的动态）。 默认键集大小为 0。 有关键集驱动的游标的详细信息，请参阅[键集驱动的游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定大小超过最大键集大小，驱动程序将替换该大小并返回 SQLSTATE 01S02（选项值已更改）。<br /><br /> 如果键集大小大于 0 且小于行集大小 **，SQLFetch** **或 SQLFetchScroll**将返回错误。|  
|SQL_ATTR_MAX_LENGTH （ODBC 1.0）|SQLULEN 值，用于指定驱动程序从字符或二进制列返回的最大数据量。 如果*ValuePtr*小于可用数据的长度 **，SQLFetch**或**SQLGetData**会截取数据并返回SQL_SUCCESS。 如果*ValuePtr*为 0（默认值），驱动程序将尝试返回所有可用数据。<br /><br /> 如果指定的长度小于数据源可以返回的最小数据量或大于数据源可以返回的最大数据量，驱动程序将替换该值并返回 SQLSTATE 01S02（选项值已更改）。<br /><br /> 此属性的值可以在打开的游标上设置;也可以在打开的游标上设置此属性的值。但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02（选项值已更改）并将属性重置为其原始值。<br /><br /> 此属性旨在减少网络流量，并且仅当多层驱动程序中的数据源（而不是驱动程序）可以实现时，才应支持此属性。 应用程序不应使用此机制来截截数据;因此，应用程序不应使用此机制来截截数据。为了截断接收的数据，应用程序应在**SQLBindCol**或**SQLGetData**中的*缓冲区长度*参数中指定最大缓冲区长度。|  
|SQL_ATTR_MAX_ROWS （ODBC 1.0）|与要返回到**SELECT**语句的应用程序的最大行数对应的 SQLULEN 值。 如果\* *ValuePtr*等于 0（默认值），则驱动程序将返回所有行。<br /><br /> 此属性旨在减少网络流量。 从概念上讲，在创建结果集时应用它，并将结果集限制为第一个*ValuePtr*行。 如果结果集中的行数大于*ValuePtr，* 则结果集将被截断。<br /><br /> SQL_ATTR_MAX_ROWS应用于*语句*上的所有结果集，包括目录函数返回的结果集。 SQL_ATTR_MAX_ROWS为游标行计数的值建立最大值。<br /><br /> 如果驱动程序不能保证SQL_ATTR_MAX_ROWS将正确实现，则驱动程序不应模拟**SQLFetch**或**SQLFetchScroll** SQL_ATTR_MAX_ROWS行为（如果无法在数据源中实现结果集大小限制）。<br /><br /> 它是驱动程序定义的SQL_ATTR_MAX_ROWS是否适用于 SELECT 语句以外的语句（如目录函数）。<br /><br /> 此属性的值可以在打开的游标上设置;也可以在打开的游标上设置此属性的值。但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02（选项值已更改）并将属性重置为其原始值。|  
|SQL_ATTR_METADATA_ID （ODBC 3.0）|SQLULEN 值，用于确定如何处理目录函数的字符串参数。<br /><br /> 如果SQL_TRUE，目录函数的字符串参数将被视为标识符。 情况并不严重。 对于非分隔字符串，驱动程序删除任何尾随空格，并将字符串折叠到大写。 对于分隔字符串，驱动程序删除任何前导或尾随空格，并从字面上获取分隔符之间的任何内容。 如果这些参数之一设置为空指针，则函数将返回SQL_ERROR和 SQLSTATE HY009（无效使用空指针）。<br /><br /> 如果SQL_FALSE，目录函数的字符串参数不被视为标识符。 案件意义重大。 它们可以包含字符串搜索模式，也可以不包含字符串搜索模式，具体取决于参数。<br /><br /> 默认值为SQL_FALSE。<br /><br /> **SQLTables**的*表类型*参数 （它采用值列表） 不受此属性的影响。<br /><br /> 也可以在连接级别设置SQL_ATTR_METADATA_ID。 （它和SQL_ATTR_ASYNC_ENABLE是唯一也是连接属性的语句属性。<br /><br /> 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN （ODBC 1.0）|SQLULEN 值，指示驱动程序是否应扫描 SQL 字符串的转义序列：<br /><br /> SQL_NOSCAN_OFF = 驱动程序扫描 SQL 字符串以搜索转义序列（默认值）。<br /><br /> SQL_NOSCAN_ON = 驱动程序不扫描 SQL 字符串的转义序列。 相反，驱动程序将语句直接发送到数据源。<br /><br /> 有关详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR （ODBC 3.0）|SQLULEN = 值，指向添加到用于更改动态参数绑定的指针的偏移量。 如果此字段为非空，则驱动程序将引用指针，将已引用的值添加到描述符记录中的每个延迟字段（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR），并在绑定时使用新的指针值。 默认情况下，它设置为 null。<br /><br /> 绑定偏移量始终直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR字段。 如果偏移更改为其他值，则新值仍直接添加到描述符字段中的值。 新偏移量不会添加到字段值加上任何较早的偏移量中。<br /><br /> 有关详细信息，请参阅[参数绑定偏移量](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 设置语句属性将设置 APD 标头中的SQL_DESC_BIND_OFFSET_PTR字段。|  
|SQL_ATTR_PARAM_BIND_TYPE （ODBC 3.0）|一个 SQLULEN 值，指示要用于动态参数的绑定方向。<br /><br /> 此字段设置为SQL_PARAM_BIND_BY_COLUMN（默认值）以选择按列方向绑定。<br /><br /> 要选择按行绑定，此字段设置为将绑定到一组动态参数的结构或缓冲区实例的长度。 此长度必须包括所有绑定参数的空间以及结构或缓冲区的任何填充，以确保当绑定参数的地址以指定长度递增时，结果将指向下一组参数中同一参数的开头。 在 ANSI C 中使用*大小*运算符时，此行为得到保证。<br /><br /> 有关详细信息，请参阅[参数的绑定数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 设置此语句属性将设置 aPD 标头中SQL_DESC_BIND_TYPE字段。|  
|SQL_ATTR_PARAM_OPERATION_PTR （ODBC 3.0）|指向 SQLUSMALLINT 值的 SQLUSMALLINT\*值，用于在执行 SQL 语句期间忽略参数的 SQLUSMALLINT 值数组。 每个值设置为SQL_PARAM_PROCEED（要执行的参数）或SQL_PARAM_IGNORE（要忽略的参数）。<br /><br /> 在处理过程中，通过将 APD 中的SQL_DESC_ARRAY_STATUS_PTR指向的数组中的状态值设置为SQL_PARAM_IGNORE，可以忽略一组参数。 如果一组参数的状态值设置为SQL_PARAM_PROCEED或数组中未设置任何元素，则处理其状态值。<br /><br /> 此语句属性可以设置为空指针，在这种情况下，驱动程序不返回参数状态值。 可以随时设置此属性，但直到下次调用**SQLExecDirect**或**SQLExecute**时才会使用新值。<br /><br /> 如果没有绑定参数，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用参数数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 设置语句属性将设置 APD 标头中SQL_DESC_ARRAY_STATUS_PTR字段。|  
|SQL_ATTR_PARAM_STATUS_PTR （ODBC 3.0）|SQLUSMALLINT\*值，该值指向 SQLUSMALLINT 值数组，该值包含对 SQLExecute 或**SQLExecDirect** **SQLExecDirect**调用后每行参数值的状态信息。 仅当PARAMSET_SIZE大于 1 时，才需要此字段。<br /><br /> 状态值可以包含以下值：<br /><br /> SQL_PARAM_SUCCESS：已成功为这组参数执行 SQL 语句。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO：已成功为这组参数执行 SQL 语句;但是，诊断数据结构中提供了警告信息。<br /><br /> SQL_PARAM_ERROR：处理这组参数时出错。 诊断数据结构中提供了其他错误信息。<br /><br /> SQL_PARAM_UNUSED：此参数集未使用，可能是因为以前的一些参数集导致错误中止了进一步处理，或者因为SQL_PARAM_IGNORE为SQL_ATTR_PARAM_OPERATION_PTR指定的数组中该参数集设置了。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE：驱动程序将参数数组视为单片单元，因此不会生成此级别的错误信息。<br /><br /> 此语句属性可以设置为空指针，在这种情况下，驱动程序不返回参数状态值。 可以随时设置此属性，但直到下次调用**SQLExecute**或**SQLExecDirect**时才会使用新值。 请注意，设置此属性可能会影响驱动程序实现的输出参数行为。<br /><br /> 有关详细信息，请参阅[使用参数数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 设置此语句属性将设置 IPD 标头中SQL_DESC_ARRAY_STATUS_PTR字段。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR （ODBC 3.0）|指向缓冲区的\*SQLULEN 记录字段，用于返回已处理的参数集数，包括错误集。 如果这是空指针，则不会返回任何数字。<br /><br /> 设置此语句属性将设置 IPD 标头中的SQL_DESC_ROWS_PROCESSED_PTR字段。<br /><br /> 如果对**SQLExecDirect**或**SQLExecute**的调用填充此属性指向的缓冲区未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容未定义。<br /><br /> 有关详细信息，请参阅[使用参数数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE （ODBC 3.0）|指定每个参数的值数的 SQLULEN 值。 如果SQL_ATTR_PARAMSET_SIZE大于 APD 指向数组的 1、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR。 每个数组的基数等于此字段的值。<br /><br /> 如果没有绑定参数，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用参数数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 设置语句属性将设置 APD 标头中的SQL_DESC_ARRAY_SIZE字段。|  
|SQL_ATTR_QUERY_TIMEOUT （ODBC 1.0）|SQLULEN 值对应于等待 SQL 语句执行后返回到应用程序的秒数。 如果*ValuePtr*等于 0（默认值），则没有超时。<br /><br /> 如果指定的超时超过数据源中的最大超时或小于最小超时 **，SQLSetStmtAttr**将替换该值并返回 SQLSTATE 01S02（选项值已更改）。<br /><br /> 请注意，如果**SELECT**语句超时，应用程序无需调用**SQLCloseCursor**来重用该语句。<br /><br /> 此语句属性中的查询超时设置在同步和异步模式下都有效。|  
|SQL_ATTR_RETRIEVE_DATA （ODBC 2.0）|SQLULEN 值：<br /><br /> SQL_RD_ON = **SQLFetchScroll，** 在 ODBC *3.x*中 **，SQLFetch**在将光标定位到指定位置后检索数据。 这是默认值。<br /><br /> SQL_RD_OFF = **SQLFetchScroll，** 在 ODBC *3.x*中 **，SQLFetch**在定位光标后不会检索数据。<br /><br /> 通过将SQL_RETRIEVE_DATA设置为SQL_RD_OFF，应用程序可以验证行是否存在或检索行的书签，而不会产生检索行的开销。 有关详细信息，请参阅[滚动和提取行](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 此属性的值可以在打开的游标上设置;也可以在打开的游标上设置此属性的值。但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02（选项值已更改）并将属性重置为其原始值。|  
|SQL_ATTR_ROW_ARRAY_SIZE （ODBC 3.0）|SQLULEN 值，用于指定每次调用**SQLFetch**或**SQLFetchScroll**返回的行数。 这也是**SQLBulk 操作**中批量书签操作中使用的书签数组中的行数。 默认值为 1。<br /><br /> 如果指定的行集大小超过数据源支持的最大行集大小，驱动程序将替换该值并返回 SQLSTATE 01S02（选项值已更改）。<br /><br /> 有关详细信息，请参阅[行集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 设置语句属性将设置 ARD 标头中SQL_DESC_ARRAY_SIZE字段。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR （ODBC 3.0）|SQLULEN = 值，指向添加到指针以更改列数据绑定的偏移量。 如果此字段为非空，则驱动程序将引用指针，将已引用的值添加到描述符记录中的每个延迟字段（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR），并在绑定时使用新的指针值。 默认情况下，它设置为 null。<br /><br /> 设置语句属性将设置 ARD 标头中SQL_DESC_BIND_OFFSET_PTR字段。|  
|SQL_ATTR_ROW_BIND_TYPE （ODBC 1.0）|SQLULEN 值，用于设置在关联语句上调用**SQLFetch**或**SQLFetchScroll**时要使用的绑定方向。 通过将值设置为SQL_BIND_BY_COLUMN来选择按列绑定。 通过将值设置为将结果列绑定到的缓冲区或缓冲区实例的长度来选择行绑定。<br /><br /> 如果指定了长度，它必须包含所有绑定列的空间以及结构或缓冲区的任何填充，以确保当绑定列的地址以指定长度递增时，结果将指向下一行中同一列的开头。 在 ANSI C 中使用具有结构或联合**的大小**运算符时，此行为得到保证。<br /><br /> 列绑定是**SQLFetch**和**SQLFetchScroll**的默认绑定方向。<br /><br /> 有关详细信息，请参阅[绑定列以与块游标一起使用](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 设置语句属性将设置 SQL_DESC_BIND_TYPE 字段在 ARD 标头中。|  
|SQL_ATTR_ROW_NUMBER （ODBC 2.0）|SQLULEN 值，它是整个结果集中的当前行的编号。 如果无法确定当前行的数量或没有当前行，则驱动程序返回 0。<br /><br /> 此属性可以通过对**SQLGetStmtAttr**的调用检索，但不能通过调用**SQLSetStmtAttr**来设置。|  
|SQL_ATTR_ROW_OPERATION_PTR （ODBC 3.0）|指向 SQLUSMALLINT\*值的值，用于使用**SQLSetPos**在批量操作期间忽略行的 SQLUSMALLINT 值数组。 每个值设置为SQL_ROW_PROCEED（用于在批量操作中包含行）或SQL_ROW_IGNORE（将行从批量操作中排除）。 （在调用**SQLBulk 操作**期间使用此数组不能忽略行。<br /><br /> 此语句属性可以设置为空指针，在这种情况下，驱动程序不会返回行状态值。 可以随时设置此属性，但直到下次调用**SQLSetPos**时才会使用新值。<br /><br /> 有关详细信息，请参阅使用[SQLSetPos 更新行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)，以及[使用 SQLSetPos 在行集中删除行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 设置此语句属性将设置 ARD 中SQL_DESC_ARRAY_STATUS_PTR字段。|  
|SQL_ATTR_ROW_STATUS_PTR （ODBC 3.0）|指向 SQLFetch 或\* **SQLFetchScroll**调用后包含行状态值的 SQLUSMALLINT 值数组的 SQLUSMALLINT 值的值。 **SQLFetch** 数组具有与行集中的行一样多的元素。<br /><br /> 此语句属性可以设置为空指针，在这种情况下，驱动程序不会返回行状态值。 此属性可以随时设置，但新值在下次调用**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos**之前不会使用。 **SQLFetchScroll**<br /><br /> 有关详细信息，请参阅[已提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 设置语句属性将设置 IRD 标头中SQL_DESC_ARRAY_STATUS_PTR字段。<br /><br /> 此属性由 ODBC *2.x*驱动程序映射到对**SQL 扩展获取**调用中的*rgbRowStatus*数组。|  
|SQL_ATTR_ROWS_FETCHED_PTR （ODBC 3.0）|指向一个缓冲区\*的 SQLULEN 值，该缓冲区用于返回调用**SQLFetch**或**SQLFetchScroll**后获取的行数;受调用**SQLSetPos**执行的批量操作影响的行数，*操作*参数为 SQL_REFRESH;或受**SQLBulk 操作**执行的批量操作影响的行数。 此数字包括错误行。<br /><br /> 有关详细信息，请参阅[已提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 设置语句属性将设置 IRD 标头中SQL_DESC_ROWS_PROCESSED_PTR字段。<br /><br /> 如果对**SQLFetch**或**SQLFetchScroll**的调用填充此属性指向的缓冲区未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容未定义。|  
|SQL_ATTR_SIMULATE_CURSOR （ODBC 2.0）|SQLULEN 值，用于指定模拟定位更新和删除语句的驱动程序是否保证此类语句仅影响一行。<br /><br /> 要模拟定位的更新和删除语句，大多数驱动程序都会构造搜索**的更新**或**DELETE**语句，其中包含一个**WHERE**子句，该子句指定当前行中每列的值。 除非这些列构成唯一的键，否则此类语句可能会影响多个行。<br /><br /> 为了保证此类语句仅影响一行，驱动程序确定唯一键中的列并将这些列添加到结果集中。 如果应用程序保证结果集中的列构成唯一的键，则不需要驱动程序这样做。 这可能会缩短执行时间。<br /><br /> SQL_SC_NON_UNIQUE = 驱动程序不保证模拟定位更新或删除语句仅影响一行;因此，驱动程序不保证将只影响一行。这是应用程序的责任这样做。 如果语句影响多个行 **，SQLExecute、SQLExecDirect**或**SQLSetPos**将返回 SQLSTATE 01001（游标操作冲突）。 **SQLExecDirect**<br /><br /> SQL_SC_TRY_UNIQUE = 驱动程序尝试保证模拟定位更新或删除语句仅影响一行。 驱动程序始终执行此类语句，即使它们可能会影响多个行，例如没有唯一键时。 如果语句影响多个行 **，SQLExecute、SQLExecDirect**或**SQLSetPos**将返回 SQLSTATE 01001（游标操作冲突）。 **SQLExecDirect**<br /><br /> SQL_SC_UNIQUE = 驱动程序保证模拟定位更新或删除语句仅影响一行。 如果驱动程序无法保证给定语句的此参数 **，SQLExecDirect**或**SQLPrepare**将返回错误。<br /><br /> 如果数据源为定位更新和删除语句提供本机 SQL 支持，并且驱动程序不模拟游标，则当请求SQL_SIMULATE_CURSORSQL_SC_UNIQUE时，将返回SQL_SUCCESS。 如果请求SQL_SC_TRY_UNIQUE或SQL_SC_NON_UNIQUE，则返回SQL_SUCCESS_WITH_INFO。 如果数据源提供SQL_SC_TRY_UNIQUE级别的支持，而驱动程序不提供，则返回SQL_SUCCESSSQL_SC_TRY_UNIQUE，并为SQL_SC_NON_UNIQUE返回SQL_SUCCESS_WITH_INFO。<br /><br /> 如果数据源不支持指定的游标模拟类型，驱动程序将替换不同的模拟类型并返回 SQLSTATE 01S02（选项值已更改）。 对于SQL_SC_UNIQUE，驾驶员按顺序替换SQL_SC_TRY_UNIQUE或SQL_SC_NON_UNIQUE。 对于SQL_SC_TRY_UNIQUE，驾驶员将替换SQL_SC_NON_UNIQUE。<br /><br /> 默认值为SQL_SC_UNIQUE。<br /><br /> 有关详细信息，请参阅[模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS （ODBC 2.0）|SQLULEN 值，用于指定应用程序是否使用带有光标的书签：<br /><br /> SQL_UB_OFF = 关闭（默认值）<br /><br /> SQL_UB_VARIABLE = 应用程序将使用带有光标的书签，如果支持，驱动程序将提供可变长度书签。 SQL_UB_FIXED在 ODBC *3.x*中弃用。 ODBC *3.x*应用程序应始终使用可变长度书签，即使使用 ODBC *2.x*驱动程序（仅支持 4 字节、固定长度书签）。 这是因为固定长度书签只是可变长度书签的特殊情况。 使用 ODBC *2.x*驱动程序时，驱动程序管理器将SQL_UB_VARIABLE映射到SQL_UB_FIXED。<br /><br /> 要将书签与游标一起使用，应用程序必须在打开游标之前使用SQL_UB_VARIABLE值指定此属性。<br /><br /> 有关详细信息，请参阅[检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [1] 仅当描述符是实现描述符而不是应用程序描述符时，才能异步调用这些函数。  
  
 请参阅[列-Wise 绑定](../../../odbc/reference/develop-app/column-wise-binding.md)和[行-Wise 绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置描述符的单个字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
