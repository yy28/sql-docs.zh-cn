---
title: "SQLAllocHandle 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLAllocHandle
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLAllocHandle
helpviewer_keywords: SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e355208a1ddcae70eaea4fd01e7d3193e3b2db47
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLAllocHandle**分配一个环境、 连接、 语句或描述符句柄。  
  
> [!NOTE]  
>  此函数是替换 ODBC 2.0 函数用于分配句柄的泛型函数**SQLAllocConnect**， **SQLAllocEnv**，和**SQLAllocStmt**。 若要允许应用程序调用**SQLAllocHandle**用于 ODBC 2。*x*驱动程序，调用**SQLAllocHandle**映射在驱动程序管理器到**SQLAllocConnect**， **SQLAllocEnv**，或**SQLAllocStmt**适当。 有关详细信息，请参阅"注释"。 有关详细信息有关哪些驱动程序管理器时，将映射此函数可对 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射用于向后兼容性的应用程序的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要分配的句柄类型**SQLAllocHandle**。 必须是以下值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 仅由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *InputHandle*  
 [输入]在其上下文中新的句柄是要分配到输入的句柄。 如果*HandleType*是 SQL_HANDLE_ENV，这是 SQL_NULL_HANDLE。 如果*HandleType*是 SQL_HANDLE_DBC，这必须是环境句柄，并且如果它是 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，它必须是连接句柄。  
  
 *OutputHandlePtr*  
 [输出]指向要返回的句柄到新分配的数据结构在其中的缓冲区的指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_INVALID_HANDLE 或 SQL_ERROR。  
  
 如果分配环境句柄，以外的句柄时**SQLAllocHandle**返回 SQL_ERROR，它将设置*OutputHandlePtr*到 SQL_NULL_HDBC、 SQL_NULL_HSTMT 或 SQL_NULL_HDESC，具体取决于值*HandleType*，除非输出参数为 null 指针。 应用程序就可以从与中的句柄关联的诊断数据结构获得其他信息*InputHandle*自变量。  
  
## <a name="environment-handle-allocation-errors"></a>环境句柄分配错误  
 环境分配，均会发生在驱动程序管理器中每个驱动程序。 返回的错误**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_ENV 取决于发生了错误的级别。  
  
 如果驱动程序管理器无法分配内存 *\*OutputHandlePtr*时**SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 称为，或应用程序提供了 null 指针*OutputHandlePtr*， **SQLAllocHandle**返回 SQL_ERROR。 驱动程序管理器设置 **OutputHandlePtr*到 SQL_NULL_HENV （除非应用程序提供 null 指针，它返回 SQL_ERROR）。 与之关联的其他诊断信息没有句柄。  
  
 驱动程序管理器不会调用之前应用程序调用的驱动程序级别环境句柄分配函数**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**. 如果错误发生在驱动程序级别**SQLAllocHandle**函数，则驱动程序管理器 – 级别**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**函数返回 SQL_ERROR。 诊断数据结构包含 SQLSTATE IM004 (驱动程序的**SQLAllocHandle**失败)。 在连接句柄上返回的错误。  
  
 有关驱动程序管理器和驱动程序之间的函数调用的流的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLAllocHandle**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**使用相应*HandleType*和*处理*设置的值为*InputHandle*。 为可以返回 SQL_SUCCESS_WITH_INFO （但不是 SQL_ERROR） *OutputHandle*自变量。 下表列出了通常返回的 SQLSTATE 值**SQLAllocHandle**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) *HandleType*参数为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，但通过指定连接*InputHandle*自变量未打开。 必须已成功完成连接处理 （和必须打开连接） 驱动程序分配的语句或描述符处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 **MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|(DM) 驱动程序管理器无法为指定的句柄分配内存。<br /><br /> 该驱动程序无法为指定的句柄分配内存。|  
