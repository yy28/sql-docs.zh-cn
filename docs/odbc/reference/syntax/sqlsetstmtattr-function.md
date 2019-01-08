---
title: SQLSetStmtAttr 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f22051ca07dbdb732cfcda2f8200b7375f593463
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202886"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**设置与语句相关的属性。  
  
> [!NOTE]
>  详细了解驱动程序管理器映射的内容到此函数时 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，请参阅[用于向后映射替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 [输入]选项设置，列出在"注释"。  
  
 *ValuePtr*  
 [输入]若要与之关联的值*属性*。 具体取决于值*特性*， *ValuePtr*将是以下之一：  
  
-   ODBC 描述符句柄。  
  
-   一个 SQLUINTEGER 值。  
  
-   一个 sqlulen 生成的值。  
  
-   一个指向以下项之一：  
  
    -   以 null 结尾的字符串。  
  
    -   二进制缓冲区中。  
  
    -   一个值或类型为 SQLLEN、 sqlulen 生成或 SQLUSMALLINT 的数组。  
  
    -   驱动程序定义的值。  
  
 如果*特性*参数为特定于驱动程序的值， *ValuePtr*可能是一个有符号的整数。  
  
 *StringLength*  
 [输入]如果*特性*是一个 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度\* *ValuePtr*. 如果*特性*是一个 ODBC 定义的属性和*ValuePtr*是一个整数*StringLength*将被忽略。  
  
 如果*特性*是一个驱动程序定义的属性，该应用程序通过设置指示特性的驱动程序管理器的性质*StringLength*参数。 *StringLength*可以具有以下值：  
  
-   如果*ValuePtr*是一个指向一个字符串，然后*StringLength*是 sql_nts; 的字符串的长度。  
  
-   如果*ValuePtr*是一个指向二进制缓冲区，则 SQL_LEN_BINARY_ATTR 将结果放置于该应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*指向的字符串或二进制字符串以外的值，即*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含一个固定长度值，则*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，根据需要。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetStmtAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetStmtAttr** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持在指定的值*ValuePtr*，或在指定的值*ValuePtr*无效由于实现运行情况，因此驱动程序替换一个相近的值。 (**SQLGetStmtAttr**可以调用以确定暂时被替换的值。)替换值是否为有效*StatementHandle*直到关闭游标，此时语句属性将恢复为以前的值。 可以更改的语句属性有：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|*特性*是 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR，还是 SQL_ATTR_USE_BOOKMARKS，并打开游标的。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY009|使用空指针无效|*特性*参数标识所需的字符串属性，一个语句属性和*ValuePtr*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLSetStmtAttr**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY011 并显示|现在无法设置属性|*特性*SQL_ATTR_CONCURRENCY、 SQL_ ATTR_CURSOR_TYPE、 SQL_ ATTR_SIMULATE_CURSOR 或 SQL_ ATTR_USE_BOOKMARKS，准备的语句。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY017|自动分配的描述符句柄的使用无效|（数据挖掘）*特性*参数为 SQL_ATTR_IMP_ROW_DESC 或 SQL_ATTR_IMP_PARAM_DESC。<br /><br /> （数据挖掘）*特性*参数为 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 和中的值*ValuePtr*最初以外句柄的隐式分配的描述符句柄为 ARD 或 APD 分配。|  
|HY024|属性值无效|给出指定*特性*值，在指定了无效的值*ValuePtr*。 （驱动程序管理器将返回此仅适用于连接和语句属性接受一组离散的值，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ ATTR_ASYNC_ENABLE 的 SQLSTATE。 对于所有其他连接和语句属性，该驱动程序必须验证中指定的值*ValuePtr*。)<br /><br /> *特性*参数为 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，并*ValuePtr*已不在同一连接的显式分配的描述符句柄*StatementHandle*参数。|  
|HY090|字符串或缓冲区长度无效|（数据挖掘）  *\*ValuePtr*是一个字符串，并且*StringLength*参数为小于 0，但不是 sql_nts;。|  
|HY092|属性/选项标识符无效|(DM) 的参数指定的值*特性*对 ODBC 驱动程序支持的版本无效。<br /><br /> (DM) 的参数指定的值*特性*是只读的属性。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*特性*版本的 ODBC 驱动程序支持，但不受驱动程序是有效的 ODBC 语句属性。<br /><br /> *特性*参数为 sql_attr_async_enable 设置，并调用**SQLGetInfo**与*信息类型*SQL_ASYNC_MODE 返回 SQL_AM_CONNECTION。<br /><br /> *特性*参数为 SQL_ATTR_ENABLE_AUTO_IPD，而 SQL_ATTR_AUTO_IPD 连接属性的值 SQL_FALSE。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|S1118|驱动程序不支持异步通知|如果调用**SQLSetStmtAttr**设置 SQL_ATTR_ASYNC_STMT_EVENT; 驱动程序不支持异步通知。|  
  
