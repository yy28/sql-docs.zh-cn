---
title: SQLSetConnectAttr 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4acd7ce6a33665ce3d32e42328c906aaec3049
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910387"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**设置可以控制以下方面的连接的属性。  
  
> [!NOTE]
>  详细了解驱动程序管理器映射的内容到此函数时 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，请参阅[用于向后映射替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入] 连接句柄。  
  
 *Attribute*  
 [输入]要设置，属性列在"注释"。  
  
 *ValuePtr*  
 [输入]指向要与之关联的值*属性*。 具体取决于值*特性*， *ValuePtr*将无符号的整数值或将指向以 null 结尾的字符串。 请注意，整数类型的*特性*参数可能不会修复长度，请参阅注释部分了解详细信息。  
  
 *StringLength*  
 [输入]如果*特性*是一个 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度 **ValuePtr*。 对于字符串数据，此参数应包含在字符串中的字节数。  
  
 如果*特性*是一个 ODBC 定义的属性和*ValuePtr*是一个整数*StringLength*将被忽略。  
  
 如果*特性*是一个驱动程序定义的属性，该应用程序通过设置指示特性的驱动程序管理器的性质*StringLength*参数。 *StringLength*可以具有以下值：  
  
-   如果*ValuePtr*是一个指向一个字符串，然后*StringLength*是 sql_nts; 的字符串的长度。  
  
-   如果*ValuePtr*是一个指向二进制缓冲区，则 SQL_LEN_BINARY_ATTR 将结果放置于该应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*指向的字符串或二进制字符串以外的值，即*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含一个固定长度值，则*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，根据需要。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConnectAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetConnectAttr** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
 该驱动程序可以返回 SQL_SUCCESS_WITH_INFO 以提供有关设置选项的结果的信息。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持在指定的值*ValuePtr*和替换一个相近的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08002|在使用的连接名称|*特性*参数为 SQL_ATTR_ODBC_CURSORS，和驱动程序已连接到数据源。|  
|08003|连接未打开|（数据挖掘）*特性*指定值的所需的开放连接，但*ConnectionHandle*当时不处于连接状态。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|*特性*参数为 SQL_ATTR_CURRENT_CATALOG，和结果集已挂起。|  
|25000|在本地事务中的非法操作|在尝试通过设置连接属性 SQL_ATTR_ENLIST_IN_DTC 登记分布式的事务连接 (DTC) 在本地事务中的连接。<br /><br /> 已在 DTC 中登记连接。<br /><br /> 连接已经登记分布式的事务连接中，通过将 SQL_ATTR_AUTOCOMMIT 设置为 SQL_AUTOCOMMIT_OFF 启动本地事务。|  
|3D000|目录名称无效|*特性*参数为 SQL_CURRENT_CATALOG，和指定的目录名称无效。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*ConnectionHandle*。 **SQLSetConnectAttr**调用函数，和之前执行完毕[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，，然后**SQLSetConnectAttr**上再次调用函数*ConnectionHandle*。<br /><br /> 或者， **SQLSetConnectAttr**调用函数，和之前执行完毕**SQLCancelHandle**上调用了*ConnectionHandle*来自不同线程中一个多线程应用程序。|  
|HY009|使用空指针无效|*特性*参数标识的字符串值，所需的连接属性和*ValuePtr*参数是空指针。|  
|HY010|函数序列错误|(DM) 的调用以异步方式执行的函数*StatementHandle*与关联*ConnectionHandle*和仍在执行时**SQLSetConnectAttr**调用。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *ConnectionHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*ConnectionHandle* ，并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*与相关联*ConnectionHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） **SQLBrowseConnect**曾为*ConnectionHandle*和返回 SQL_NEED_DATA。 此函数调用之前**SQLBrowseConnect**返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|HY011|现在无法设置属性|*特性*参数为 SQL_ATTR_TXN_ISOLATION，和一个事务处于打开状态。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY024|属性值无效|给出指定*特性*值，在指定了无效的值*ValuePtr*。 （驱动程序管理器将返回仅适用于连接和语句属性接受一组离散的值，例如 SQL_ATTR_ACCESS_MODE 或 sql_attr_async_enable 设置此 SQLSTATE。 对于所有其他连接和语句属性，该驱动程序必须验证中指定的值*ValuePtr*。)<br /><br /> *特性*参数为 SQL_ATTR_TRACEFILE 或 SQL_ATTR_TRANSLATE_LIB，并*ValuePtr*是空字符串。|  
|HY090|字符串或缓冲区长度无效|*（数据挖掘） \*ValuePtr*是一个字符串，并*StringLength*参数为小于 0，但不是 sql_nts;。|  
|HY092|属性/选项标识符无效|(DM) 的参数指定的值*特性*对 ODBC 驱动程序支持的版本无效。<br /><br /> (DM) 的参数指定的值*特性*是只读的属性。|  
|HY114|驱动程序不支持连接级别异步函数执行|(DM) 应用程序尝试在启用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 与驱动程序不支持异步连接操作的异步函数执行。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|不能同时启用游标库和识别驱动程序的池|有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*特性*是有效的 ODBC 连接或驱动程序支持版本的 ODBC 语句属性，但不是受驱动程序。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*ConnectionHandle*不支持该函数。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为连接指定的 DLL。 可以返回此错误时，才*特性*是 SQL_ATTR_TRANSLATE_LIB。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|（在已连接） 后设置 SQL_ATTR_ASYNC_DBC_EVENT 但驱动程序不支持异步通知。|  
  
 当*特性*是一个语句的属性， **SQLSetConnectAttr**可以返回返回的任何 SQLSTATEs **SQLSetStmtAttr**。  
  