|HY009|不允许使用 null 指针|(DM) *OutputHandlePtr*自变量是空指针。|  
|HY010|函数序列错误|(DM) *HandleType*自变量为 SQL_HANDLE_DBC，和**SQLSetEnvAttr**尚未调用以将 SQL_ODBC_VERSION 环境属性设置。<br /><br /> (DM) 以异步方式执行的函数曾为**InputHandle**和仍在执行时**SQLAllocHandle**函数调用时使用**HandleType**设置到 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY013|内存管理错误|*HandleType*参数为 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC;，因为基础内存对象无法访问，可能是由于内存不足，无法处理函数调用条件。|  
|HY014|超出了句柄数限制|可分配的句柄的类型的句柄数的驱动程序定义限制由*HandleType*已达到自变量。|  
|HY092|属性/选项标识符无效|(DM) *HandleType*参数不是： SQL_HANDLE_ENV、 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|*HandleType*自变量为 SQL_HANDLE_DESC 和驱动程序是 ODBC 2。*x*驱动程序。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) *HandleType*参数 SQL_HANDLE_STMT，并且该驱动程序不是有效的 ODBC 驱动程序。<br /><br /> (DM) *HandleType*自变量为 SQL_HANDLE_DESC，和驱动程序不支持分配的描述符句柄。|  
  
