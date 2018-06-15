---
title: SQLSetConnectAttr 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 83
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd64bb19ed9bc7beed48e9920b61139ae791d983
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923552"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**设置控制方面的连接的属性。  
  
> [!NOTE]  
>  有关什么驱动程序管理器时，将映射此函数可对 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，请参阅[映射用于向后的替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *属性*  
 [输入]要设置，属性列在"注释"。  
  
 *ValuePtr*  
 [输入]指向要与之关联的值*属性*。 根据值*属性*， *ValuePtr*将无符号的整数值或将指向以 null 结尾的字符串。 请注意，整型类型*属性*自变量可能不会修复长度，请参阅备注部分以了解详细信息。  
  
 *stringLength*  
 [输入]如果*属性*是 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度 **ValuePtr*。 对于字符串数据，此自变量应包含在字符串中的字节数。  
  
 如果*属性*是 ODBC 定义的属性和*ValuePtr*是一个整数， *StringLength*将被忽略。  
  
 如果*属性*是驱动程序定义的属性，应用程序通过设置指示属性到驱动程序管理器的性质*StringLength*自变量。 *StringLength*可以具有下列值：  
  
-   如果*ValuePtr*然后是指向字符串， *StringLength*是字符串或 sql_nts 以的长度。  
  
-   如果*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定长度的值，然后*StringLength*为 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，与相应。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConnectAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetConnectAttr**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
 该驱动程序可以返回 SQL_SUCCESS_WITH_INFO 提供的结果的设置选项的信息。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持在指定的值*ValuePtr*和替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08002|连接名称已在使用|*属性*自变量为 SQL_ATTR_ODBC_CURSORS，和驱动程序已连接到数据源。|  
|08003|连接未打开|(DM)*属性*指定值，需要打开的连接，但*ConnectionHandle*当时不处于已连接状态。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|*属性*参数 SQL_ATTR_CURRENT_CATALOG，且结果集为挂起。|  
|25000|本地事务中的非法操作|连接正在尝试通过设置连接属性 SQL_ATTR_ENLIST_IN_DTC 登记分布式的事务连接 (DTC) 中时的一个本地事务。<br /><br /> 已在 DTC 中登记连接。<br /><br /> 已经在分布式的事务的连接中登记连接，通过将 SQL_ATTR_AUTOCOMMIT 设置为 SQL_AUTOCOMMIT_OFF 启动本地事务。|  
|3D000|无效的目录名称|*属性*参数 SQL_CURRENT_CATALOG，且指定的目录名称为无效。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*ConnectionHandle*。 **SQLSetConnectAttr**调用函数，并且它之前完成执行， [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，，然后**SQLSetConnectAttr**函数上调用了再次*ConnectionHandle*。<br /><br /> 或者， **SQLSetConnectAttr**调用函数，并且它之前完成执行， **SQLCancelHandle**上调用了*ConnectionHandle*来自中的不同线程一个多线程应用程序。|  
|HY009|不允许使用 null 指针|*属性*自变量标识所需的字符串值，连接属性和*ValuePtr*自变量是空指针。|  
|HY010|函数序列错误|(DM) 以异步方式执行的函数曾为*StatementHandle*与关联*ConnectionHandle*和仍在执行时**SQLSetConnectAttr**调用。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*ConnectionHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**与关联的语句句柄之一调用*ConnectionHandle*并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*与关联*ConnectionHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) **SQLBrowseConnect**曾为*ConnectionHandle*并返回 SQL_NEED_DATA。 此函数调用之前**SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS 返回。|  
|HY011|现在无法设置属性|*属性*自变量为 SQL_ATTR_TXN_ISOLATION，和一个事务处于打开状态。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY024|无效属性值|给出指定*属性*中值，指定无效的值是*ValuePtr*。 （驱动程序管理器返回仅适用于连接和语句属性接受一组离散的值，如 SQL_ATTR_ACCESS_MODE 或 SQL_ATTR_ASYNC_ENABLE 此 SQLSTATE。 对于所有其他连接和语句属性，该驱动程序必须验证中指定的值*ValuePtr*。)<br /><br /> *属性*参数为 SQL_ATTR_TRACEFILE 或 SQL_ATTR_TRANSLATE_LIB，和*ValuePtr*是空字符串。|  
|HY090|字符串或缓冲区长度无效|*(DM) \*ValuePtr*是一个字符串，与*StringLength*自变量为小于 0，但未 sql_nts 以。|  
|HY092|属性/选项标识符无效|(DM) 值的参数的指定*属性*对 ODBC 驱动程序支持的版本无效。<br /><br /> (DM) 值的参数的指定*属性*只读属性。|  
|HY114|驱动程序不支持连接级别异步函数执行|(DM) 应用程序尝试以启用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 与驱动程序不支持异步连接操作的异步函数执行。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|游标库和识别驱动程序的池不能在同一时间的情况下启用|有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*属性*是有效的 ODBC 连接或语句属性版本的 ODBC 驱动程序支持，但由驱动程序不支持。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*ConnectionHandle*不支持该函数。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为连接指定的 DLL。 可以返回此错误仅当*属性*是 SQL_ATTR_TRANSLATE_LIB。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|（后建立该连接时） 设置 SQL_ATTR_ASYNC_DBC_EVENT 但驱动程序不支持异步通知。|  
  
 当*属性*是语句属性， **SQLSetConnectAttr**可以返回由任何 SQLSTATEs **SQLSetStmtAttr**。  
  
