---
title: SQLSetConnectAttr 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8424462ddde4f99196e26d633fddfa5bb2ed6ee9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301933"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**设置控制连接方面的属性。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序时的详细信息，请参阅[映射应用程序向后兼容性的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
 *特性*  
 [输入]要设置的属性，列在"注释"中。  
  
 *ValuePtr*  
 [输入]指向要与*属性*关联的值的指针。 根据*属性*的值 *，ValuePtr*将是一个未签名的整数值，或将指向一个空端接的字符串。 请注意，*属性*参数的整数类型可能不是固定长度，请参阅注释部分了解详细信息。  
  
 *字符串长度*  
 [输入]如果*属性*是 ODBC 定义的属性 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为 **ValuePtr*的长度。 对于字符串数据，此参数应包含字符串中的字节数。  
  
 如果*属性*是 ODBC 定义的属性 *，ValuePtr*是整数，则忽略*字符串长度*。  
  
 如果*属性*是驱动程序定义的属性，则应用程序通过设置*StringLength*参数指示该属性对驱动程序管理器的性质。 *字符串长度*可以具有以下值：  
  
-   如果*ValuePtr*是指向字符串的指针，则*StringLength*是字符串的长度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*StringLength 中*。 这将在*字符串长度*中放置负值。  
  
-   如果*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*StringLength*应具有该值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定长度值，则*StringLength*会根据需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConnectAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_DBC的*句柄类型*和*连接句柄*的*句柄*。 下表列出了**SQLSetConnectAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
 驱动程序可以返回SQL_SUCCESS_WITH_INFO以提供有关设置选项的结果的信息。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持*ValuePtr*中指定的值，并替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08002|正在使用的连接名称|*属性*参数已SQL_ATTR_ODBC_CURSORS，并且驱动程序已连接到数据源。|  