## <a name="comments"></a>注释  
 **SQLAllocHandle**用于分配句柄的环境、 连接、 语句和描述符，如以下各节中所述。 有关句柄的常规信息，请参阅[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驱动程序支持多个分配，则可以将多个环境、 连接或语句的句柄分配一次应用程序。 ODBC，在没有限制定义的环境、 连接、 语句或可以在任何一次分配的描述符句柄数。 驱动程序可能会对施加某种类型的一次; 可以分配的句柄的数量限制有关详细信息，请参阅驱动程序文档。  
  
 如果应用程序调用**SQLAllocHandle**与 *\*OutputHandlePtr*设置为环境、 连接、 语句或已存在的描述符句柄，该驱动程序覆盖与关联的信息*处理*，除非应用程序使用连接池 （请参阅"分配环境属性的连接池"本部分中更高版本）。 驱动程序管理器不会检查以查看是否*处理*进入 *\*OutputHandlePtr*已被使用，也不会覆盖这些之前检查以前的句柄的内容.  
  
> [!NOTE]  
>  它是不正确的 ODBC 应用程序编程调用**SQLAllocHandle**两次，并为定义相同的应用程序变量 *\*OutputHandlePtr*而不调用**SQLFreeHandle**重新分配它之前释放句柄。 覆盖 ODBC 以此方式的句柄可能导致不一致的行为或部分 ODBC 驱动程序的错误。  
  
 支持多个线程的操作系统，请在应用程序可以在不同的线程使用相同的环境、 连接、 语句或描述符句柄。 因此，驱动程序必须支持此信息; 安全、 多线程访问一种方法来实现此目的，例如，是通过使用临界区或信号量。 关于线程处理的详细信息，请参阅[多线程处理](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**未设置 SQL_ATTR_ODBC_VERSION 环境属性调用分配环境句柄; 必须由应用程序或 SQLSTATE HY010 设置环境属性 （函数序列错误） 将是返回时**SQLAllocHandle**调用以分配连接句柄。  
  
 对于符合标准的应用程序， **SQLAllocHandle**映射到**SQLAllocHandleStd**在编译时。 这两个函数之间的差异在于**SQLAllocHandleStd**当使用调用将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3 *HandleType*参数设置为 SQL_HANDLE_ENV。 这样做是因为符合标准的应用程序始终是 ODBC 3。*x*应用程序。 此外，标准不需要要注册的应用程序版本。 这是这两个函数; 唯一的区别否则，它们是相同的。 **SQLAllocHandleStd**映射到**SQLAllocHandle**驱动程序管理器内。 因此，第三方驱动程序不需要实现**SQLAllocHandleStd**。  
  
 ODBC 3.8 应用程序应使用：  
  
-   **SQLAllocHandle 和不 SQLAllocHandleStd**分配环境句柄。  
  
-   **SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>分配环境句柄  
 环境句柄提供如有效的连接句柄和活动连接句柄的全局信息的访问权限。 有关环境句柄的常规信息，请参阅[环境句柄](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 若要请求的环境句柄，应用程序调用**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_ENV 和*InputHandle* SQL_NULL_HANDLE。 该驱动程序的环境信息和传递关联的句柄的值重新分配内存 *\*OutputHandlePtr*自变量。 应用程序传递 *\*OutputHandle*在需要的环境句柄自变量的所有后续调用中的值。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驱动程序管理器的环境句柄，如果已存在驱动程序的环境句柄，然后**SQLAllocHandle**与*HandleType*中该驱动程序未调用的 SQL_HANDLE_ENV 时建立连接，仅**SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC。 如果下驱动程序管理器的环境句柄，驱动程序的环境句柄不存在，驱动程序中调用使用 SQL_HANDLE_ENV HandleType SQLAllocHandle 和与 SQL_HANDLE_DBC HandleType SQLAllocHandle 时第一个连接句柄的环境连接到该驱动程序。  
  
 当驱动程序管理器处理**SQLAllocHandle**起作用*HandleType*的 SQL_HANDLE_ENV，它会检查**跟踪**系统 [ODBC] 部分中的关键字信息。 如果设置为 1，驱动程序管理器为启用跟踪当前应用程序。 设置跟踪标志，如果第一个环境句柄分配和结束时释放的最后一个的环境句柄时启动跟踪。 有关详细信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 分配的环境句柄后, 应用程序必须调用**SQLSetEnvAttr**环境句柄设置 SQL_ATTR_ODBC_VERSION 环境属性上。 如果之前未设置此属性**SQLAllocHandle**调用以分配连接句柄在环境中，用于分配连接的调用将返回 SQLSTATE HY010 （函数序列错误）。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>分配连接池的共享环境  
 可以在单个进程上的多个组件之间共享环境。 可同时由多个组件共享的环境。 当一个组件使用的共享的环境时，它可以使用已入池的连接，这允许应用程序分配，而无需重新创建该连接使用一个现有的连接。  
  
 应用程序分配的共享的环境可用于连接池之前，必须调用**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 环境属性设置为 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 **SQLSetEnvAttr**在这种情况下使用调用*EnvironmentHandle*设置为 null，这使得进程级别属性的属性。  
  
 在启用连接池后，应用程序调用**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_ENV。 此调用所分配的环境将隐式的共享的环境，因为在启用连接池。  
  
 分配的共享的环境后，将使用的环境，未确定直到**SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC 的调用。 此时，驱动程序管理器尝试查找与请求的应用程序环境特性相匹配的现有环境。 如果不存在任何此类环境，将作为共享环境中创建一个。 驱动程序管理器维护每个共享环境中; 的引用计数首次创建环境时，计数设置为 1。 如果找到匹配的环境，则该环境的句柄返回给应用程序，并递增引用计数。 在这种方式中分配的环境句柄可以用于接受作为输入自变量的环境句柄任何 ODBC 函数中。  
  
## <a name="allocating-a-connection-handle"></a>分配连接句柄  
 连接句柄可以访问信息，例如有效的语句和描述符句柄连接和事务的目前是否打开。 有关连接句柄的常规信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 若要请求连接句柄，应用程序调用**SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC。 *InputHandle*参数设置为通过调用返回的环境句柄**SQLAllocHandle**分配该句柄。 该驱动程序的连接信息和传递关联的句柄的值重新分配内存 *\*OutputHandlePtr*。 应用程序传递 *\*OutputHandlePtr*在需要连接句柄的所有后续调用中的值。 有关详细信息，请参阅[分配连接处理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 驱动程序管理器处理**SQLAllocHandle**函数并调用驱动程序的**SQLAllocHandle**函数时在应用程序调用**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**。 (有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。)  
  
 如果之前未设置 SQL_ATTR_ODBC_VERSION 环境属性**SQLAllocHandle**调用以分配连接句柄在环境中，用于分配连接的调用将返回 SQLSTATE HY010 （函数序列错误）。  
  
 在应用程序调用**SQLAllocHandle**与*InputHandle*自变量设置为 SQL_HANDLE_DBC，并且还将设置为共享的环境句柄，驱动程序管理器将尝试查找现有的共享由应用程序设置的环境属性匹配的环境。 如果不存在任何此类环境，将创建一个，引用计数 1 （由驱动程序管理器中维护）。 如果匹配共享找到环境、 该句柄返回给应用程序和其引用计数会递增。  
  
 将使用的实际连接不确定的驱动程序管理器直到**SQLConnect**或**SQLDriverConnect**调用。 驱动程序管理器的调用中使用的连接选项**SQLConnect** (或在调用连接关键字**SQLDriverConnect**) 和连接分配到后设置连接属性确定应使用池中的连接。 有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>分配的语句句柄  
 语句句柄提供语句的信息，如错误消息、 游标名称和状态信息的 SQL 语句处理的访问。 有关语句句柄的常规信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 若要请求的语句句柄，应用程序连接到数据源，然后调用**SQLAllocHandle**提交 SQL 语句之前。 在此调用中， *HandleType*应设置为 SQL_HANDLE_STMT 和*InputHandle*应设置为通过调用返回的连接句柄**SQLAllocHandle**分配该句柄。 驱动程序的语句信息分配内存，将语句句柄与指定的连接，并将传递回关联的句柄的值相关联 *\*OutputHandlePtr*。 应用程序传递 *\*OutputHandlePtr*在需要语句句柄的所有后续调用中的值。 有关详细信息，请参阅[分配语句处理](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 该驱动程序分配语句句柄后，自动分配的四个描述符一组并将这些描述符句柄赋给 SQL_ATTR_APP_ROW_DESC、 SQL_ATTR_APP_PARAM_DESC、 SQL_ATTR_IMP_ROW_DESC 和 SQL_ATTR_IMP_PARAM_DESC语句属性。 这些被称为*隐式*分配描述符。 若要显式分配应用程序描述符，请参阅以下部分中，"分配的描述符句柄"。  
  
## <a name="allocating-a-descriptor-handle"></a>分配的描述符句柄  
 在应用程序调用**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_DESC，驱动程序分配了应用程序描述符。 这些被称为*显式*分配描述符。 应用程序指示要通过调用而不是自动分配一个给定的语句句柄使用显式分配应用程序描述符的驱动程序**SQLSetStmtAttr**具有 SQL_ATTR_APP_ROW_DESC 函数或 SQL_ATTR_APP_PARAM_DESC 属性。 无法显式分配实现描述符也可以在中指定实现描述符**SQLSetStmtAttr**函数调用。  
  
 （如自动分配的描述符），显式分配的描述符都与连接句柄而不是语句句柄关联。 仅当应用程序实际连接到数据库时，描述符保持分配。 因为显式分配的描述符连接句柄与相关联，应用程序可以将与连接中的多个语句关联显式分配的描述符。 另一方面，隐式分配应用程序描述符，无法与多个语句句柄关联。 （它不能与它已分配给以外的任何语句句柄关联。）显式分配的描述符句柄可以被显式释放应用程序或通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC，或隐式连接时关闭。  
  
 释放显式分配的描述符，隐式分配的描述符时，再次与该语句相关联。 （该语句的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 属性重新设置为隐式分配的描述符句柄。）这适用于与连接上显式分配的描述符相关联的所有语句。  
  
 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)， [SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)，和[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放环境、 连接、 语句或描述符句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