## <a name="comments"></a>注释  
 之前已被另一个调用更改语句的语句属性保持有效**SQLSetStmtAttr**或直到通过调用删除该语句**SQLFreeHandle**。 调用**SQLFreeStmt**与 SQL_CLOSE、 SQL_UNBIND 或 SQL_RESET_PARAMS 选项不会不会重置的语句属性。  
  
 如果数据源不支持在指定的值，某些语句属性支持类似的值替换成*ValuePtr*。 在这种情况下，驱动程序将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。 例如，如果*特性*是 SQL_ATTR_CONCURRENCY 和*ValuePtr*是否 SQL_CONCUR_ROWVER，以及如果数据源不支持此，该驱动程序将替换为 SQL_CONCUR_VALUES 并且返回 SQL_SUCCESS_WITH_INFO。 若要确定被替换的值，应用程序调用**SQLGetStmtAttr**。  
  
 信息的格式设置*ValuePtr*取决于指定*属性*。 **SQLSetStmtAttr**接受两个不同的格式之一的属性信息： 字符串或整数值。 该特性的描述中记录了每个消息格式。 此格式适用于为每个属性返回的信息**SQLGetStmtAttr**。 指向的字符串*ValuePtr*的参数**SQLSetStmtAttr**具有长度*StringLength*。  
  