|08003|连接未打开|（DM） 指定了需要打开连接*的属性*值，但*ConnectHandle*未处于连接状态。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|*属性*参数SQL_ATTR_CURRENT_CATALOG，并且结果集处于挂起状态。|  
|25000|本地交易中的非法操作|当尝试通过设置连接属性SQL_ATTR_ENLIST_IN_DTC在分布式事务连接 （DTC） 中登记时，连接位于本地事务中。<br /><br /> 已在 DTC 中登记了连接。<br /><br /> 已登记在分布式事务连接中连接，并通过将SQL_ATTR_AUTOCOMMIT设置为SQL_AUTOCOMMIT_OFF启动本地事务。|  
|3D000|无效目录名称|*属性*参数SQL_CURRENT_CATALOG，指定的目录名称无效。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|为*连接句柄*启用了异步处理。 **SQLSetConnectAttr**函数被调用，在完成执行之前，在*ConnectHandle*上调用[了 SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，然后在*ConnectHandle*上再次调用**SQLSetConnectAttr**函数。<br /><br /> 或者，调用**SQLSetConnectAttr**函数，在完成执行之前，SQLCancelHandle 是从多线程应用程序中的不同线程调用的**ConnectHandle。** *ConnectionHandle*|  
|HY009|无效使用空指针|*属性*参数标识了需要字符串值的连接属性 *，ValuePtr*参数为空指针。|  
|HY010|函数序列错误|（DM） 调用了与*ConnectHandle*关联的*语句句柄*的异步执行函数，并且在调用**SQLSetConnectAttr**时仍在执行。<br /><br /> （DM） 为*ConnectHandle*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用，用于与*连接句柄*关联的语句句柄之一，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用一个语句句柄，该*语句句柄*与*连接句柄*相关联并返回SQL_NEED_DATA。 **SQLExecute** **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） **SQLBrowseConnect**被调用用于*连接句柄*并返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前调用此功能。|  
|HY011|无法立即设置属性|*属性*参数SQL_ATTR_TXN_ISOLATION，并且事务处于打开状态。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY024|无效属性值|给定指定的*属性*值，在*ValuePtr*中指定了无效值。 （驱动程序管理器仅对接受一组离散值（如SQL_ATTR_ACCESS_MODE或SQL_ATTR_ASYNC_ENABLE）的连接和语句属性返回此 SQLSTATE。 对于所有其他连接和语句属性，驱动程序必须验证*ValuePtr*中指定的值 。<br /><br /> *属性*参数是SQL_ATTR_TRACEFILE或*SQL_ATTR_TRANSLATE_LIB，ValuePtr*是一个空字符串。|  
|HY090|无效的字符串或缓冲区长度|*（DM） \*ValuePtr*是一个字符串，*字符串长度*参数小于 0，但没有SQL_NTS。|  
|HY092|无效属性/选项标识符|（DM） 为参数*属性*指定的值对驱动程序支持的 ODBC 版本无效。<br /><br /> （DM） 为参数*属性*指定的值是只读属性。|  
|HY114|驱动程序不支持连接级异步函数执行|（DM） 应用程序尝试为不支持异步连接操作的驱动程序启用具有SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE异步函数执行。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|无法同时启用光标库和驱动程序感知池|有关详细信息，请参阅[驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 连接或语句属性，但驱动程序不支持该驱动程序。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*连接句柄*关联的驱动程序不支持该功能。|  
|IM009|无法加载转换 DLL|驱动程序无法加载为连接指定的转换 DLL。 仅当*属性*SQL_ATTR_TRANSLATE_LIB时，才能返回此错误。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
|S1118|驱动程序不支持异步通知|SQL_ATTR_ASYNC_DBC_EVENT已设置（在建立连接后），但驱动程序不支持异步通知。|  
  
 当*属性*是语句属性时 **，SQLSetConnectAttr**可以返回**SQLSetStmtAttr**返回的任何 SQLStatEs。  
  
## <a name="comments"></a>注释  
 有关连接属性的一般信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 当前定义的属性及其引入的 ODBC 版本在本节后面的表中显示;预计将定义更多的属性以利用不同的数据源。 ODBC 保留一系列属性;驱动程序开发人员必须从 Open Group 为其特定于驱动程序使用保留值。  
  
> [!NOTE]
>  通过调用**SQLSetConnectAttr**在连接级别设置语句属性的能力已在 ODBC 3 *.x*中被弃用。 ODBC 3 *.x*应用程序绝不应在连接级别设置语句属性。 ODBC 3 *.x*语句属性无法在连接级别设置，但SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE属性除外，这些属性既是连接属性，也是语句属性，可以在连接级别或语句级别设置。  
> 
>  ODBC 3 *.x*驱动程序仅需要支持此功能，如果它们应与在连接级别设置 ODBC 2 *.x*语句选项的 ODBC 2 *.x*应用程序配合使用。 有关详细信息，请参阅附录 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)：向后兼容性的驱动程序指南。  
  
 应用程序可以在分配和释放连接之间的任何时间调用**SQLSetConnectAttr。** 应用程序为连接成功设置的所有连接和语句属性将一直持续到在连接上调用**SQLFreeHandle**为止。 例如，如果应用程序在连接到数据源之前调用**SQLSetConnectAttr，** 则即使**SQLSetConnectAttr**在驱动程序中失败，当应用程序连接到数据源时，该属性也会保留。如果应用程序设置特定于驱动程序的属性，则即使应用程序连接到连接上的不同驱动程序，该属性也会保留。  
  
 某些连接属性只能在建立连接之前进行设置;其他连接只能在建立连接后进行设置。 下表指示必须在建立连接之前或之后设置的连接属性。 *任一表示*可以在连接之前或之后设置该属性。  
  
|特性|在连接之前还是之后设置？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|要么[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之后|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|要么[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之后|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之后|  
|SQL_ATTR_ASYNC_ENABLE|要么[2]|  
|SQL_ATTR_AUTO_IPD|之前或之后|  
|SQL_ATTR_AUTOCOMMIT|要么[5]|  
|SQL_ATTR_CONNECTION_DEAD|之后|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之后|  
|SQL_ATTR_CURRENT_CATALOG|要么[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|之后|  
|SQL_ATTR_ENLIST_IN_DTC|之后|  
|SQL_ATTR_LOGIN_TIMEOUT|之前|  
|SQL_ATTR_METADATA_ID|之前或之后|  
|SQL_ATTR_ODBC_CURSORS|之前|  
|SQL_ATTR_PACKET_SIZE|之前|  
|SQL_ATTR_QUIET_MODE|之前或之后|  
|SQL_ATTR_TRACE|之前或之后|  
|SQL_ATTR_TRACEFILE|之前或之后|  
|SQL_ATTR_TRANSLATE_LIB|之后|  
|SQL_ATTR_TRANSLATE_OPTION|之后|  
|SQL_ATTR_TXN_ISOLATION|要么[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE和SQL_ATTR_CURRENT_CATALOG可在连接之前或连接后设置，具体取决于驱动程序。 但是，可互操作的应用程序在连接前设置它们，因为某些驱动程序不支持在连接后更改它们。  
  
 [2] SQL_ATTR_ASYNC_ENABLE必须在有活动语句之前设置。  
  
 {3} 仅当连接上没有未结交易记录时，才能设置SQL_ATTR_TXN_ISOLATION。 如果数据源不支持\**ValuePtr*中指定的值，则某些连接属性支持替换类似的值。 在这种情况下，驱动程序返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02（选项值已更改）。 例如，如果*属性*为\**SQL_ATTR_PACKET_SIZE，ValuePtr*超过最大数据包大小，则驱动程序将替换最大大小。 要确定替换值，应用程序调用**SQLGetConnectAttr**。  
  
 [4] 如果在连接打开之前设置了SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE，则在调用**SQLBrowseConnect、SQLConnect**或**SQLDriverConnect**期间加载驱动程序时，驱动程序管理器将**SQLConnect**设置驱动程序的属性。 在调用**SQLBrowseConnect** **、SQLConnect**或**SQLDriverConnect**之前，驱动程序管理器不知道要连接到哪个驱动程序，也不知道驱动程序是否支持异步连接操作。 因此，驱动程序管理器始终返回SQL_SUCCESS。 但是，如果驱动程序不支持异步连接操作，则对**SQLBrowseConnect、SQLConnect**或**SQLConnect** **SQLDriverConnect**的调用将失败。  
  
 [5] 当SQL_ATTR_AUTOCOMMIT设置为 FALSE 时，如果任何 API 返回SQL_ERROR以确保事务一致性，则应用程序应调用 SQLEndTran（SQL_ROLLBACK）。  
  
 \* *ValuePtr*缓冲区中设置的信息格式取决于指定的*属性*。 **SQLSetConnectAttr**将接受两种不同格式之一的属性信息：空端字符字符串或整数值。 每个格式在属性的说明中注明。 **SQLSetConnectAttr** *的 ValuePtr*参数指向的字符串的长度为*字符串长度字节*。  
  
 如果长度由属性定义，则忽略*StringLength*参数，ODBC 2 *.x*或更早版本中引入的所有属性就是这种情况。  
  
|*特性*|*价值 Ptr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE （ODBC 1.0）|SQLUinTEGER 值。 驱动程序或数据源使用SQL_MODE_READ_ONLY作为指示，指示不支持导致发生更新的 SQL 语句不需要连接。 此模式可用于优化锁定策略、事务管理或驱动程序或数据源的其他领域。 不需要驱动程序来防止此类语句提交到数据源。 当要求驱动程序和数据源处理只读连接期间未读的 SQL 语句时，驱动程序和数据源的行为是实现定义的。 SQL_MODE_READ_WRITE为默认值。|  
|SQL_ATTR_ASYNC_DBC_EVENT （ODBC 3.8）|作为事件句柄的 SQLPOINTER 值。<br /><br /> 通过使用SQL_ATTR_ASYNC_STMT_EVENT属性调用**SQLSetConnectAttr**并指定事件句柄，启用异步函数完成通知。 **注：** 游标库不支持通知方法。 如果应用程序尝试在启用通知方法时通过 SQLSetConnectAttr 启用游标库，则会收到错误消息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE （ODBC 3.8）|启用或禁用连接句柄上所选函数的异步执行的 SQLUINTEGER 值。 有关详细信息，请参阅[异步执行（轮询方法）。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 为指定的连接相关功能启用异步操作。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （默认） 禁用指定连接相关函数的异步操作。<br /><br /> 设置SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE始终是同步的（也就是说，它永远不会返回SQL_STILL_EXECUTING）。<br /><br /> 使用SQL_ATTR_ASYNC_ENABLE启用语句操作的异步执行。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK （ODBC 3.8）|指向上下文结构的 SQLPOINTER 值。<br /><br /> 只有驱动程序管理器可以使用此属性调用驱动程序的**SQLSetStmtAttr**函数。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT （ODBC 3.8）|指向上下文结构的 SQLPOINTER 值。<br /><br /> 只有驱动程序管理器可以使用此属性调用驱动程序的**SQLSetStmtAttr**函数。|  
|SQL_ATTR_ASYNC_ENABLE （ODBC 3.0）|SQLULEN 值，用于指定是否异步执行使用指定连接上语句调用的函数：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用语句操作的连接级异步执行支持（默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 为语句操作启用连接级异步执行支持。<br /><br /> 是否可以设置此属性，无论是具有SQL_ASYNC_MODE信息类型的**SQLGetInfo**返回SQL_AM_CONNECTION还是SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD （ODBC 3.0）|只读 SQLUINTEGER 值，用于指定是否支持调用**SQLPrepare**后 IPD 的自动填充：<br /><br /> SQL_TRUE = 驱动程序支持调用**SQLPrepare**后 IPD 的自动填充。<br /><br /> SQL_FALSE = 驱动程序不支持调用**SQLPrepare**后 IPD 的自动填充。 不支持准备好的语句的服务器将无法自动填充 IPD。<br /><br /> 如果为SQL_ATTR_AUTO_IPD连接属性返回SQL_TRUE，则可以将语句属性SQL_ATTR_ENABLE_AUTO_IPD设置为打开或关闭 IPD 的自动填充。 如果SQL_ATTR_AUTO_IPDSQL_FALSE，则无法将SQL_ATTR_ENABLE_AUTO_IPD设置为SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD的默认值等于SQL_ATTR_AUTO_IPD的值。<br /><br /> 此连接属性可以由**SQLGetConnectAttr**返回，但不能由**SQLSetConnectAttr**设置。|  
|SQL_ATTR_AUTOCOMMIT （ODBC 1.0）|指定是使用自动提交模式还是手动提交模式的 SQLUINTEGER 值：<br /><br /> SQL_AUTOCOMMIT_OFF = 驱动程序使用手动提交模式，应用程序必须显式提交或回滚**SQLEndTran**的事务。<br /><br /> SQL_AUTOCOMMIT_ON = 驱动程序使用自动提交模式。 每个语句在执行后立即提交。 这是默认值。 当SQL_ATTR_AUTOCOMMIT设置为 SQL_AUTOCOMMIT_ON从手动提交模式更改为自动提交模式时，将提交连接上的任何未结事务。<br /><br /> 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要提示：** 在每次提交语句时，某些数据源都会删除访问计划并关闭连接上所有语句的游标;自动提交模式可能导致在执行每个非查询语句或为查询关闭游标时发生这种情况。 有关详细信息，请参阅[SQLGetInfo 中](../../../odbc/reference/syntax/sqlgetinfo-function.md)SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型以及[事务对游标和准备语句的影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 当批处理在自动提交模式下执行时，有两件事是可能的。 可以将整个批处理视为自动提交单元，或者批处理中的每个语句都被视为自动提交单元。 某些数据源可以同时支持这些行为，并可能提供一种选择其中一种行为的方法。 它是驱动程序定义的是批处理是否被视为可自动提交单元，还是批处理中的每个语句都是可自动提交的。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> （ODBC 3.5）|指示连接状态的只读 SQLUINTE 格值。 如果SQL_CD_TRUE，连接已丢失。 如果SQL_CD_FALSE，则连接仍然处于活动状态。|  
|SQL_ATTR_CONNECTION_TIMEOUT （ODBC 3.0）|SQLUINTEGER 值对应于等待连接上的任何请求完成，然后再返回到应用程序。 驱动程序应随时返回 SQLSTATE HYT00（超时已过期），以便在与查询执行或登录无关的情况下超时。<br /><br /> 如果*ValuePtr*等于 0（默认值），则没有超时。|  
|SQL_ATTR_CURRENT_CATALOG （ODBC 2.0）|包含数据源要使用的目录名称的字符串。 例如，在 SQL Server 中，目录是一个数据库，因此驱动程序向数据源发送**USE** _数据库_语句，其中*数据库*是\**ValuePtr*中指定的数据库。 对于单层驱动程序，目录可能是目录，因此驱动程序将其当前目录更改为 [*ValuePtr*中指定的目录》。|  
|SQL_ATTR_DBC_INFO_TOKEN（ODBC 3.8）|当[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的 （\**pbb*） 参数不等于 100 时，用于将连接信息令牌重新设置到 DBC 句柄的 SQLPOINTER 值。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN是仅设置的。 无法使用**SQLGetConnectAttr**或**SQLGetConnectOption**检索此值。 驱动程序管理器的**SQLSetConnectAttr**不会接受SQL_ATTR_DBC_INFO_TOKEN，因为应用程序不应设置此属性。<br /><br /> 如果驱动程序在设置SQL_ATTR_DBC_INFO_TOKEN后返回SQL_ERROR，则刚刚从池中获取的连接将被释放。 然后，驱动程序管理器将尝试从池中获取另一个连接。 有关详细信息[，请参阅在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|SQL_ATTR_ENLIST_IN_DTC （ODBC 3.0）|SQLPOINTER 值，用于指定在 Microsoft 组件服务协调的分布式事务中是否使用 ODBC 驱动程序。<br /><br /> 传递指定要导出到 SQL Server 的事务或SQL_DTC_DONE以结束连接的 DTC 关联的 DTC OLE 事务对象。<br /><br /> 客户端调用 Microsoft 分布式事务协调器 （MS DTC） OLE I交易分配器：：开始事务方法以开始 MS DTC 事务并创建表示事务的 MS DTC 事务对象。 然后，应用程序使用SQL_ATTR_ENLIST_IN_DTC选项调用 SQLSetConnectAttr，以将事务对象与 ODBC 连接相关联。 将在 MS DTC 事务的保护下执行所有相关的数据库活动。 应用程序使用 SQL_DTC_DONE 调用 SQLSetConnectAttr 以结束连接的 DTC 关联。 有关详细信息，请参阅 MS DTC 文档。|  
|SQL_ATTR_LOGIN_TIMEOUT （ODBC 1.0）|SQLUINTEGER 值对应于等待登录请求完成才能返回应用程序的秒数。 默认值与驱动程序相关。 如果*ValuePtr*为 0，则超时将禁用，连接尝试将无限期等待。<br /><br /> 如果指定的超时超过数据源中的最大登录超时，驱动程序将替换该值并返回 SQLSTATE 01S02（选项值已更改）。|  
|SQL_ATTR_METADATA_ID （ODBC 3.0）|SQLUINTEGER 值，用于确定如何处理目录函数的字符串参数。<br /><br /> 如果SQL_TRUE，目录函数的字符串参数将被视为标识符。 情况并不严重。 对于非分隔字符串，驱动程序删除任何尾随空格，并将字符串折叠到大写。 对于分隔字符串，驱动程序删除任何前导或尾随空格，并从字面上获取分隔符之间的任何内容。 如果这些参数之一设置为空指针，则函数将返回SQL_ERROR和 SQLSTATE HY009（无效使用空指针）。<br /><br /> 如果SQL_FALSE，目录函数的字符串参数不被视为标识符。 案件意义重大。 它们可以包含字符串搜索模式，也可以不包含字符串搜索模式，具体取决于参数。<br /><br /> 默认值为SQL_FALSE。<br /><br /> **SQLTables**的*表类型*参数 （它采用值列表） 不受此属性的影响。<br /><br /> 也可以在语句级别设置SQL_ATTR_METADATA_ID。 （它是唯一也是语句属性的连接属性。<br /><br /> 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS （ODBC 2.0）|指定驱动程序管理器如何使用 ODBC 游标库的 SQLULEN 值：<br /><br /> SQL_CUR_USE_IF_NEEDED = 驱动程序管理器仅在需要时才使用 ODBC 游标库。 如果驱动程序支持**SQLFetchScroll**中的SQL_FETCH_PRIOR选项，则驱动程序管理器将使用驱动程序的滚动功能。 否则，它使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_ODBC = 驱动程序管理器使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_DRIVER = 驱动程序管理器使用驱动程序的滚动功能。 这是默认设置。<br /><br /> 有关 ODBC 游标库的详细信息，请参阅[附录 F：ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告：** 游标库将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。|  
|SQL_ATTR_PACKET_SIZE （ODBC 2.0）|指定以字节为单位的网络数据包大小的 SQLUINTEGER 值。 **注：** 许多数据源不支持此选项，或者只能返回但不设置网络数据包大小。 <br /><br /> 如果指定大小超过最大数据包大小或小于最小数据包大小，驱动程序将替换该值并返回 SQLSTATE 01S02（选项值已更改）。<br /><br /> 如果应用程序在连接后设置数据包大小，驱动程序将返回 SQLSTATE HY011（现在无法设置属性）。|  
|SQL_ATTR_QUIET_MODE （ODBC 2.0）|窗口句柄 （HWND）。<br /><br /> 如果窗口句柄为空指针，则驱动程序不显示任何对话框。<br /><br /> 如果窗口句柄不是空指针，则应是应用程序的父窗口句柄。 这是默认值。 驱动程序使用此句柄显示对话框。 **注：** 连接属性SQL_ATTR_QUIET_MODE不适用于**SQLDriverConnect**显示的对话框。|  
|SQL_ATTR_TRACE （ODBC 1.0）|SQLUINTEGER 值告诉驱动程序管理器是否执行跟踪：<br /><br /> SQL_OPT_TRACE_OFF = 跟踪关闭（默认值）<br /><br /> SQL_OPT_TRACE_ON = 上跟踪<br /><br /> 启用跟踪时，驱动程序管理器将每个 ODBC 函数调用写入跟踪文件。 **注：** 启用跟踪时，驱动程序管理器可以从任何函数返回 SQLSTATE IM013（跟踪文件错误）。 <br /><br /> 应用程序指定具有SQL_ATTR_TRACEFILE选项的跟踪文件。 如果文件已存在，驱动程序管理器将追加到该文件。 否则，它将创建该文件。 如果跟踪处于打开，并且未指定跟踪文件，则驱动程序管理器将写入文件 SQL。在根目录中登录。<br /><br /> 应用程序可以设置变量**ODBCSharedTraceFlag**以动态启用跟踪。 然后，为当前运行的所有 ODBC 应用程序启用跟踪。 如果应用程序关闭跟踪，则仅关闭该应用程序。<br /><br /> 如果当应用程序使用*SQL_HANDLE_ENV 的句柄类型*调用**SQLAllocHandle**时，系统信息中的**Trace**关键字设置为 1，则为所有句柄启用跟踪。 它仅为称为**SQLAllocHandle**的应用程序启用。<br /><br /> 使用SQL_ATTR_TRACE*属性*调用**SQLSetConnectAttr**并不要求*连接句柄*参数有效，并且如果*连接句柄*为 NULL，则不会返回SQL_ERROR。 此属性适用于所有连接。|  
|SQL_ATTR_TRACEFILE （ODBC 1.0）|包含跟踪文件名称的 null 端接字符串。<br /><br /> SQL_ATTR_TRACEFILE属性的默认值在系统信息中使用**TraceFile**关键字指定。 有关详细信息，请参阅[ODBC 子键](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 使用 SQL_ATTR_ TRACEFILE*的属性*调用**SQLSetConnectAttr**不需要*连接句柄*参数有效，如果*连接句柄*无效，则不会返回SQL_ERROR。 此属性适用于所有连接。|  
|SQL_ATTR_TRANSLATE_LIB （ODBC 1.0）|包含包含函数**SQLDriverToDataSource**和**SQLDataSourceToDriver**的库名称的 null 端接字符串，驱动程序访问该字符串以执行字符集转换等任务。 仅当驱动程序已连接到数据源时，才能指定此选项。 此属性的设置将在整个连接中保留。 有关翻译数据的详细信息，请参阅[翻译 DLL](../../../odbc/reference/develop-app/translation-dlls.md)和[翻译 DLL 函数参考](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION （ODBC 1.0）|传递给转换 DLL 的 32 位标志值。 仅当驱动程序已连接到数据源时，才能指定此属性。 有关翻译数据的信息，请参阅翻译[DLL](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION （ODBC 1.0）|一个 32 位位掩码，用于设置当前连接的事务隔离级别。 应用程序必须调用**SQLEndTran**以提交或回滚连接上的所有打开的事务，然后再使用此选项调用**SQLSetConnectAttr。**<br /><br /> *ValuePtr*的有效值可以通过调用**SQLGetInfo**确定，*其信息类型*等于SQL_TXN_ISOLATION_OPTIONS。<br /><br /> 有关事务隔离级别的说明，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[事务隔离级别](../../../odbc/reference/develop-app/transaction-isolation-levels.md)中SQL_DEFAULT_TXN_ISOLATION信息类型的说明。|  
  
 [1] 仅当描述符是实现描述符而不是应用程序描述符时，才能异步调用这些函数。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