## <a name="comments"></a>注释  
 有关连接属性的常规信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 在此部分; 更高版本中的表中显示当前定义的属性和 ODBC 介绍它们的版本应将定义更多属性以充分利用不同的数据源。 由 ODBC; 保留一系列属性驱动程序开发人员必须保留供从 Open Group 自己特定于驱动程序使用的值。  
  
> [!NOTE]
>  设置在连接级别的语句属性通过调用的能力**SQLSetConnectAttr** ODBC 3 中已弃用 *.x*。 ODBC 3 *.x*应用程序应永远不会在连接级别设置语句属性。 ODBC 3 *.x*语句属性不能设置在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句属性，可以是设置在连接级别或语句级别。  
> 
>  ODBC 3 *.x*驱动程序仅需要支持此功能，如果他们应适用于 ODBC 2 *.x*设置 ODBC 2 应用程序都 *.x*在连接级别的语句选项。 有关详细信息，请参阅[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附录 g:为了向后兼容的驱动程序指南。  
  
 应用程序可以调用**SQLSetConnectAttr**分配和释放该连接的时间之间的任何时候。 已成功设置应用程序在连接的所有连接和语句属性都保存直到**SQLFreeHandle**连接上调用。 例如，如果应用程序调用**SQLSetConnectAttr**之前连接到数据源，该属性仍然存在即使**SQLSetConnectAttr**时应用程序连接到驱动程序中失败数据源;如果应用程序设置特定于驱动程序的属性，该属性仍然存在，即使应用程序连接到不同驱动程序在连接上。  
  
 只能在已建立连接; 之前，可以设置某些连接属性建立连接时，才可以设置其他人。 下表指示之前或之后建立连接必须设置这些连接属性。 *任一*指示之前或之后连接，可以设置该属性。  
  
|特性|设置之前或之后连接？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之后|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|是 [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之后|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之后|  
|SQL_ATTR_ASYNC_ENABLE|任一 [2]|  
|SQL_ATTR_AUTO_IPD|之前或之后|  
|SQL_ATTR_AUTOCOMMIT|是 [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之后|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|早于|  
|SQL_ATTR_METADATA_ID|之前或之后|  
|SQL_ATTR_ODBC_CURSORS|早于|  
|SQL_ATTR_PACKET_SIZE|早于|  
|SQL_ATTR_QUIET_MODE|之前或之后|  
|SQL_ATTR_TRACE|之前或之后|  
|SQL_ATTR_TRACEFILE|之前或之后|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE SQL_ATTR_CURRENT_CATALOG 设置和之前或之后连接，具体取决于驱动程序。 但是，可互操作应用程序设置这些连接之前由于某些驱动程序不支持更改这些连接后。  
  
 [活动语句之前，必须设置 sql_attr_async_enable 设置 2]。  
  
 [可以设置 3] SQL_ATTR_TXN_ISOLATION，仅当没有在连接上打开的事务。 如果数据源不支持在指定的值，有些连接属性支持类似的值替换成\* *ValuePtr*。 在这种情况下，驱动程序将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。 例如，如果*特性*是 SQL_ATTR_PACKET_SIZE 和\* *ValuePtr*超过最大数据包大小，该驱动程序替换的最大大小。 若要确定被替换的值，应用程序调用**SQLGetConnectAttr**。  
  
 [在调用期间加载驱动程序 4] 如果在打开连接，则前设置 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE，驱动程序管理器将设置驱动程序的属性**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**。 对调用之前**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**，驱动程序管理器不知道要连接到的驱动程序，但不知道是否驱动程序支持异步连接操作。 因此，驱动程序管理器始终返回 SQL_SUCCESS。 但是，如果驱动程序不支持异步连接操作，在调用**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**将失败。  
  
 [5] 当 SQL_ATTR_AUTOCOMMIT 设置为 FALSE 时，应用程序应调用 SQLEndTran(SQL_ROLLBACK)，如果任何 API 返回 SQL_ERROR，以确保事务一致性。  
  
 在中设置的信息的格式\* *ValuePtr*缓冲区取决于指定*特性*。 **SQLSetConnectAttr**将接受两个不同的格式之一的属性信息： 以 null 结尾的字符串或整数值。 该特性的描述中记录了每个消息格式。 指向的字符串*ValuePtr*的参数**SQLSetConnectAttr**具有长度*StringLength*字节。  
  
 *StringLength* ，将忽略参数长度定义属性，如果在 ODBC 2 中引入的所有属性的情况一样 *.x*或更早版本。  
  
|*Attribute*|*ValuePtr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|一个 SQLUINTEGER 值。 SQL_MODE_READ_ONLY 用作由驱动程序或数据源连接不需要支持会导致更新发生的 SQL 语句的指示器。 此模式可用于优化锁定的策略、 事务管理或根据驱动程序或数据源的其他区域。 该驱动程序不需要以防止此类语句被提交到数据源。 驱动程序和数据源时需要处理不是只读的只读连接期间的 SQL 语句的行为是实现定义的。 默认值为 SQL_MODE_READ_WRITE。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|一个 SQLPOINTER 值，该值是事件的句柄。<br /><br /> 异步函数完成通知的启用通过调用**SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 属性和指定的事件句柄。 **注意：** 游标库不支持的通知方法。 如果它尝试启用游标库通过 SQLSetConnectAttr，启用通知方法时，应用程序将收到错误消息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|一个 SQLUINTEGER 值，该值启用或禁用连接句柄上的所选函数的异步执行。 有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 启用异步操作，用于指定与连接相关的函数。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （默认值） 禁用异步操作，用于指定与连接相关的函数。<br /><br /> 设置 sql_attr_async_dbc_functions_enable 始终同步 （即，它将永远不会返回 SQL_STILL_EXECUTING）。<br /><br /> 异步执行的语句操作启用了 sql_attr_async_enable 设置。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|指向上下文结构 SQLPOINTER 值。<br /><br /> 驱动程序管理器可以调用的驱动程序仅**SQLSetStmtAttr**具有此特性的函数。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|指向上下文结构 SQLPOINTER 值。<br /><br /> 驱动程序管理器可以调用的驱动程序仅**SQLSetStmtAttr**具有此特性的函数。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|一个 sqlulen 生成值，该值指定是否以异步方式执行与指定连接上的语句时调用的函数：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用连接级别的异步执行语句对操作的支持 （默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 启用连接级别的异步执行语句对操作的支持。<br /><br /> 此属性可以设置是否**SQLGetInfo** SQL_ASYNC_MODE 信息类型返回 SQL_AM_CONNECTION 或 SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|一个只读的 SQLUINTEGER 值，该值指定是否对的调用后自动填充 IPD **SQLPrepare**支持：<br /><br /> SQL_TRUE = 到调用后的自动填充 IPD **SQLPrepare**驱动程序支持。<br /><br /> SQL_FALSE = 到调用后的自动填充 IPD **SQLPrepare**驱动程序不支持。 服务器不支持准备的语句不能以自动填充 IPD。<br /><br /> 如果为 SQL_ATTR_AUTO_IPD 连接属性返回 SQL_TRUE，则可以设置语句属性 SQL_ATTR_ENABLE_AUTO_IPD 若要打开或关闭自动填充 IPD。 如果 SQL_ATTR_AUTO_IPD，SQL_FALSE SQL_ATTR_ENABLE_AUTO_IPD 不能设置为 SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD 的默认值等于 SQL_ATTR_AUTO_IPD 的值。<br /><br /> 可以通过返回此连接属性**SQLGetConnectAttr**但不能通过设置**SQLSetConnectAttr**。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|一个 SQLUINTEGER 值，该值指定是否使用自动提交或手动提交模式下：<br /><br /> SQL_AUTOCOMMIT_OFF = 驱动程序将使用手动提交模式和应用程序必须显式提交或回滚的事务**SQLEndTran**。<br /><br /> Sql_autocommit_on，否则 = 驱动程序使用自动提交模式。 每个语句都在提交后执行。 这是默认设置。 SQL_ATTR_AUTOCOMMIT 设置为 sql_autocommit_on，否则，若要从手动提交模式更改为自动提交模式时，在连接上任何打开的事务将提交。<br /><br /> 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要提示：** 某些数据源删除访问计划，并关闭的语句都在提交; 每次在连接上的所有语句的游标自动提交模式下可能会导致这种情况发生在执行每个 nonquery 语句后或游标关闭查询时。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)并[对游标和准备的语句影响的事务](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 在自动提交模式下执行批处理时，可能会出现两件事情。 Autocommitable 单元，可将其视为整个批处理或批处理中的每个语句视为 autocommitable 单元。 某些数据源可以支持这两个这些行为，并且可能会提供一种方法选择一个或另一个。 它是驱动程序定义批处理被视为 autocommitable 单元或在批处理中每个单独的语句是否 autocommitable。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|只读 SQLUINTEGER 值，该值指示连接的状态。 如果 SQL_CD_TRUE，连接已丢失。 如果 SQL_CD_FALSE，连接仍处于活动状态。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|一个 SQLUINTEGER 值对应的任何请求完成，然后返回到应用程序在连接上等待的秒数。 该驱动程序应返回 SQLSTATE HYT00 （超时已过期） 随时是可能的情况下，未与查询执行或登录名关联的超时。<br /><br /> 如果*ValuePtr*是等于 0 （默认值），没有任何超时。|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|包含要由数据源的目录的名称的字符串。 例如，在 SQL Server 中，目录是一个数据库，因此驱动程序发送**使用**_数据库_语句与数据源，其中*数据库*中指定的数据库\* *ValuePtr*。 单层驱动程序的目录可能是一个目录，因此驱动程序更改其当前目录中指定的目录为 **ValuePtr*。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|用来设置的 SQLPOINTER 值返回到 DBC 的连接信息令牌处理何时[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的 (\**pRating*) 参数不等于 100。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 是只设置的。 不能使用**SQLGetConnectAttr**或**SQLGetConnectOption**来检索此值。 驱动程序管理器**SQLSetConnectAttr** SQL_ATTR_DBC_INFO_TOKEN，因为应用程序不应设置此属性也不会接受。<br /><br /> 如果驱动程序设置 SQL_ATTR_DBC_INFO_TOKEN 后返回 SQL_ERROR，只需从池中获取的连接会被释放。 然后，驱动程序管理器将尝试从该池中获取另一个连接。 请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)有关详细信息。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|一个 SQLPOINTER 值，该值指定是否在由 Microsoft 组件服务进行协调的分布式事务中使用的 ODBC 驱动程序。<br /><br /> 传递一个 DTC OLE 事务对象，指定要将导出到 SQL Server 或 SQL_DTC_DONE 结束连接的 DTC 关联的事务。<br /><br /> 客户端调用 Microsoft 分布式事务处理协调器 (MS DTC) OLE itransactiondispenser:: Begintransaction 方法来开始执行 MS DTC 事务，并创建一个表示事务的 MS DTC 事务对象。 然后，应用程序使用 ODBC 连接相关联的事务对象的 SQL_ATTR_ENLIST_IN_DTC 选项调用 SQLSetConnectAttr。 将在 MS DTC 事务的保护下执行所有相关的数据库活动。 若要结束连接的 DTC 关联应用程序调用使用 SQL_DTC_DONE SQLSetConnectAttr。 有关详细信息，请参阅 MS DTC 文档。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|一个 SQLUINTEGER 值对应于要等待的时间完成，然后返回到应用程序的登录请求的秒数。 默认值为驱动程序相关。 如果*ValuePtr*为 0，禁用超时且连接尝试将无限期等待。<br /><br /> 如果指定的超时时间超过了数据源中的最大登录超时值，该驱动程序替代该值，并返回 SQLSTATE 01S02 （选项值已更改）。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|SQLUINTEGER 值，该值确定如何处理目录函数将字符串参数。<br /><br /> 如果 SQL_TRUE，目录函数的字符串自变量被视为标识符。 这种情况并不重要。 对于分隔字符串，该驱动程序中删除任何尾随空格和字符串折叠为大写。 对于带分隔符的字符串，该驱动程序中删除任何前导或尾随空格和按原义采用任何分隔符之间是。 如果其中一个参数设置为 null 指针，该函数返回 SQL_ERROR 并且 SQLSTATE HY009 （null 指针的使用无效）。<br /><br /> 如果 SQL_FALSE，目录函数将字符串参数不被视为标识符。 这种情况很重要。 它们可以包含字符串的搜索模式，取决于参数。<br /><br /> 默认值为 SQL_FALSE。<br /><br /> *TableType*的参数**SQLTables**，其将一系列值，不会影响此属性。<br /><br /> 此外可以在语句级别上设置 SQL_ATTR_METADATA_ID。 （它是唯一的连接属性，也是语句属性。）<br /><br /> 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Sqlulen 生成值，该值指定驱动程序管理器如何使用 ODBC 游标库：<br /><br /> SQL_CUR_USE_IF_NEEDED = 的驱动程序管理器中使用 ODBC 游标库，仅当需要它。 如果该驱动程序支持中的 SQL_FETCH_PRIOR 选项**SQLFetchScroll**，驱动程序管理器使用的驱动程序的滚动功能。 否则，它使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_ODBC = 的驱动程序管理器中使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_DRIVER = 的驱动程序管理器中使用的驱动程序的滚动功能。 这是默认设置。<br /><br /> 有关 ODBC 游标库的详细信息，请参阅[附录 f:ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 警告：  将 Windows 的未来版本中删除该游标库。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|SQLUINTEGER 值，该值以字节为单位指定的网络数据包大小。 **注意：** 多个数据源也不支持此选项，或仅可以返回，但未设置网络数据包大小。 <br /><br /> 如果指定的大小超出了最大数据包大小或小于最小数据包大小，该驱动程序替代该值，并返回 SQLSTATE 01S02 （选项值已更改）。<br /><br /> 如果已建立连接后，应用程序设置数据包大小，则驱动程序将返回 SQLSTATE HY011 （属性不能立即设置）。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|窗口句柄 (HWND)。<br /><br /> 窗口句柄是否为 null 指针，该驱动程序不显示任何对话框。<br /><br /> 如果窗口句柄不是 null 指针，它应该是应用程序的父窗口句柄。 这是默认设置。 该驱动程序使用此句柄来显示对话框。 **注意：** SQL_ATTR_QUIET_MODE 连接属性不适用于显示的对话框**SQLDriverConnect**。|  
|SQL_ATTR_TRACE (ODBC 1.0)|告知驱动程序管理器是否执行跟踪 SQLUINTEGER 值：<br /><br /> SQL_OPT_TRACE_OFF 跟踪 = off （默认）<br /><br /> SQL_OPT_TRACE_ON = on 的跟踪<br /><br /> 在跟踪时，驱动程序管理器将写入到跟踪文件的每个 ODBC 函数调用。 **注意：** 当跟踪时，驱动程序管理器可返回 SQLSTATE IM013 （跟踪文件错误） 从任何函数。 <br /><br /> 应用程序使用 SQL_ATTR_TRACEFILE 选项指定跟踪文件。 如果该文件已存在，则驱动程序管理器将追加到文件。 否则，它将创建文件。 如果跟踪已打开，并指定不跟踪文件，驱动程序管理器将写入到 SQL 的文件。日志的根目录中。<br /><br /> 应用程序可以设置该变量**ODBCSharedTraceFlag**表示启用动态跟踪。 然后为当前正在运行的所有 ODBC 应用程序启用跟踪。 如果应用程序将关闭跟踪，它处于关闭状态仅对该应用程序。<br /><br /> 如果**跟踪**中的系统信息的关键字设置为 1，当应用程序调用**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_ENV，为所有启用跟踪句柄。 仅对调用应用程序启用**SQLAllocHandle**。<br /><br /> 调用**SQLSetConnectAttr**与*特性*的 SQL_ATTR_TRACE 不要求*ConnectionHandle*参数是有效并且不会返回 SQL_ERROR，如果*ConnectionHandle*为 NULL。 此特性应用于所有连接。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|包含的跟踪文件的名称的以 null 结尾的字符字符串。<br /><br /> 使用指定 SQL_ATTR_TRACEFILE 属性的默认值**TraceFile**系统信息中的关键字。 有关详细信息，请参阅[ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 调用**SQLSetConnectAttr**与*特性*不需要的 SQL_ATTR_ TRACEFILE *ConnectionHandle*参数有效并且不会返回 SQL_ERROR，如果*ConnectionHandle*无效。 此特性应用于所有连接。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|包含一个库，包含函数的名称的以 null 结尾的字符字符串**SQLDriverToDataSource**并**SQLDataSourceToDriver**驱动程序访问以执行以下任务字符集转译。 此选项可能仅在指定是否驱动程序已连接到数据源。 在连接中，该属性的设置将保持原样。 有关将数据转换的详细信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)并[转换 DLL 函数引用](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|一个 32 位标志值，该值传递给转换 DLL。 此属性可以是仅在指定是否驱动程序已连接到数据源。 有关将数据转换的信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|一个 32 位的位掩码设置当前连接的事务隔离级别。 应用程序必须调用**SQLEndTran**提交或回滚所有打开的事务上的连接，然后再调用**SQLSetConnectAttr**使用此选项。<br /><br /> 有效值*ValuePtr*可确定通过调用**SQLGetInfo**与*信息类型*等于 SQL_TXN_ISOLATION_OPTIONS。<br /><br /> 有关事务隔离级别的说明，请参阅 SQL_DEFAULT_TXN_ISOLATION 信息类型中的说明[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)并[事务隔离级别](../../../odbc/reference/develop-app/transaction-isolation-levels.md)。|  
  
 [仅当该描述符是实现描述符，而不是应用程序描述符，可以以异步方式调用 1] 这些函数。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