> [!NOTE]
>  设置在连接级别的语句属性通过调用的能力**SQLSetConnectAttr** ODBC 3 中已弃用 *.x*。 ODBC 3 *.x*应用程序应永远不会在连接级别设置语句属性。 ODBC 3 *.x*不能在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句属性，并且可以设置语句属性设置在连接级别或语句级别。  
> 
> [!NOTE]
>  ODBC 3 *.x*驱动程序仅需要支持此功能，如果他们应适用于 ODBC 2 *.x*设置 ODBC 2 应用程序都 *.x*在连接级别的语句选项。 有关详细信息，请参阅"设置语句选项在连接级别"下[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附录 g:为了向后兼容的驱动程序指南。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>设置描述符字段的语句属性  
 多个语句属性对应于一个描述符标头字段。 描述符字段的设置中设置这些属性实际结果。 通过调用设置字段**SQLSetStmtAttr**而不是个**SQLSetDescField**描述符句柄不需要获取函数调用的优点。  
  
> [!CAUTION]  
>  调用**SQLSetStmtAttr**为一条语句可能会影响其他语句。 APD 或与语句相关联的 ARD 显式分配，并且也是与其他语句相关联，将发生这种情况。 因为**SQLSetStmtAttr**修改 APD 或 ARD，所做的修改将应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联此描述符的其他语句 (通过调用**SQLSetStmtAttr** SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 字段设置为另一种描述符句柄） 之前调用**SQLSetStmtAttr**试。  
  
 当由于所设置的相应语句属性设置描述符字段时，仅为都由该语句与当前相关联的适用描述符设置字段*StatementHandle*自变量，以及属性设置不会影响任何可能与该语句在将来的描述符。 当通过调用设置也是语句属性的描述符字段**SQLSetDescField**，设置相应的语句属性。 如果从语句中取消关联显式分配的描述符，对应于一个标头字段的语句属性将恢复为在隐式分配的描述符字段的值。  
  
 何时分配一个语句 (请参阅[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md))，四个描述符句柄将自动分配和与语句相关联。 显式分配的描述符句柄可通过调用与该语句相关联**SQLAllocHandle**与*fHandleType*的 SQL_HANDLE_DESC 分配描述符句柄并调用**SQLSetStmtAttr**将描述符句柄与语句相关联。  
  
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
 下表中; 中显示当前定义的属性和在其中引入的 ODBC 版本应更多属性将由驱动程序以利用不同的数据源。 由 ODBC; 保留一系列属性驱动程序开发人员必须保留供从 Open Group 自己特定于驱动程序使用的值。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|Attribute|*ValuePtr*内容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|句柄，以便后续调用 APD **SQLExecute**并**SQLExecDirect**语句句柄。 此属性的初始值是在初始分配该语句时隐式分配的描述符。 如果此属性的值设置为 SQL_NULL_DESC 或描述符最初分配的句柄，从其中取消关联是以前与语句句柄相关联的显式分配的 APD 句柄和语句句柄将恢复为隐式分配 APD 句柄。<br /><br /> 不能设置此属性，为已为另一个语句隐式分配的描述符句柄或隐式设置在同一语句; 的另一个描述符句柄隐式分配的描述符句柄不能与多个语句或描述符句柄相关联。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|为语句句柄上的后续提取 ARD 句柄。 此属性的初始值是在初始分配该语句时隐式分配的描述符。 如果此属性的值设置为 SQL_NULL_DESC 或描述符最初分配的句柄，从其中取消关联是以前与语句句柄相关联的显式分配的 ARD 句柄和语句句柄将恢复为隐式分配 ARD 句柄。<br /><br /> 不能设置此属性，为已为另一个语句隐式分配的描述符句柄或隐式设置在同一语句; 的另一个描述符句柄隐式分配的描述符句柄不能与多个语句或描述符句柄相关联。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|一个 sqlulen 生成值，该值指定是否以异步方式执行与指定的语句时调用的函数：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用语句级别的异步执行支持 （默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 启用语句级别的异步执行支持。<br /><br /> 有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> 使用语句级别的异步执行支持的驱动程序，请将语句属性 sql_attr_async_enable 设置为只读。 分配语句句柄时，其值为具有相同名称的连接级别属性的值相同。<br /><br /> 调用**SQLSetStmtAttr** sql_attr_async_enable 设置时 SQL_ASYNC_MODE*信息类型*返回 SQL_AM_CONNECTION 返回 SQLSTATE HYC00 （未实现的可选功能）。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)有关详细信息。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|一个 SQLPOINTER 值，该值是事件的句柄。<br /><br /> 异步函数完成通知的启用通过调用**SQLSetStmtAttr**若要设置**SQL_ATTR_ASYNC_STMT_EVENT**属性，指定的事件句柄。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|SQLPOINTER 异步回调函数。<br /><br /> 驱动程序管理器可以调用的驱动程序仅**SQLSetStmtAttr**具有此特性的函数。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|SQLPOINTER 上下文结构<br /><br /> 驱动程序管理器可以调用的驱动程序仅**SQLSetStmtAttr**具有此特性的函数。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|一个指定游标并发的 sqlulen 生成值：<br /><br /> SQL_CONCUR_READ_ONLY = 游标是只读的。 不允许任何更新。<br /><br /> SQL_CONCUR_LOCK = 游标使用的锁定足以确保可以更新的行的最低级别。<br /><br /> SQL_CONCUR_ROWVER = 游标使用乐观并发控制，例如 SQLBase ROWID 或 Sybase 时间戳的行版本进行比较。<br /><br /> SQL_CONCUR_VALUES = 游标使用乐观并发控制、 对值进行比较。<br /><br /> 默认值为 sql_attr_concurrency 设置为 SQL_CONCUR_READ_ONLY。<br /><br /> 不能为打开的游标指定此属性。 有关详细信息，请参阅[并发类型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果 SQL_ATTR_CURSOR_TYPE*特性*更改为不支持 sql_attr_concurrency 设置的当前值类型，sql_attr_concurrency 设置的值将更改在执行时，和时发出警告**SQLExecDirect**或**SQLPrepare**调用。<br /><br /> 如果该驱动程序支持**SELECT FOR UPDATE** sql_attr_concurrency 设置的值设置为 SQL_CONCUR_READ_ONLY 时执行语句，此类语句，就会返回错误。 如果 sql_attr_concurrency 设置的值更改为一个值，该驱动程序支持的 SQL_ATTR_CURSOR_TYPE 某些值而不是 SQL_ATTR_CURSOR_TYPE 的当前值，将在执行时间和 SQLSTATE 01S02 更改的 SQL_ATTR_CURSOR_TYPE 值（选项值已更改） 时发出**SQLExecDirect**或**SQLPrepare**调用。<br /><br /> 如果数据源不支持指定的并发，驱动程序将替换为不同的并发，并返回 SQLSTATE 01S02 （选项值已更改）。 对于 SQL_CONCUR_VALUES，驱动程序将替换为 SQL_CONCUR_ROWVER，反之亦然。 对于 SQL_CONCUR_LOCK，驱动程序将替换为，按顺序，SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES。 直到执行时不检查被替换的值的有效性。<br /><br /> 有关 SQL_ATTR_CONCURRENCY 和其他游标属性之间的关系的详细信息，请参阅[游标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|一个 sqlulen 生成值，指定的应用程序所需的支持级别。 将此属性设置会影响对后续调用**SQLExecDirect**并**SQLExecute**。<br /><br /> SQL_NONSCROLLABLE = 可滚动游标的语句句柄上不需要。 如果应用程序调用**SQLFetchScroll**此句柄，唯一有效的值上*FetchOrientation*是 SQL_FETCH_NEXT。 这是默认设置。<br /><br /> SQL_SCROLLABLE = 可滚动游标要求对语句句柄。 调用时**SQLFetchScroll**，应用程序可能指定的任何有效的值*FetchOrientation*，实现游标定位在顺序模式以外的模式下。<br /><br /> 有关可滚动游标的详细信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关 SQL_ATTR_CURSOR_SCROLLABLE 和其他游标属性之间的关系的详细信息，请参阅[游标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|Sqlulen 生成值，该值指定是否使可见游标语句句柄上的另一个游标设置为结果所做的更改。 将此属性设置会影响对后续调用**SQLExecDirect**并**SQLExecute**。 应用程序可以读取在应用程序设置要获取其初始状态或其状态为最最近此特性的值返回。<br /><br /> SQL_UNSPECIFIED = 未指定游标类型是什么并是否游标语句句柄上的使可见的结果集由另一个游标所做的更改。 游标语句句柄上的可能会使可见 none、 部分或全部此类更改。 这是默认设置。<br /><br /> SQL_INSENSITIVE = 由任何其他游标的所有游标语句句柄显示的结果集而无需专用于反映将对其做任何更改。 不敏感游标是只读的。 这对应于静态游标，它是只读的并发。<br /><br /> SQL_SENSITIVE = 语句句柄品牌可见由另一个游标设置为结果所做的所有更改上的所有游标。<br /><br /> 有关 SQL_ATTR_CURSOR_SENSITIVITY 和其他游标属性之间的关系的详细信息，请参阅[游标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|Sqlulen 生成值，该值指定游标类型：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 向前滚动游标唯一。<br /><br /> SQL_CURSOR_STATIC = 数据在结果集为静态。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 驱动程序将保存并 SQL_ATTR_KEYSET_SIZE 语句属性中指定的行数为使用密钥。<br /><br /> SQL_CURSOR_DYNAMIC = 驱动程序将保存，并使用行集中的行仅密钥。<br /><br /> 默认值为 SQL_CURSOR_FORWARD_ONLY。 已准备好的 SQL 语句之后，不能指定此属性。<br /><br /> 如果数据源不支持指定的游标类型，该驱动程序将替换为不同的游标类型，并返回 SQLSTATE 01S02 （选项值已更改）。 对于混合或动态游标，该驱动程序替换，按顺序，由键集驱动的或静态游标。 对于由键集驱动的游标，该驱动程序将替换为静态游标。<br /><br /> 有关可滚动游标类型的详细信息，请参阅[可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 有关 SQL_ATTR_CURSOR_TYPE 和其他游标属性之间的关系的详细信息，请参阅[游标特征和游标类型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|指定是否执行自动填充 IPD sqlulen 生成值：<br /><br /> SQL_TRUE 表示打开到调用后自动填充 IPD **SQLPrepare**。 SQL_FALSE 表示关闭后自动填充 IPD **SQLPrepare**。 (应用程序仍可以通过调用获取 IPD 字段信息**SQLDescribeParam**，如果受支持。)语句属性 SQL_ATTR_ENABLE_AUTO_IPD 的默认值为 SQL_FALSE。 有关详细信息，请参阅[自动填充 IPD](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|为 SQLLEN\*指向二进制书签值。 当**SQLFetchScroll**使用调用*fFetchOrientation*驱动程序提取等于 SQL_FETCH_BOOKMARK，此字段中的书签值。 此字段默认为 null 指针。 有关详细信息，请参阅[按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 指向此字段的值不用于按书签删除、 更新的书签，或通过书签操作中提取**SQLBulkOperations**，其中使用缓存在行集的缓冲区中的书签。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD 句柄。 此属性的值是在初始分配该语句时分配的描述符。 应用程序不能设置此属性。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未设置通过调用**SQLSetStmtAttr**。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD 句柄。 此属性的值是在初始分配该语句时分配的描述符。 应用程序不能设置此属性。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未设置通过调用**SQLSetStmtAttr**。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|指定的由键集驱动游标中的行数 SQLULEN。 如果由键集大小为 0 （默认值），则游标是完全由键集驱动。 如果由键集大小大于 0，则游标被混合 （键集中由键集驱动和动态外键集）。 默认值由键集大小为 0。 有关由键集驱动游标的详细信息，请参阅[由键集驱动游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定的大小超出最大的键集大小，该驱动程序替代该大小，并返回 SQLSTATE 01S02 （选项值已更改）。<br /><br /> **SQLFetch**或**SQLFetchScroll**如果由键集大小是大于 0 且小于行集大小，则返回错误。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|Sqlulen 生成值，该值指定最大的驱动程序将返回字符或二进制列中的数据量。 如果*ValuePtr*可用数据的长度小于**SQLFetch**或**SQLGetData**将截断数据，并返回 SQL_SUCCESS。 如果*ValuePtr*为 0 （默认值），则驱动程序将尝试返回所有可用的数据。<br /><br /> 如果指定的长度小于最小的数据源可以返回的数据量或大于最大的数据量，可以返回数据源，驱动程序替换的值并将返回 SQLSTATE 01S02 （选项值已更改）。<br /><br /> 此属性的值可以设置对打开的游标;但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02 （选项值已更改） 并将该属性重置为其原始值。<br /><br /> 此属性用于减少网络流量，并且应仅在数据源 （而不是驱动程序） 中的多层驱动程序可以实现它时支持。 此机制不应由应用程序要截断的数据;若要减少收到的数据，应用程序应指定最大缓冲区的默认值*BufferLength*中的参数**SQLBindCol**或**SQLGetData**。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|对应于要返回的应用程序的行的最大数 sqlulen 生成值**选择**语句。 如果\* *ValuePtr*等于 0 （默认值），驱动程序将返回所有行。<br /><br /> 此属性用于减少网络流量。 从概念上讲，应用时的结果集创建并与第一个结果集限制*ValuePtr*行。 如果结果集中的行数大于*ValuePtr*，结果集将被截断。<br /><br /> SQL_ATTR_MAX_ROWS 适用于所有结果集上*语句*，包括那些目录函数返回的。 SQL_ATTR_MAX_ROWS 建立游标行计数的值的最大。<br /><br /> 驱动程序应该不会模拟 SQL_ATTR_MAX_ROWS 行为**SQLFetch**或**SQLFetchScroll** （如果结果集大小限制不能实现在数据源） 如果无法保证该 SQL_ATTR_MAX_ROWS 将正确实现。<br /><br /> 它是驱动程序定义 SQL_ATTR_MAX_ROWS 是否适用于非 SELECT 语句 （如目录函数） 的语句。<br /><br /> 此属性的值可以设置对打开的游标;但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02 （选项值已更改） 并将该属性重置为其原始值。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Sqlulen 生成值，该值确定如何处理目录函数将字符串参数。<br /><br /> 如果 SQL_TRUE，目录函数的字符串自变量被视为标识符。 这种情况并不重要。 对于分隔字符串，该驱动程序中删除任何尾随空格和字符串折叠为大写。 对于带分隔符的字符串，该驱动程序中删除任何前导或尾随空格和采用任何按字面意思是在分隔符。 如果其中一个参数设置为 null 指针，该函数返回 SQL_ERROR 并且 SQLSTATE HY009 （null 指针的使用无效）。<br /><br /> 如果 SQL_FALSE，目录函数将字符串参数不被视为标识符。 这种情况很重要。 它们可以包含字符串的搜索模式，取决于参数。<br /><br /> 默认值为 SQL_FALSE。<br /><br /> *TableType*的参数**SQLTables**，其将一系列值，不会影响此属性。<br /><br /> 此外可以在连接级别上设置 SQL_ATTR_METADATA_ID。 （它和 sql_attr_async_enable 设置是也是连接属性的唯一语句属性。）<br /><br /> 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|Sqlulen 生成值，该值指示该驱动程序是否应扫描 SQL 字符串的转义序列：<br /><br /> SQL_NOSCAN_OFF = 驱动程序扫描 SQL 字符串的转义序列 （默认值）。<br /><br /> SQL_NOSCAN_ON = 驱动程序不会扫描 SQL 转义序列的字符串。 相反，该驱动程序该语句将直接发送到数据源。<br /><br /> 有关详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 偏移量添加到要更改的动态参数的绑定指针所指向的值。 如果此字段为非 null，驱动程序取消引用指针，将取消引用的值添加到每个描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中的延迟字段并使用新指针值绑定时。 它设置为默认情况下为 null。<br /><br /> 绑定偏移量是始终直接添加到 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段。 如果偏移量更改为不同的值，新值是仍直接添加到描述符字段中的值。 新的偏移量不添加到字段值再加上任何早期的偏移量。<br /><br /> 有关详细信息，请参阅[参数绑定偏移量](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 设置此语句属性 APD 标头中设置 SQL_DESC_BIND_OFFSET_PTR 字段。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|Sqlulen 生成值，该值指示要用于动态参数的绑定方向。<br /><br /> 此字段设置为 sql_param_bind_by_column （默认值），可以选择按列绑定。<br /><br /> 若要选择按行绑定，此字段设置为结构或实例将绑定到一组的动态参数的缓冲区的长度。 此长度必须包括所有绑定参数和结构或缓冲区以确保当绑定参数的地址与指定的长度递增时，结果将点到下一步中的相同参数的开头的任何填充大小的空间参数集。 使用时*sizeof* ANSI C 中的运算符，将保证该行为。<br /><br /> 有关详细信息，请参阅[绑定的参数的数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 设置此语句属性 APD 标头中设置 SQL_DESC_ BIND_TYPE 字段。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 值的数组的值用于在 SQL 语句的执行过程中忽略参数。 每个值设置为 SQL_PARAM_PROCEED （适用于要执行的参数） 或 SQL_PARAM_IGNORE （适用于要忽略的参数）。<br /><br /> 通过设置指向 SQL_DESC_ARRAY_STATUS_PTR 到 SQL_PARAM_IGNORE APD 中的数组中的状态值，可以在处理期间忽略的一组参数。 如果其状态的值设置为 SQL_PARAM_PROCEED 或设置数组中的没有元素处理的一组参数。<br /><br /> 此语句属性可以设置为 null 指针，在这种情况下，驱动程序不返回参数状态值。 此属性可以设置在任何时候，但下一次之前未使用的新值**SQLExecDirect**或**SQLExecute**调用。<br /><br /> 没有绑定的参数时，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 设置此语句属性 APD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*值，该值指向数组 SQLUSMALLINT 值包含每行的参数值对的调用后的状态信息**SQLExecute**或**SQLExecDirect**。 此字段是必需的仅当 PARAMSET_SIZE 大于 1。<br /><br /> 状态值可以包含以下值：<br /><br /> SQL_PARAM_SUCCESS:此参数集的成功执行 SQL 语句。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO:参数; 这一组已成功执行 SQL 语句但是，诊断数据结构中提供了警告信息。<br /><br /> SQL_PARAM_ERROR:处理此套参数时出错。 诊断数据结构中提供了其他错误的信息。<br /><br /> SQL_PARAM_UNUSED:此参数集为未使用，可能是因为，一些以前的参数集导致中止将来进行处理，出现错误或因为 SQL_PARAM_IGNORE 设置该集指定的 SQL_ATTR_PARAM_OPERATION_PTR 数组中的参数。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE:该驱动程序将参数的数组作为一个整体化单元，并因此不会生成此级别的错误的信息。<br /><br /> 此语句属性可以设置为 null 指针，在这种情况下，驱动程序不返回参数状态值。 此属性可以设置在任何时候，但下一次之前未使用的新值**SQLExecute**或**SQLExecDirect**调用。 请注意，设置此属性可能会影响由驱动程序实现的输出参数行为。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置在 IPD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|SQLULEN\*指向的缓冲区中要返回的已处理，包括错误集的参数集的数量的记录字段。 如果这是 null 指针，则将返回无编号。<br /><br /> 将此语句属性设置在 IPD 标头中设置 SQL_DESC_ROWS_PROCESSED_PTR 字段。<br /><br /> 如果在调用**SQLExecDirect**或**SQLExecute** ，填充此属性指向的缓冲区中未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|则 SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|Sqlulen 生成值，该值指定为每个参数的值的数目。 如果 SQL_ATTR_PARAMSET_SIZE 大于 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 指向数组。 每个数组的基数是此字段的值相等。<br /><br /> 没有绑定的参数时，将忽略此属性。<br /><br /> 有关详细信息，请参阅[使用的参数的数组](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 将此语句属性设置的 SQL_DESC_ARRAY_SIZE 字段设置 APD 标头中。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|对应于为 SQL 语句执行返回给应用程序之前等待的秒数 sqlulen 生成值。 如果*ValuePtr*是等于 0 （默认值），没有任何超时。<br /><br /> 如果指定的超时时间超出了数据源中的最大超时或小于最小超时值，则**SQLSetStmtAttr**替代该值，并返回 SQLSTATE 01S02 （选项值已更改）。<br /><br /> 请注意，该应用程序无需调用**SQLCloseCursor**如果重复使用该语句**选择**语句已超时。<br /><br /> 在此语句属性中设置的查询超时值是在同步和异步模式中有效。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|Sqlulen 生成的值：<br /><br /> SQL_RD_ON = **SQLFetchScroll**并在 ODBC 3 *.x*， **SQLFetch**之后将光标放置到指定位置检索数据。 这是默认设置。<br /><br /> SQL_RD_OFF = **SQLFetchScroll**并在 ODBC 3 *.x*， **SQLFetch**之后它将光标置于不检索数据。<br /><br /> 通过设置为 SQL_RD_OFF SQL_RETRIEVE_DATA，应用程序可以验证行存在，或检索的行的书签，而不会产生检索行的开销。 有关详细信息，请参阅[滚动和提取行](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 此属性的值可以设置对打开的游标;但是，该设置可能不会立即生效，在这种情况下，驱动程序将返回 SQLSTATE 01S02 （选项值已更改） 并将该属性重置为其原始值。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|Sqlulen 生成值，该值指定由每次调用返回的行数**SQLFetch**或**SQLFetchScroll**。 它也是在大容量书签运算中的书签数组中的行数**SQLBulkOperations**。 默认值为 1。<br /><br /> 如果指定的行集大小超过最大行集大小支持的数据源，该驱动程序替代该值，并返回 SQLSTATE 01S02 （选项值已更改）。<br /><br /> 有关详细信息，请参阅[行集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 将此语句属性设置的 SQL_DESC_ARRAY_SIZE 字段设置 ARD 标头中。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 偏移量添加到要更改的列数据的绑定指针所指向的值。 如果此字段为非 null，驱动程序取消引用指针，将取消引用的值添加到每个描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中的延迟字段并使用新指针值绑定时。 它设置为默认情况下为 null。<br /><br /> 设置此语句属性 ARD 标头中设置 SQL_DESC_BIND_OFFSET_PTR 字段。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|设置绑定方向的 sqlulen 生成值时要使用**SQLFetch**或**SQLFetchScroll**对关联的语句调用。 通过将值设置为 sql_bind_by_column，可以选择按列绑定。 按行绑定被选中的值设置为一个结构或结果列绑定到其中的缓冲区的实例的长度。<br /><br /> 如果指定长度，则它必须包括所有绑定的列和结构或缓冲区以确保当绑定列的地址与指定的长度递增时，结果将点到个中的同一列开头的任何填充大小的空间e 下一行。 使用时**sizeof**运算符与结构或联合 ANSI C 中的，将保证该行为。<br /><br /> 按列绑定为的默认绑定方向**SQLFetch**并**SQLFetchScroll**。<br /><br /> 有关详细信息，请参阅[绑定列用于块游标](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 设置此语句属性 ARD 标头中设置 SQL_DESC_BIND_TYPE 字段。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|设置是在整个结果中的当前行数 sqlulen 生成值。 如果无法确定当前的行数或没有当前行，该驱动程序将返回 0。<br /><br /> 此属性可以通过调用来检索**SQLGetStmtAttr**但未设置通过调用**SQLSetStmtAttr**。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 值的数组的值用于在大容量操作使用过程中忽略行**SQLSetPos**。 每个值设置为 SQL_ROW_PROCEED （适用于要包含在大容量操作的行） 或 SQL_ROW_IGNORE （适用于要从大容量操作中排除的行）。 (在调用到期间使用此数组不能忽略行**SQLBulkOperations**。)<br /><br /> 此语句属性可以设置为 null 指针，用例驱动程序不返回行状态的值。 此属性可以设置在任何时候，但下一次之前未使用的新值**SQLSetPos**调用。<br /><br /> 有关详细信息，请参阅[更新行集中的行使用 SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)并[删除行集中的行使用 SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 设置此语句属性设置中 ARD SQL_DESC_ARRAY_STATUS_PTR 字段。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*指向 SQLUSMALLINT 的数组的值是在调用后值包含的行状态值**SQLFetch**或**SQLFetchScroll**。 数组不包含任意多个元素的行集中的行一样。<br /><br /> 此语句属性可以设置为 null 指针，用例驱动程序不返回行状态的值。 此属性可以设置在任何时候，但下一次之前未使用的新值**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。<br /><br /> 有关详细信息，请参阅[提取的行号和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 设置此语句属性 IRD 标头中设置 SQL_DESC_ARRAY_STATUS_PTR 字段。<br /><br /> 此属性映射由 ODBC 2 *.x*驱动程序添加到*rgbRowStatus*对的调用中的数组**SQLExtendedFetch**。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|SQLULEN\*指向的缓冲区中要返回到调用后提取的行数的值**SQLFetch**或**SQLFetchScroll**; 执行大容量复制操作受影响的行数通过调用**SQLSetPos**与*操作*SQL_REFRESH; 或通过执行大容量复制操作影响的行数的参数**SQLBulkOperations**. 此数字包括错误行。<br /><br /> 有关详细信息，请参阅[提取的行号和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 设置此语句属性 IRD 标头中设置 SQL_DESC_ROWS_PROCESSED_PTR 字段。<br /><br /> 如果在调用**SQLFetch**或**SQLFetchScroll** ，填充此属性指向的缓冲区中未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|Sqlulen 生成值，该值指定模拟定位的更新和删除语句的驱动程序是否保证此类语句会影响只有一个单一行。<br /><br /> 若要模拟定位的 update 和 delete 语句，大多数驱动程序构造搜索**更新**或**删除**包含语句**其中**指定子句当前行中的每个列的值。 除非这些列组成的唯一键，此类语句可能会影响多个行。<br /><br /> 若要保证此类语句会影响只有一行，驱动程序确定在唯一键列，并将这些列添加到结果集。 如果应用程序可保证在结果集中的列组成的唯一键，该驱动程序不需要执行此操作。 这可能会降低执行时间。<br /><br /> SQL_SC_NON_UNIQUE = 驱动程序不模拟的保证是否定位 update 或 delete 语句会影响只有一个行;它是应用程序负责执行此操作。 如果语句影响多个行**SQLExecute**， **SQLExecDirect**，或**SQLSetPos**返回 SQLSTATE 01001 （游标操作冲突）。<br /><br /> SQL_SC_TRY_UNIQUE = 的驱动程序尝试以保证模拟定位更新或删除语句影响只占一行。 即使它们可能会影响多个行，例如当驱动程序将始终执行此类语句没有唯一键。 如果语句影响多个行**SQLExecute**， **SQLExecDirect**，或**SQLSetPos**返回 SQLSTATE 01001 （游标操作冲突）。<br /><br /> SQL_SC_UNIQUE = 模拟定位的更新的驱动程序保证或删除语句影响只占一行。 如果该驱动程序不能保证这一点对于给定的语句， **SQLExecDirect**或**SQLPrepare**返回错误。<br /><br /> 如果数据源提供了本机 SQL 支持定位的 update 和 delete 语句和驱动程序不模拟游标，SQL_SC_UNIQUE 为 SQL_SIMULATE_CURSOR 请求将返回 SQL_SUCCESS。 如果请求 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE 时，将返回 SQL_SUCCESS_WITH_INFO。 如果数据源提供 SQL_SC_TRY_UNIQUE 级别的支持，该驱动程序不为 SQL_SC_NON_UNIQUE 返回 SQL_SC_TRY_UNIQUE 和 SQL_SUCCESS_WITH_INFO 返回 SQL_SUCCESS。<br /><br /> 如果数据源不支持指定的游标模拟类型，该驱动程序将替换为不同的模拟类型，并返回 SQLSTATE 01S02 （选项值已更改）。 对于 SQL_SC_UNIQUE，驱动程序将替换为，按顺序，SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE。 对于 SQL_SC_TRY_UNIQUE，驱动程序将替换为 SQL_SC_NON_UNIQUE。<br /><br /> 默认值为 SQL_SC_UNIQUE。<br /><br /> 有关详细信息，请参阅[模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|指定应用程序是否将与游标使用书签 sqlulen 生成值：<br /><br /> SQL_UB_OFF = Off （默认）<br /><br /> SQL_UB_VARIABLE = 应用程序将与某个游标使用书签和驱动程序将提供长度可变的书签，如果它们受支持。 在 ODBC 3 中已弃用 SQL_UB_FIXED *.x*。 ODBC 3 *.x*应用程序应始终使用长度可变的书签，即使使用 ODBC 2 *.x*驱动程序 （它支持仅 4 字节的定长书签）。 这是书签的因为定长书签是书签的只是书签的一种长度可变的特殊情况。 使用 ODBC 2 时 *.x*驱动程序，则驱动程序管理器会将 SQL_UB_VARIABLE 映射到 SQL_UB_FIXED。<br /><br /> 若要使用书签与游标，该应用程序必须指定此特性 SQL_UB_VARIABLE 值之前打开的游标。<br /><br /> 有关详细信息，请参阅[检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [仅当该描述符是实现描述符，而不是应用程序描述符，可以以异步方式调用 1] 这些函数。  
  
 请参阅[按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)并[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置单个的描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