## <a name="comments"></a>注释  
 有关连接属性的常规信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 本节后面; 表中显示当前定义的特性和引入这些 ODBC 的版本应将定义更多属性以利用不同数据源。 ODBC; 保留一组属性驱动程序开发人员必须保留用于 Open Group 自己特定于驱动程序使用的值。  
  
> [!NOTE]  
>  能够在连接级别设置语句特性，通过调用**SQLSetConnectAttr** ODBC 3 中已弃用 *.x*。 ODBC 3 *.x*应用应永远不会将语句属性设置在连接级别。 ODBC 3 *.x*语句属性不能在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句属性，可以设置在连接级别或语句级上设置。  
>   
>  ODBC 3 *.x*驱动程序仅需要支持此功能，如果它们应使用 ODBC 2 *.x*应用程序将 ODBC 2 设置 *.x*在连接级别的语句选项。 有关详细信息，请参阅[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
 应用程序可以调用**SQLSetConnectAttr**分配和释放连接在任何时间之间的时间。 成功地设置连接应用程序的所有连接和语句属性都保留直到**SQLFreeHandle**连接上调用。 例如，如果应用程序调用**SQLSetConnectAttr**之前连接到数据源，该属性仍然存在即使**SQLSetConnectAttr**失败驱动程序中，当应用程序连接到数据源;如果应用程序设置特定于驱动程序的属性，该属性仍然存在，即使应用程序连接到不同的驱动程序连接上。  
  
 只能在已建立连接; 之前，才可以设置某些连接属性只有在建立连接后，才可以设置其他人。 下表指示之前或之后在建立连接必须设置这些连接属性。 *任一*指示之前或之后连接，可以设置该属性。  
  
|Attribute|设置之前或之后连接？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|是 [1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之后|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|任一 [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之后|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之后|  
|SQL_ATTR_ASYNC_ENABLE|任一 [2]|  
|SQL_ATTR_AUTO_IPD|之前或之后|  
|SQL_ATTR_AUTOCOMMIT|是 [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之后|  
|SQL_ATTR_CURRENT_CATALOG|是 [1]|  
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
|SQL_ATTR_TXN_ISOLATION|任一 [3]|  
  
 [可以设置 1] SQL_ATTR_ACCESS_MODE 和 SQL_ATTR_CURRENT_CATALOG 之前, 或之后连接，具体取决于该驱动程序。 但是，可互操作的应用程序设置它们在连接之前由于某些驱动程序不支持更改这些连接后。  
  
 [活动语句之前，必须设置 SQL_ATTR_ASYNC_ENABLE 2]。  
  
 [可以设置 3] SQL_ATTR_TXN_ISOLATION，仅在没有连接上没有打开的事务。 某些连接特性支持类似的值替换，如果数据源不支持在指定的值\* *ValuePtr*。 在这种情况下，该驱动程序返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （选项值已更改）。 例如，如果*属性*是 SQL_ATTR_PACKET_SIZE 和\* *ValuePtr*超过最大的数据包大小，该驱动程序替换的最大大小。 若要确定被替换的值，应用程序调用**SQLGetConnectAttr**。  
  
 [4] 如果 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 设置之前连接处于打开状态，驱动程序加载在调用时，驱动程序管理器将设置驱动程序的属性**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**。 调用之前**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**，驱动程序管理器不知道要连接到的驱动程序，而不知道是否驱动程序支持异步连接操作。 因此，驱动程序管理器始终返回 SQL_SUCCESS。 但是，以防该驱动程序不支持异步连接操作，对的调用**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**将失败。  
  
 [5] 当 SQL_ATTR_AUTOCOMMIT 设置为 FALSE，则应用程序应调用 SQLEndTran(SQL_ROLLBACK)，如果任何 API 返回 SQL_ERROR 以确保事务一致性。  
  
 在中设置的信息的格式\* *ValuePtr*缓冲区取决于指定*属性*。 **SQLSetConnectAttr**将接受两个不同的格式之一的特性信息： 以 null 结尾的字符串或整数值。 每个格式将其记录在该特性的说明。 字符字符串的指向*ValuePtr*参数**SQLSetConnectAttr**具有长度为*StringLength*字节。  
  
 *StringLength*将忽略自变量长度定义的属性，如果是 ODBC 2 中引入的所有特性如此 *.x*或更早版本。  
  
|*属性*|*ValuePtr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|一个 SQLUINTEGER 值。 SQL_MODE_READ_ONLY 用作由驱动程序或数据源连接不需要支持导致更新自动进行的 SQL 语句的指示器。 此模式可用于优化锁定策略、 事务管理或根据驱动程序或数据源的其他区域。 该驱动程序不需要阻止此类语句被提交到数据源。 驱动程序和数据源时要求处理不是只读的只读连接期间的 SQL 语句的行为是实现定义的。 默认值为 SQL_MODE_READ_WRITE。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|SQLPOINTER 值，一个事件句柄。<br /><br /> 异步函数完成通知的启用通过调用**SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 属性和指定的事件句柄。 **注意：** 游标库不支持通知方法。 如果它尝试启用通过 SQLSetConnectAttr，光标库，启用通知方法后，应用程序将收到错误消息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|一个 SQLUINTEGER 值，启用或禁用连接句柄上的所选函数的异步执行。 有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 启用异步操作的指定与连接相关的函数。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （默认值） 禁用异步操作的指定与连接相关的函数。<br /><br /> 设置 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 始终是同步的 （即，它将永远不会返回 SQL_STILL_EXECUTING）。<br /><br /> 异步执行的语句操作是使用 SQL_ATTR_ASYNC_ENABLE 启用的。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|指向上下文结构 SQLPOINTER 值。<br /><br /> 仅驱动程序管理器可以调用驾**SQLSetStmtAttr**使用此特性的函数。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|指向上下文结构 SQLPOINTER 值。<br /><br /> 仅驱动程序管理器可以调用驾**SQLSetStmtAttr**使用此特性的函数。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|SQLULEN 值，该值指定是否以异步方式执行使用一条语句指定连接上调用的函数：<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用连接级别的异步执行支持语句操作 （默认值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 为语句操作启用连接级别的异步执行支持。<br /><br /> 此属性可以设置是否**SQLGetInfo** SQL_ASYNC_MODE 信息类型返回 SQL_AM_CONNECTION 或 SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|一个只读的 SQLUINTEGER 值，指定是否自动填充的 IPD 后调用**SQLPrepare**支持：<br /><br /> SQL_TRUE = 的 IPD 后调用的自动填充**SQLPrepare**由驱动程序支持。<br /><br /> SQL_FALSE = 的 IPD 后调用的自动填充**SQLPrepare**驱动程序不支持。 不支持准备的语句的服务器将不能自动填充 IPD。<br /><br /> 如果 SQL_TRUE 返回 SQL_ATTR_AUTO_IPD 连接属性，可以设置语句属性 SQL_ATTR_ENABLE_AUTO_IPD 为打开或关闭的 IPD 自动填充。 如果 SQL_ATTR_AUTO_IPD，SQL_FALSE SQL_ATTR_ENABLE_AUTO_IPD 不能设置为 SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD 的默认值等于 SQL_ATTR_AUTO_IPD 的值。<br /><br /> 此连接属性可以由**SQLGetConnectAttr**但不能通过设置**SQLSetConnectAttr**。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|SQLUINTEGER 值，该值指定是否使用自动或手动提交模式：<br /><br /> SQL_AUTOCOMMIT_OFF = 驱动程序将使用手动提交模式下，和应用程序必须显式提交或回滚的事务**SQLEndTran**。<br /><br /> SQL_AUTOCOMMIT_ON = 驱动程序使用自动提交模式。 立即执行后才能提交每个语句。 这是默认设置。 当 SQL_ATTR_AUTOCOMMIT 设置为 SQL_AUTOCOMMIT_ON 从手动提交模式更改为自动提交模式时，连接上的打开任何事务将提交。<br /><br /> 有关详细信息，请参阅[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要说明：** 某些数据源删除访问计划关闭的所有语句，在每次连接上游标语句被提交; 自动提交模式可能会导致执行每个 nonquery 语句后，或当光标位于时执行此操作关闭查询。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[游标和准备的语句上的事务影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 当在自动模式下执行批处理时，可能会出现以下两项操作。 可作为 autocommitable 单元视为整个批处理或批处理中的每个语句视为 autocommitable 单元。 某些数据源可以支持这两种这些行为，并且可能会提供一种方法选择一个或另一个。 它是驱动程序定义是否将一批视为 autocommitable 单元或批处理中每个单独的语句是否 autocommitable。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|一个只读 SQLUINTEGER 值，该值指示连接的状态。 如果 SQL_CD_TRUE，连接已丢失。 如果 SQL_CD_FALSE，连接仍处于活动状态。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|一个 SQLUINTEGER 值对应于为任何请求完成，然后返回到应用程序连接上等待的秒数。 该驱动程序应返回 SQLSTATE HYT00 （超时） 随时是可能的情况下，未与查询执行或登录名关联的超时。<br /><br /> 如果*ValuePtr*是等于 0 （默认值），没有任何超时。|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|包含要使用数据源的目录名称的字符串。 例如，在 SQL Server 中，该目录是一个数据库，所以，该驱动程序会发送**使用***数据库*语句与数据源，其中*数据库*中指定数据库\* *ValuePtr*。 单层驱动程序，该目录可能是一个目录，因此驱动程序更改其当前目录中指定的目录为 **ValuePtr*。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|用于设置 SQLPOINTER 值返回到 DBC 连接信息令牌处理时[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的 (\**pRating*) 参数不等于 100。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 是仅。 不能使用**SQLGetConnectAttr**或**SQLGetConnectOption**检索此值。 驱动程序管理器的**SQLSetConnectAttr**将不接受 SQL_ATTR_DBC_INFO_TOKEN，因为应用程序不应设置此属性。<br /><br /> 如果驱动程序设置 SQL_ATTR_DBC_INFO_TOKEN 后返回 SQL_ERROR，只需从池中获取的连接会被释放。 驱动程序管理器将尝试从池中获取另一个连接。 请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)有关详细信息。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|一个 SQLPOINTER 值，指定是否在由 Microsoft 组件服务来协调的分布式事务中使用 ODBC 驱动程序。<br /><br /> 传递的 DTC OLE 事务对象，指定要将导出到 SQL Server 或 SQL_DTC_DONE 结束连接的 DTC 关联的事务。<br /><br /> 客户端调用的 Microsoft 分布式事务处理协调器 (MS DTC) OLE ITransactionDispenser::BeginTransaction 方法开始 MS DTC 事务，并创建一个表示事务的 MS DTC 事务对象。 然后，应用程序使用 ODBC 连接相关联的事务对象的 SQL_ATTR_ENLIST_IN_DTC 选项调用 SQLSetConnectAttr。 将在 MS DTC 事务的保护下执行所有相关的数据库活动。 在应用程序调用 SQLSetConnectAttr 与 SQL_DTC_DONE 结束连接的 DTC 关联。 有关详细信息，请参阅 MS DTC 文档。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|一个 SQLUINTEGER 值对应的要等待的时间完成，然后返回到应用程序的登录请求的秒数。 默认值为驱动程序相关。 如果*ValuePtr*为 0、 禁用超时和连接尝试将无限期等待。<br /><br /> 如果指定的超时时间超过数据源中的最大登录超时，该驱动程序替代此值，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|一个 SQLUINTEGER 值，确定如何处理目录函数的字符串自变量。<br /><br /> 如果 SQL_TRUE，目录函数的字符串自变量将被视为标识符。 这种情况并不重要。 对于 nondelimited 字符串，该驱动程序中删除任何尾随空格和字符串折叠为大写形式。 分隔字符串的驱动程序中移除任何前导空格或尾随空格和按原义采用任何是分隔符之间。 如果这些自变量之一设置为 null 指针，函数将返回 SQL_ERROR 和 SQLSTATE HY009 （不允许使用 null 指针）。<br /><br /> 如果 SQL_FALSE，目录函数的字符串自变量不被视为标识符。 这种情况很重要。 它们可以包含字符串的搜索模式或，具体取决于自变量。<br /><br /> 默认值为 SQL_FALSE。<br /><br /> *TableType*参数**SQLTables**，它将采用的值，列表不会影响此属性。<br /><br /> 此外可以在语句级上设置 SQL_ATTR_METADATA_ID。 （它是唯一的连接属性，也是一个语句属性）。<br /><br /> 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|SQLULEN 值，该值指定如何驱动程序管理器使用 ODBC 游标库：<br /><br /> SQL_CUR_USE_IF_NEEDED = 驱动程序管理器使用 ODBC 游标库，仅当需要它。 如果驱动程序支持中的 SQL_FETCH_PRIOR 选项**SQLFetchScroll**，驱动程序管理器使用该驱动程序的滚动功能。 否则，它使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_ODBC = 驱动程序管理器使用 ODBC 游标库。<br /><br /> SQL_CUR_USE_DRIVER = 驱动程序管理器使用该驱动程序的滚动功能。 这是默认设置。<br /><br /> 有关 ODBC 游标库的详细信息，请参阅[附录 f: ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告：** 在 Windows 的未来版本中将删除的是光标库。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|以字节为单位指定的网络数据包大小的 SQLUINTEGER 值。 **注意：** 或者多个数据源不支持此选项，或者只可以返回，但未设置网络数据包大小。 <br /><br /> 如果指定的大小超出了最大的数据包大小，或小于最小数据包大小，该驱动程序替代此值，并返回 SQLSTATE 01s02 的警告 （选项值已更改）。<br /><br /> 如果已建立连接后，应用程序将设置数据包大小，该驱动程序将返回 SQLSTATE HY011 （不能设置属性现在）。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|窗口句柄 (HWND)。<br /><br /> 如果窗口句柄为 null 指针，该驱动程序不显示任何对话框。<br /><br /> 如果窗口句柄不是 null 指针，它应为应用程序的父窗口句柄。 这是默认设置。 该驱动程序使用此句柄来显示对话框。 **注意：** SQL_ATTR_QUIET_MODE 连接属性不适用于显示的对话框**SQLDriverConnect**。|  
|SQL_ATTR_TRACE (ODBC 1.0)|告知驱动程序管理器是否执行跟踪 SQLUINTEGER 值：<br /><br /> SQL_OPT_TRACE_OFF = 跟踪关闭 （默认值）<br /><br /> SQL_OPT_TRACE_ON = on 的跟踪<br /><br /> 当跟踪时，驱动程序管理器将写入到跟踪文件每个 ODBC 函数调用。 **注意：** 驱动程序管理器打开跟踪时，可以返回 SQLSTATE IM013 （跟踪文件错误） 从任何函数。 <br /><br /> 应用程序使用 SQL_ATTR_TRACEFILE 选项指定跟踪文件。 如果该文件已存在，驱动程序管理器将追加到文件。 否则，它会创建该文件。 如果跟踪已打开，并且尚未指定任何跟踪文件，驱动程序管理器将写入文件 SQL。日志的根目录中。<br /><br /> 应用程序可以设置变量**ODBCSharedTraceFlag**表示启用动态跟踪。 对于所有当前正在运行的 ODBC 应用程序，然后启用跟踪。 如果应用程序将关闭跟踪，它处于关闭状态仅对该应用程序。<br /><br /> 如果**跟踪**的系统信息中的关键字设置为 1 时应用程序调用**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_ENV，为所有启用跟踪句柄。 仅对调用应用程序启用**SQLAllocHandle**。<br /><br /> 调用**SQLSetConnectAttr**与*属性*的 SQL_ATTR_TRACE 不要求*ConnectionHandle*自变量是有效并且不会返回 SQL_ERROR 如果*ConnectionHandle*为 NULL。 此属性适用于所有连接。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|包含跟踪文件的名称的以 null 结尾的字符字符串。<br /><br /> 使用指定 SQL_ATTR_TRACEFILE 属性的默认值**TraceFile**的系统信息中的关键字。 有关详细信息，请参阅[ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 调用**SQLSetConnectAttr**与*属性*不需要的 SQL_ATTR_ TRACEFILE *ConnectionHandle*自变量才能有效并且不会返回 SQL_ERROR 如果*ConnectionHandle*无效。 此属性适用于所有连接。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|包含包含的函数库的名称的以 null 结尾的字符字符串**SQLDriverToDataSource**和**SQLDataSourceToDriver**驱动程序有权执行如下任务字符集转译。 此选项可能仅指定是否驱动程序已连接到数据源。 该属性的设置将在连接中保持原样。 有关将数据转换的详细信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)和[转换 DLL 函数引用](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|传递给转换 DLL 一个 32 位标志值。 此属性可以仅指定是否驱动程序已连接到数据源。 有关将数据转换的信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|一个 32 位位掩码，设置当前连接的事务隔离级别。 应用程序必须调用**SQLEndTran**无法提交或回滚连接时之前调用, 所有打开的事务**SQLSetConnectAttr**使用此选项。<br /><br /> 有效值*ValuePtr*可以确定通过调用**SQLGetInfo**与*信息类型*等于 SQL_TXN_ISOLATION_OPTIONS。<br /><br /> 有关事务隔离级别的说明，请参阅 SQL_DEFAULT_TXN_ISOLATION 信息类型中的描述[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[事务隔离级别](../../../odbc/reference/develop-app/transaction-isolation-levels.md)。|  
  
 [仅当描述符不是实现描述符，而不是应用程序描述符，可以以异步方式调用 1] 这些函数。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
