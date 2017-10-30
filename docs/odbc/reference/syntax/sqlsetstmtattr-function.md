---
title: "SQLSetStmtAttr 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d652d9e028cb9eb8edd2ec2865449a4b379c4c64
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**设置与语句相关的属性。  
  
> [!NOTE]  
>  有关什么驱动程序管理器时，将映射此函数可对 ODBC 3*.x*应用程序使用 ODBC 2*.x*驱动程序，请参阅[映射用于向后的替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *Attribute*  
 [输入]若要设置的选项列在"注释"。  
  
 *ValuePtr*  
 [输入]要与关联值*属性*。 根据值*属性*， *ValuePtr*将为以下之一：  
  
-   ODBC 的描述符句柄。  
  
-   一个 SQLUINTEGER 值。  
  
-   一个 SQLULEN 值。  
  
-   指向以下项之一：  
  
    -   以 null 结尾的字符串。  
  
    -   二进制缓冲区中。  
  
    -   值或 SQLLEN、 SQLULEN 或 SQLUSMALLINT 的类型数组。  
  
    -   驱动程序定义的值。  
  
 如果*属性*自变量是特定于驱动程序的值， *ValuePtr*可能是一个带符号的整数。  
  
 *StringLength*  
 [输入]如果*属性*是 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度\* *ValuePtr*. 如果*属性*是 ODBC 定义的属性和*ValuePtr*是一个整数， *StringLength*将被忽略。  
  
 如果*属性*是驱动程序定义的属性，应用程序通过设置指示属性到驱动程序管理器的性质*StringLength*自变量。 *StringLength*可以具有下列值：  
  
-   如果*ValuePtr*然后是指向字符串， *StringLength*是字符串或 sql_nts 以的长度。  
  
-   如果*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定长度的值，然后*StringLength*为 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，与相应。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetStmtAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetStmtAttr**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|该驱动程序不支持在指定的值*ValuePtr*，或在指定的值*ValuePtr*无效由于实现工作条件，因此驱动程序替换类似的值。 (**SQLGetStmtAttr**可以调用以确定暂时被替换的值。)替换值可用于*StatementHandle*直到游标关闭，此时语句属性将恢复为以前的值。 可以更改这些语句属性包括：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|*属性*SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 或 SQL_ATTR_USE_BOOKMARKS，并且光标处于打开状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY009|不允许使用 null 指针|*属性*自变量标识所需的字符串属性，一个语句属性和*ValuePtr*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLSetStmtAttr**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY011|现在无法设置属性|*属性*已 SQL_ATTR_CONCURRENCY、 SQL_ ATTR_CURSOR_TYPE、 SQL_ ATTR_SIMULATE_CURSOR 或 SQL_ ATTR_USE_BOOKMARKS 和语句已准备就绪。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY017|使用自动分配的描述符句柄无效|(DM)*属性*参数为 SQL_ATTR_IMP_ROW_DESC 或 SQL_ATTR_IMP_PARAM_DESC。<br /><br /> (DM)*属性*自变量为 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 和中的值*ValuePtr*最初以外句柄的隐式分配的描述符句柄分配给 ARD 或 APD。|  
|HY024|无效属性值|给出指定*属性*中值，指定无效的值是*ValuePtr*。 （驱动程序管理器返回仅适用于连接和语句属性接受一组离散的值，如 SQL_ATTR_ACCESS_MODE 或 SQL_ ATTR_ASYNC_ENABLE 此 SQLSTATE。 对于所有其他连接和语句属性，该驱动程序必须验证中指定的值*ValuePtr*。)<br /><br /> *属性*参数为 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，和*ValuePtr*已为同一连接不是一个显式分配的描述符句柄*StatementHandle*自变量。|  
|HY090|字符串或缓冲区长度无效|(DM) * \*ValuePtr*是一个字符串，与*StringLength*自变量为小于 0，但未 sql_nts 以。|  
|HY092|属性/选项标识符无效|(DM) 值的参数的指定*属性*对 ODBC 驱动程序支持的版本无效。<br /><br /> (DM) 值的参数的指定*属性*只读属性。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*属性*的 ODBC 版本所支持的驱动程序，但不支持驱动程序是有效的 ODBC 语句属性。<br /><br /> *属性*自变量为 SQL_ATTR_ASYNC_ENABLE，并调用**SQLGetInfo**与*信息类型*SQL_ASYNC_MODE 返回 SQL_AM_CONNECTION。<br /><br /> *属性*参数 SQL_ATTR_ENABLE_AUTO_IPD，且连接属性 SQL_ATTR_AUTO_IPD 的值为 SQL_FALSE。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|S1118|驱动程序不支持异步通知|如果调用**SQLSetStmtAttr**设置 SQL_ATTR_ASYNC_STMT_EVENT; 驱动程序不支持异步通知。|  
  
## <a name="comments"></a>注释  
 之前已被另一个调用更改为语句的语句属性保持有效**SQLSetStmtAttr**或直到语句删除通过调用**SQLFreeHandle**。 调用**SQLFreeStmt** SQL_CLOSE、 SQL_UNBIND，或 SQL_RESET_PARAMS 选项不重置语句属性。  
  
 某些语句特性支持类似的值替换，如果数据源不支持在指定的值*ValuePtr*。 在这种情况下，该驱动程序返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （选项值已更改）。 例如，如果*属性*是 SQL_ATTR_CONCURRENCY 和*ValuePtr* SQL_CONCUR_ROWVER，以及如果数据源不支持这，驱动程序替换 SQL_CONCUR_VALUES 返回 SQL_SUCCESS_WITH_INFO。 若要确定被替换的值，应用程序调用**SQLGetStmtAttr**。  
  
 信息的格式设置*ValuePtr*取决于指定*属性*。 **SQLSetStmtAttr**接受特性信息的两个不同的格式之一： 字符串或整数值。 每个格式将其记录在该特性的说明。 此格式适用于为每个属性中返回的信息**SQLGetStmtAttr**。 字符字符串的指向*ValuePtr*参数**SQLSetStmtAttr**具有长度为*StringLength*。  
  
> [!NOTE]  
>  能够在连接级别设置语句特性，通过调用**SQLSetConnectAttr** ODBC 3 中已弃用*.x*。 ODBC 3*.x*应用应永远不会将语句属性设置在连接级别。 ODBC 3*.x*语句属性不能在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句特性，可以设置在连接级别或语句级上设置。  
  
> [!NOTE]  
>  ODBC 3*.x*驱动程序仅需要支持此功能，如果它们应使用 ODBC 2*.x*应用程序将 ODBC 2 设置*.x*在连接级别的语句选项。 详细信息，请参阅"设置语句选项在连接级别"下[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>设置描述符字段的语句属性  
 许多语句特性对应于描述符标头字段。 将这些特性实际结果设置描述符字段的设置。 通过调用设置字段**SQLSetStmtAttr**而不是为**SQLSetDescField**不需要获得的函数调用的描述符句柄的优势。  
  
> [!CAUTION]  
>  调用**SQLSetStmtAttr**为一条语句可能会影响其他语句。 APD 或与语句关联的 ARD 显式分配，并且也是与其他语句相关联，将发生这种情况。 因为**SQLSetStmtAttr**修改 APD 或 ARD，修改将应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联的其他语句此描述符 (通过调用**SQLSetStmtAttr** SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 字段设置为另一种描述符句柄） 之前调用**SQLSetStmtAttr**试。  
  
 当描述符字段设置由于相应语句特性设置时，只能为都由标识的语句与当前关联的适用描述符设置字段*StatementHandle*自变量，以及属性设置不会影响任何可能与该语句在将来的描述符。 当通过调用设置也是一个语句的属性的描述符字段**SQLSetDescField**，设置了相应的语句属性。 如果显式分配的描述符从语句取消关联，对应于标头字段的语句特性将恢复为隐式分配的描述符中的字段的值。  
  
 当分配一个语句 (请参阅[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md))，四个描述符句柄将自动分配并与该语句相关联。 显式分配的描述符句柄可以通过调用与该语句相关联**SQLAllocHandle**与*fHandleType*的 SQL_HANDLE_DESC 分配的描述符句柄并调用**SQLSetStmtAttr**要语句相关联的描述符句柄。  
  
 下表中的语句属性对应于描述符标头字段。  
  
|语句属性|标头字段|Desc。|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|ARD|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|ARD|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|ARD|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|ARD|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>语句属性  
 下表中; 中显示当前定义的特性和引入这些 ODBC 的版本预期结果是，将由驱动程序以利用不同数据源中定义更多属性。 ODBC; 保留一组属性驱动程序开发人员必须保留用于 Open Group 自己特定于驱动程序使用的值。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|Attribute|*ValuePtr*内容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|句柄，以便后续调用 APD **SQLExecute**和**SQLExecDirect**语句句柄上。 此属性的初始值是在最初分配语句时隐式分配的描述符。 如果此属性的值设置为 SQL_NULL_DESC 或最初分配的描述符句柄，以前语句句柄有关联的显式分配的 APD 句柄从它取消关联，并且语句句柄将恢复为隐式分配 APD 句柄。<br /><br /> 此属性不能设置到已为另一个语句隐式分配的描述符句柄或另一个的描述符句柄上的相同的语句; 隐式设置隐式分配的描述符句柄不能与多个语句或的描述符句柄关联。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|语句句柄上的后续提取 ARD 句柄。 此属性的初始值是在最初分配语句时隐式分配的描述符。 如果此属性的值设置为 SQL_NULL_DESC 或最初分配的描述符句柄，以前语句句柄有关联的显式分配的 ARD 句柄从它取消关联，并且语句句柄将恢复为隐式分配 ARD 句柄。<br /><br /> 此属性不能设置到已为另一个语句隐式分配的描述符句柄或另一个的描述符句柄上的相同的语句; 隐式设置隐式分配的描述符句柄不能与多个语句或的描述符句柄关联。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|SQLULEN 值，该值指定是否以异步方式执行使用指定的语句时调用的函数：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用语句级的异步执行支持 （默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 启用语句级的异步执行支持。<br /><br /> 有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> 对于具有语句级的异步执行支持的驱动程序，该语句属性 SQL_ATTR_ASYNC_ENABLE 为只读。 其值将位于语句句柄已分配的时间与具有相同名称的连接级别属性的值相同。<br /><br /> 调用**SQLSetStmtAttr**设置 SQL_ATTR_ASYNC_ENABLE 时 SQL_ASYNC_MODE*信息类型*返回 SQL_AM_CONNECTION 返回 SQLSTATE HYC00 （未实现的可选功能）。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)有关详细信息。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|SQLPOINTER 值，一个事件句柄。<br /><br /> 异步函数完成通知的启用通过调用**SQLSetStmtAttr**设置**SQL_ATTR_ASYNC_STMT_EVENT**属性，并指定事件句柄。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|对异步回调函数 SQLPOINTER。<br /><br /> 仅驱动程序管理器可以调用驾**SQLSetStmtAttr**使用此特性的函数。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|上下文结构 SQLPOINTER<br /><br /> 仅驱动程序管理器可以调用驾**SQLSetStmtAttr**使用此特性的函数。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|指定游标并发 SQLULEN 值：<br /><br /> SQL_CONCUR_READ_ONLY = 游标是只读的。 不允许任何更新。<br /><br /> SQL_CONCUR_LOCK = 光标使用锁定不足以确保可以更新的行的最低级别。<br /><br /> SQL_CONCUR_ROWVER = 光标使用乐观并发控制，比较如 SQLBase ROWID 或 Sybase 时间戳的行版本。<br /><br /> SQL_CONCUR_VALUES = 光标使用乐观并发控制，对值进行比较。<br /><br /> SQL_ATTR_CONCURRENCY 的默认值是 SQL_CONCUR_READ_ONLY。<br /><br /> 对于打开的游标不能指定此属性。 有关详细信息，请参阅[并发类型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果 SQL_ATTR_CURSOR_TYPE*属性*更改为不支持 SQL_ATTR_CONCURRENCY 的当前值的类型，SQL_ATTR_CONCURRENCY 的值将更改在执行时，和时发出警告**SQLExecDirect**或**SQLPrepare**调用。<br /><br /> 如果驱动程序支持**选择 FOR UPDATE** SQL_ATTR_CONCURRENCY 的值设置为 SQL_CONCUR_READ_ONLY 执行语句，此类语句，就将返回一个错误。 如果 SQL_ATTR_CONCURRENCY 的值更改为一个值，则驱动程序支持 SQL_ATTR_CURSOR_TYPE 某些值而非 SQL_ATTR_CURSOR_TYPE 的当前值，将在执行时间和 SQLSTATE 01s02 的警告更改 SQL_ATTR_CURSOR_TYPE 的值（选项值已更改） 时发出**SQLExecDirect**或**SQLPrepare**调用。<br /><br /> 如果数据源不支持指定的并发，驱动程序替代另一个并发，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。 对于 SQL_CONCUR_VALUES，驱动程序将替换为 SQL_CONCUR_ROWVER，反之亦然。 对于 SQL_CONCUR_LOCK，驱动程序将替换为，按顺序，SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES。 执行时间之前不检查被替换的值的有效性。<br /><br /> 有关 SQL_ATTR_CONCURRENCY 和其他游标特性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|指定的应用程序所需的支持级别 SQLULEN 值。 设置此属性将影响后续调用**SQLExecDirect**和**SQLExecute**。<br /><br /> SQL_NONSCROLLABLE = 可滚动游标不需要语句句柄。 如果应用程序调用**SQLFetchScroll**此句柄，唯一有效的值上*FetchOrientation*是 SQL_FETCH_NEXT。 这是默认设置。<br /><br /> SQL_SCROLLABLE = 可滚动游标，需要在该语句句柄上。 在调用时**SQLFetchScroll**，则应用程序可能指定的任何有效的值*FetchOrientation*，实现光标定位在非顺序模式的模式下。<br /><br /> 有关可滚动游标的详细信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关 SQL_ATTR_CURSOR_SCROLLABLE 和其他游标特性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|指定游标语句句柄上的使可见 SQLULEN 值向结果所做的更改设置的另一个游标。 设置此属性将影响后续调用**SQLExecDirect**和**SQLExecute**。 若要获取其初始状态或其状态为最最近此属性的值由应用程序设置，应用程序可以重新读取。<br /><br /> SQL_UNSPECIFIED = 它未指定游标类型是什么，是否语句句柄上的游标进行对结果集的另一个游标所做的更改。 语句句柄上的游标可能使可见 none、 几个或所有此类更改。 这是默认设置。<br /><br /> SQL_INSENSITIVE = 所有游标语句句柄显示结果集不反映对其进行任何更改的情况下上由任何其他游标。 不敏感游标是只读的。 这对应于静态游标，它具有是只读的并发。<br /><br /> SQL_SENSITIVE = 所有游标语句句柄让上可见的另一个游标通过设置到结果所做的所有更改。<br /><br /> 有关 SQL_ATTR_CURSOR_SENSITIVITY 和其他游标特性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|SQLULEN 值，该值指定游标类型：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 向前滚动游标唯一。<br /><br /> SQL_CURSOR_STATIC = 数据在结果集是静态。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 该驱动程序保存和密钥用于 SQL_ATTR_KEYSET_SIZE 语句属性中指定的行数。<br /><br /> SQL_CURSOR_DYNAMIC = 该驱动程序保存和只有密钥用于在行集中的行。<br /><br /> 默认值为 SQL_CURSOR_FORWARD_ONLY。 准备好的 SQL 语句之后，不能指定此属性。<br /><br /> 如果数据源不支持指定的游标类型，该驱动程序替代其他游标类型，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。 对于混合或动态游标，该驱动程序替换，按顺序，键集驱动的或静态游标。 对于键集驱动游标，该驱动程序替换静态游标。<br /><br /> 有关可滚动游标类型的详细信息，请参阅[可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 有关 SQL_ATTR_CURSOR_TYPE 和其他游标特性之间的关系的详细信息，请参阅[光标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|指定是否执行自动填充的 IPD SQLULEN 值：<br /><br /> SQL_TRUE 表示打开的 IPD 后调用的自动填充**SQLPrepare**。 SQL_FALSE 表示自动填充的 IPD 调用后关闭**SQLPrepare**。 (应用程序仍可以通过调用获取 IPD 字段信息**SQLDescribeParam**，如果支持。)语句属性 SQL_ATTR_ENABLE_AUTO_IPD 的默认值是 SQL_FALSE。 有关详细信息，请参阅[自动填充的 IPD](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|SQLLEN\*指向二进制书签值。 当**SQLFetchScroll**使用调用*fFetchOrientation*等于 SQL_FETCH_BOOKMARK，驱动程序将拾取此域中的书签值。 此字段默认为 null 指针。 有关详细信息，请参阅[按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 指向此字段的值不用于书签删除、 更新的书签的地方，或提取书签中的操作**SQLBulkOperations**，其中使用缓存在行集缓冲区中的书签。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD 句柄。 此属性的值是在最初分配语句时分配的描述符。 应用程序无法设置此属性。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未通过调用设置**SQLSetStmtAttr**。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD 句柄。 此属性的值是在最初分配语句时分配的描述符。 应用程序无法设置此属性。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未通过调用设置**SQLSetStmtAttr**。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|对于键集驱动游标键集中指定的行数 SQLULEN。 如果键集大小为 0 （默认值），则游标是完全键集驱动。 如果键集大小大于 0，则游标被混合 （键集驱动内键集和动态外键集）。 默认键集大小为 0。 有关键集驱动游标的详细信息，请参阅[Keyset-Driven 游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定的大小超过最大键集大小，该驱动程序替代该大小，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。<br /><br /> **SQLFetch**或**SQLFetchScroll**返回错误，如果键集大小大于 0 且小于行集大小。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|一个 SQLULEN 值，指定最大的驱动程序返回字符或二进制列中的数据量。 如果*ValuePtr*是否可用的数据的长度小于**SQLFetch**或**SQLGetData**将截断数据，并返回 SQL_SUCCESS。 如果*ValuePtr*为 0 （默认值），该驱动程序尝试返回所有可用的数据。<br /><br /> 如果指定的长度的最小的数据源可以返回的数据量小于或大于最大的数据量可以返回的数据源，驱动程序替换值并返回 SQLSTATE 01s02 的警告 （选项值已更改）。<br /><br /> 可以在打开的游标; 上设置此属性的值但是，该设置可能不会立即生效，在这种情况下该驱动程序将返回 SQLSTATE 01s02 的警告 （选项值已更改） 和将该属性重置为其原始值。<br /><br /> 此属性旨在减少网络流量，所以应仅在数据源 （而不是驱动程序） 在多个层驱动程序可以实现它时支持。 此机制不应由应用程序截断数据;若要减少接收数据，应用程序应指定的最大的缓冲区长度以*BufferLength*中的参数**SQLBindCol**或**SQLGetData**。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|要返回的应用程序进行的行的最大次数对应 SQLULEN 值**选择**语句。 如果\* *ValuePtr*等于 0 （默认值），则该驱动程序将返回所有行。<br /><br /> 此属性被为了减少网络流量。 当结果集中创建第一个的结果集限制的应用从概念上讲， *ValuePtr*行。 如果结果集中的行数大于*ValuePtr*，结果集将被截断。<br /><br /> SQL_ATTR_MAX_ROWS 适用于所有结果集上*语句*，包括那些由目录函数。 SQL_ATTR_MAX_ROWS 建立光标行计数的值的最大。<br /><br /> 驱动程序不应模拟 SQL_ATTR_MAX_ROWS 行为**SQLFetch**或**SQLFetchScroll** （如果结果集大小限制不能实现在数据源） 如果它不能保证该 SQL_ATTR_将正确实施 MAX_ROWS。<br /><br /> 它是驱动程序定义的 SQL_ATTR_MAX_ROWS 是否适用于以外 （例如目录函数） 的 SELECT 语句的语句。<br /><br /> 可以在打开的游标; 上设置此属性的值但是，该设置可能不会立即生效，在这种情况下该驱动程序将返回 SQLSTATE 01s02 的警告 （选项值已更改） 和将该属性重置为其原始值。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|一个 SQLULEN 值，确定如何处理目录函数的字符串自变量。<br /><br /> 如果 SQL_TRUE，目录函数的字符串自变量将被视为标识符。 这种情况并不重要。 对于 nondelimited 字符串，该驱动程序中删除任何尾随空格和字符串折叠为大写形式。 对于带分隔符的字符串，该驱动程序中移除任何前导空格或尾随空格和采用任何按字面意思是分隔符之间。 如果这些自变量之一设置为 null 指针，函数将返回 SQL_ERROR 和 SQLSTATE HY009 （不允许使用 null 指针）。<br /><br /> 如果 SQL_FALSE，目录函数的字符串自变量不被视为标识符。 这种情况很重要。 它们可以包含字符串的搜索模式或，具体取决于自变量。<br /><br /> 默认值为 SQL_FALSE。<br /><br /> *TableType*参数**SQLTables**，它将采用的值，列表不会影响此属性。<br /><br /> 此外可以在连接级别上设置 SQL_ATTR_METADATA_ID。 （它和 SQL_ATTR_ASYNC_ENABLE 是，还有一些连接特性的唯一语句属性。）<br /><br /> 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|SQLULEN 值，该值指示该驱动程序是否应扫描的转义序列的 SQL 字符串：<br /><br /> SQL_NOSCAN_OFF = 驱动程序扫描 SQL 字符串的转义序列 （默认值）。<br /><br /> SQL_NOSCAN_ON = 驱动程序不会扫描 SQL 字符串的转义序列。 相反，该驱动程序将发送到数据源的直接的声明。<br /><br /> 有关详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 指向添加到指针来更改绑定的动态参数的偏移量的值。 如果此字段为非 null，该驱动程序将取消引用指针、 将取消引用的值添加到每个描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中的延迟字段并使用新指针值在绑定时。 它被设置为默认情况下 null。<br /><br /> 绑定偏移量是始终将直接添加到 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段。 如果偏移量更改为不同的值，新值仍会添加直接向描述符字段中的值。 新的偏移量不会添加到的字段值加上任何早期的偏移量。<br /><br /> 有关详细信息，请参阅[参数绑定偏移量](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 将此语句属性设置 APD 标头中设置 SQL_DESC_BIND_OFFSET_PTR 字段。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|SQLULEN 值，该值指示绑定方向，以用于动态参数。<br /><br /> 此字段设置为 SQL_PARAM_BIND_BY_COLUMN （默认值），以选择列的绑定。<br /><br /> 若要选择按行绑定，此字段设置为结构或实例将绑定到的动态参数的集的缓冲区的长度。 此长度必须包括所有绑定参数和结构或缓冲区，以确保当绑定参数的地址将递增，具有指定长度，结果将指向下一步中的相同参数的开头的任何填充空间参数集。 使用时*sizeof* ANSI C 中的运算符，此行为保证。<br /><br /> 有关详细信息，请参阅[绑定的参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置 APD 标头中设置 SQL_DESC_ BIND_TYPE 字段。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 值的数组的值用于在 SQL 语句的执行过程中忽略参数。 每个值设置为 SQL_PARAM_PROCEED （适用于要执行的参数） 或 SQL_PARAM_IGNORE （适用于要被忽略的参数）。<br /><br /> 通过设置状态值的中到 SQL_PARAM_IGNORE APD SQL_DESC_ARRAY_STATUS_PTR 指向数组中，可以在处理过程中忽略一组参数。 如果其状态值设置为 SQL_PARAM_PROCEED 或设置数组中的没有元素处理一组参数。<br /><br /> 此语句属性可以设置为 null 指针，在其中用例驱动程序不返回参数状态值。 此属性可以设置任何时候，但只有在下次时未使用的新值**SQLExecDirect**或**SQLExecute**调用。<br /><br /> 没有任何绑定的参数时，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置 APD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*值，该值指向 SQLUSMALLINT 数组值包含参数值的每一行后调用的状态信息**SQLExecute**或**SQLExecDirect**。 此字段是必需的仅当 PARAMSET_SIZE 大于 1。<br /><br /> Status 值可以包含以下值：<br /><br /> SQL_PARAM_SUCCESS： 此参数集的已成功执行 SQL 语句。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO: SQL 语句成功执行的参数; 此集但是，诊断数据结构中提供了警告信息。<br /><br /> SQL_PARAM_ERROR： 在处理此组参数时出错。 中的诊断数据结构提供了其他错误信息。<br /><br /> SQL_PARAM_UNUSED： 此参数集已不再使用，可能是因为，某些以前的参数集导致中止将来进行处理，出现错误，或因为 SQL_PARAM_IGNORE 已设置为该 SQL_ATTR_PARAM_ 所指定的数组中的参数集OPERATION_PTR。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE: 驱动程序的参数数组视为单个单元，因此不会生成此级别的错误的信息。<br /><br /> 此语句属性可以设置为 null 指针，在其中用例驱动程序不返回参数状态值。 此属性可以设置任何时候，但只有在下次时未使用的新值**SQLExecute**或**SQLExecDirect**调用。 请注意，设置此属性可以影响由驱动程序实现的输出参数行为。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置 IPD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|SQLULEN\*记录指向在其中以返回的已处理，包括错误集的参数集数量的缓冲区的字段。 如果这是 null 指针，则将返回没有数。<br /><br /> 将此语句属性设置 IPD 标头中设置 SQL_DESC_ROWS_PROCESSED_PTR 字段。<br /><br /> 如果调用**SQLExecDirect**或**SQLExecute** : SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 未返回此属性指向的缓冲区中的填充，缓冲区的内容是不确定。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|SQLULEN 值，该值指定每个参数的值的数目。 如果 SQL_ATTR_PARAMSET_SIZE 大于 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 指向数组。 基数的每个数组等于此字段的值。<br /><br /> 没有任何绑定的参数时，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置 APD 标头中设置 SQL_DESC_ARRAY_SIZE 字段。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|一个 SQLULEN 值对应于为要返回到应用程序之前执行的 SQL 语句中等待的秒数。 如果*ValuePtr*是等于 0 （默认值），没有任何超时。<br /><br /> 在指定的超时时间超过数据源中的最大超时或小于最小超时， **SQLSetStmtAttr**替代此值，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。<br /><br /> 请注意，应用程序无需调用**SQLCloseCursor**重用该语句，如果**选择**语句的操作已超时。<br /><br /> 在此语句属性中设置的查询超时值是在同步和异步模式中有效。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 值：<br /><br /> SQL_RD_ON = **SQLFetchScroll**以及在 ODBC 3*.x*， **SQLFetch**之后将光标置于到指定位置检索数据。 这是默认设置。<br /><br /> SQL_RD_OFF = **SQLFetchScroll**以及在 ODBC 3*.x*， **SQLFetch**后它将光标置于不检索数据。<br /><br /> 通过设置为 SQL_RD_OFF SQL_RETRIEVE_DATA，应用程序可以验证某行是否存在，或者检索行的书签，而不引发检索行的系统开销。 有关详细信息，请参阅[滚动和提取行](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 可以在打开的游标; 上设置此属性的值但是，该设置可能不会立即生效，在这种情况下该驱动程序将返回 SQLSTATE 01s02 的警告 （选项值已更改） 和将该属性重置为其原始值。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|指定的每个调用返回的行数的 SQLULEN 值**SQLFetch**或**SQLFetchScroll**。 它也是用于大容量书签操作中的书签数组中的行数**SQLBulkOperations**。 默认值为 1。<br /><br /> 如果指定的行集大小超过了支持数据源的最大行集大小，该驱动程序替代此值，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。<br /><br /> 有关详细信息，请参阅[行集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 将此语句属性设置 ARD 标头中设置 SQL_DESC_ARRAY_SIZE 字段。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 指向添加到指针来更改绑定的列数据的偏移量的值。 如果此字段为非 null，该驱动程序将取消引用指针、 将取消引用的值添加到每个描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中的延迟字段并使用新指针值在绑定时。 它被设置为默认情况下 null。<br /><br /> 将此语句属性设置 ARD 标头中设置 SQL_DESC_BIND_OFFSET_PTR 字段。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|设置绑定方向 SQLULEN 值时要使用**SQLFetch**或**SQLFetchScroll**相关联的语句上调用。 通过将该值设置为 SQL_BIND_BY_COLUMN 情况下，选择列绑定。 通过将该值设置为结构或结果列将绑定到其中的缓冲区的实例的长度，选择按行绑定。<br /><br /> 如果指定长度，则它必须包含的所有绑定的列和结构或缓冲区，以确保当绑定列的地址将递增，具有指定长度，结果将指向第中的同一列的开头的任何填充空间e 下一行。 使用时**sizeof**运算符具有结构或联合在 ANSI C 中，为保证此行为。<br /><br /> 按列绑定是默认绑定方向为**SQLFetch**和**SQLFetchScroll**。<br /><br /> 有关详细信息，请参阅[绑定与块状游标一起使用的列](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 将此语句属性设置 ARD 标头中设置 SQL_DESC_BIND_TYPE 字段。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|是整个结果中的当前行数 SQLULEN 值设置。 如果无法确定当前行数或没有当前行，该驱动程序将返回 0。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未通过调用设置**SQLSetStmtAttr**。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 值的数组的值用于在大容量操作使用过程中忽略某一行**SQLSetPos**。 每个值设置为 SQL_ROW_PROCEED （适用于要包含在大容量操作中的行） 或 SQL_ROW_IGNORE （适用于从大容量操作中排除的行）。 (通过调用到的过程中使用此数组不能忽略行**SQLBulkOperations**。)<br /><br /> 此语句属性可以设置为 null 指针，用例驱动程序不返回行状态值。 此属性可以设置任何时候，但只有在下次时未使用的新值**SQLSetPos**调用。<br /><br /> 有关详细信息，请参阅[更新中行 SQLSetPos 行集](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)和[删除中 SQLSetPos 行集的行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 将此语句属性设置中 ARD 设置 SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 数组的值后调用值包含行状态值**SQLFetch**或**SQLFetchScroll**。 数组有有行的行集中的所有元素。<br /><br /> 此语句属性可以设置为 null 指针，用例驱动程序不返回行状态值。 此属性可以设置任何时候，但只有在下次时未使用的新值**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。<br /><br /> 有关详细信息，请参阅[提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 将此语句属性设置 IRD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。<br /><br /> 此属性映射通过 ODBC 2*.x*驱动程序添加到*rgbRowStatus*对的调用中的数组**SQLExtendedFetch**。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|SQLULEN\*值，该值指向在其中以返回到调用后读取的行数的缓冲区**SQLFetch**或**SQLFetchScroll**; 执行大容量操作所影响的行数通过调用**SQLSetPos**与*操作*SQL_REFRESH; 或通过执行的大容量操作影响的行数参数**SQLBulkOperations**. 此数字包括错误行。<br /><br /> 有关详细信息，请参阅[提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 将此语句属性设置 IRD 标头中设置 SQL_DESC_ROWS_PROCESSED_PTR 字段。<br /><br /> 如果调用**SQLFetch**或**SQLFetchScroll** : SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 未返回此属性指向的缓冲区中的填充，缓冲区的内容是不确定。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|一个 SQLULEN 值，指定驱动程序模拟定位的 update 和 delete 语句是否保证此类语句影响只有一个单个行。<br /><br /> 若要模拟定位的 update 和 delete 语句，大多数驱动程序构造搜索**更新**或**删除**语句包含**其中**指定子句当前行中的每个列的值。 这些列组成的唯一密钥，除非此类语句可能会影响多个行。<br /><br /> 若要确保此类语句影响只有一个行，该驱动程序确定中唯一键的列，并将这些列添加到结果集。 如果应用程序可保证在结果集中的列组成的唯一密钥，该驱动程序不需要这样做。 这可能会降低执行时间。<br /><br /> SQL_SC_NON_UNIQUE = 驱动程序不模拟的保证是否定位 update 或 delete 语句将影响只有一行;它是应用程序的责任，若要这样做。 如果语句会影响多个行， **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**返回 SQLSTATE 01001 （游标操作冲突）。<br /><br /> SQL_SC_TRY_UNIQUE = 的驱动程序尝试以保证模拟定位更新或删除语句影响只包含一行。 该驱动程序执行速度始终都此类语句中，即使它们可能会影响多个行，例如，当没有唯一键。 如果语句会影响多个行， **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**返回 SQLSTATE 01001 （游标操作冲突）。<br /><br /> SQL_SC_UNIQUE = 模拟定位的更新的驱动程序保证或删除语句影响只包含一行。 如果该驱动程序无法保证这一点对于给定的语句， **SQLExecDirect**或**SQLPrepare**返回错误。<br /><br /> 如果数据源提供了本机 SQL 支持定位更新和删除语句和驱动程序不模拟游标，则返回 SQL_SUCCESS，为 SQL_SIMULATE_CURSOR 请求 SQL_SC_UNIQUE 时。 如果请求 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE，则返回 SQL_SUCCESS_WITH_INFO。 如果数据源提供 SQL_SC_TRY_UNIQUE 级别的支持，该驱动程序不为针对 SQL_SC_NON_UNIQUE 返回 SQL_SC_TRY_UNIQUE 和 SQL_SUCCESS_WITH_INFO 被返回 SQL_SUCCESS。<br /><br /> 如果数据源不支持指定的游标模拟类型，该驱动程序替换不同的模拟类型和返回 SQLSTATE 01s02 的警告 （选项值已更改）。 对于 SQL_SC_UNIQUE，驱动程序将替换为，按顺序，SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE。 对于 SQL_SC_TRY_UNIQUE，驱动程序将替换为 SQL_SC_NON_UNIQUE。<br /><br /> 默认值为 SQL_SC_UNIQUE。<br /><br /> 有关详细信息，请参阅[模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|指定应用程序是否将使用与某个游标的书签 SQLULEN 值：<br /><br /> SQL_UB_OFF = Off （默认）<br /><br /> SQL_UB_VARIABLE = 应用程序将与游标，使用书签和驱动程序将提供长度可变的书签，如果它们受支持。 在 ODBC 3 中已弃用 SQL_UB_FIXED*.x*。 ODBC 3*.x*应用程序应始终使用长度可变的书签，即使使用 ODBC 2*.x* （它支持仅 4 字节、 固定长度的书签） 的驱动程序。 这是因为固定长度书签是只是一种特殊的情况的长度可变的书签。 使用 ODBC 2 时*.x*驱动程序，则驱动程序管理器会将 SQL_UB_VARIABLE 映射到 SQL_UB_FIXED。<br /><br /> 若要使用与某个游标的书签，应用程序必须指定此属性与 SQL_UB_VARIABLE 值之前打开游标。<br /><br /> 有关详细信息，请参阅[检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [仅当描述符不是实现描述符，而不是应用程序描述符，可以以异步方式调用 1] 这些函数。  
  
 请参阅[列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)和[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句特性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置单个字段的描述符|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

