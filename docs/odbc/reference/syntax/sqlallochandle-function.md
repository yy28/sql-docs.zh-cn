---
title: SQLAllocHandle 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db8bcf70823401f60efc316caabe283f5be59f48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538108"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLAllocHandle**分配环境、 连接、 语句或描述符句柄。  
  
> [!NOTE]  
>  此函数是替换 ODBC 2.0 函数的泛型函数分配句柄**SQLAllocConnect**， **SQLAllocEnv**，并**SQLAllocStmt**。 若要允许应用程序调用**SQLAllocHandle**以使用 ODBC 2。*x*驱动程序，先调用**SQLAllocHandle**映射在驱动程序管理器向**SQLAllocConnect**， **SQLAllocEnv**，或**SQLAllocStmt**根据。 有关详细信息，请参阅"注释"。 有关哪些驱动程序管理器的详细信息将时 ODBC 3 映射到此函数。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[向后兼容性的应用程序映射替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要分配的句柄的类型**SQLAllocHandle**。 必须是以下值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只能由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *InputHandle*  
 [输入]在其上下文中新的句柄是要分配输入句柄。 如果*HandleType*为 SQL_HANDLE_ENV，这是 SQL_NULL_HANDLE。 如果*HandleType*为 SQL_HANDLE_DBC，这必须是环境句柄，并且如果它为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，它必须是连接句柄。  
  
 *OutputHandlePtr*  
 [输出]指向用于返回到新分配的数据结构的句柄缓冲区的指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_INVALID_HANDLE 或 SQL_ERROR。  
  
 如果分配环境句柄，以外的句柄时**SQLAllocHandle**将返回 SQL_ERROR，它会设置*OutputHandlePtr* SQL_NULL_HDBC、 SQL_NULL_HSTMT，或 SQL_NULL_HDESC，具体取决于值*HandleType*，除非输出参数为 null 指针。 应用程序然后可以与在句柄关联的诊断数据结构中获取其他信息*InputHandle*参数。  
  
## <a name="environment-handle-allocation-errors"></a>环境句柄分配错误  
 环境分配发生在驱动程序管理器和每个驱动程序中。 返回的错误**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_ENV 取决于发生了错误的级别。  
  
 如果驱动程序管理器无法分配内存 *\*OutputHandlePtr*时**SQLAllocHandle**与*HandleType*调用时设为 SQL_HANDLE_ENV，或应用程序提供的 null 指针*OutputHandlePtr*， **SQLAllocHandle**返回 SQL_ERROR。 驱动程序管理器设置 **OutputHandlePtr*到 SQL_NULL_HENV （除非应用程序提供 null 指针，它将返回 SQL_ERROR）。 没有任何要与关联的其他诊断信息的句柄。  
  
 驱动程序管理器不会调用应用程序调用之前的驱动程序级别环境句柄的分配函数**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**. 如果驱动程序级别中出现错误**SQLAllocHandle**函数，则驱动程序管理器级别**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**函数将返回 SQL_ERROR。 诊断数据结构包含 SQLSTATE IM004 (驱动程序的**SQLAllocHandle**失败)。 连接句柄上返回的错误。  
  
 有关驱动程序管理器和驱动程序之间的函数调用的流的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLAllocHandle**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**具有相应*HandleType*并*处理*设置的值为*InputHandle*。 为可以返回 SQL_SUCCESS_WITH_INFO （但不是 SQL_ERROR） *OutputHandle*参数。 下表列出了通常由返回的 SQLSTATE 值**SQLAllocHandle** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|（数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，但通过指定的连接*InputHandle*参数未打开。 必须成功完成连接过程 （和必须打开连接） 的驱动程序分配一个语句或描述符处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 **MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|(DM) 的驱动程序管理器无法为指定句柄分配内存。<br /><br /> 该驱动程序无法为指定句柄分配内存。|  
|HY009|使用空指针无效|（数据挖掘） *OutputHandlePtr*参数是空指针。|  
|HY010|函数序列错误|（数据挖掘） *HandleType*参数为 SQL_HANDLE_DBC，并**SQLSetEnvAttr**尚未调用设置 SQL_ODBC_VERSION 环境属性。<br /><br /> (DM) 的调用以异步方式执行的函数**InputHandle**和仍在执行时**SQLAllocHandle**调用函数时使用**HandleType**设置为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY013|内存管理错误|*HandleType*参数为 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC;，因为基础内存对象无法访问，可能是由于内存不足，无法处理函数调用条件。|  
|HY014|超出了句柄的数量限制|可分配的句柄的类型的句柄数的驱动程序定义限制为由*HandleType*已达到自变量。|  
|HY092|属性/选项标识符无效|（数据挖掘） *HandleType*参数不是：SQL_HANDLE_ENV、 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|*HandleType*参数为 SQL_HANDLE_DESC 和司机的 ODBC 2。*x*驱动程序。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|（数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT，，和驱动程序不是有效的 ODBC 驱动程序。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_DESC，并且该驱动程序不支持分配描述符句柄。|  
  
## <a name="comments"></a>注释  
 **SQLAllocHandle**用于分配句柄的环境、 连接、 语句和描述符，如以下各节中所述。 有关控点的常规信息，请参阅[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驱动程序支持多个分配，可以通过一次的应用程序分配多个环境、 连接或语句句柄。 在 ODBC 中，定义的环境、 连接、 语句或可以在任何一次分配的描述符句柄数没有限制。 驱动程序可能会施加可以一次; 分配的句柄的特定类型的数量上限有关详细信息，请参阅驱动程序文档。  
  
 如果应用程序调用**SQLAllocHandle**与 *\*OutputHandlePtr*设置为环境、 连接、 语句或描述符句柄已存在，该驱动程序将覆盖与关联的信息*处理*，除非应用程序正在使用连接池 （请参阅"分配环境属性的连接池"稍后在本部分中）。 驱动程序管理器不会检查以查看是否*处理*中输入 *\*OutputHandlePtr*已被使用，也不会覆盖前检查以前的句柄的内容.  
  
> [!NOTE]  
>  它是不正确的 ODBC 应用程序编程以调用**SQLAllocHandle**两次，并为定义的相同应用程序变量 *\*OutputHandlePtr*而无需调用**SQLFreeHandle**以重新分配它之前释放句柄。 覆盖 ODBC 句柄以这种方式可能导致不一致的行为或 ODBC 驱动程序部分的错误。  
  
 在操作系统上支持多个线程的应用程序可以在不同线程上使用相同的环境、 连接、 语句或描述符句柄。 因此，驱动程序必须支持安全、 多线程访问此信息;一种方法来实现此目的，例如，是通过使用关键节或信号量。 关于线程处理的详细信息，请参阅[多线程处理](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**未设置 SQL_ATTR_ODBC_VERSION 环境属性时被调用以在分配环境句柄; 必须由应用程序或 SQLSTATE HY010 设置环境属性 （函数序列错误） 将为时返回**SQLAllocHandle**调用以分配连接句柄。  
  
 对于符合标准的应用程序， **SQLAllocHandle**映射到**SQLAllocHandleStd**在编译时。 这两个函数之间的差异在于**SQLAllocHandleStd**时使用调用 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3 *HandleType*参数设置为 SQL_HANDLE_ENV。 这是因为符合标准的应用程序始终是 ODBC 3。*x*应用程序。 此外，标准不需要要注册的应用程序版本。 这是这两个函数; 之间的唯一区别否则，它们是相同的。 **SQLAllocHandleStd**映射到**SQLAllocHandle**驱动程序管理器内。 因此，第三方驱动程序不需要实现**SQLAllocHandleStd**。  
  
 应使用 ODBC 3.8 应用程序：  
  
-   **SQLAllocHandle 和不 SQLAllocHandleStd**以分配环境句柄。  
  
-   **SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>分配环境句柄  
 环境句柄提供有效的连接句柄和活动连接句柄等全局信息的访问。 有关环境句柄的常规信息，请参阅[环境句柄](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 若要请求环境句柄，应用程序调用**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_ENV 和一个*InputHandle*的 SQL_NULL_HANDLE。 该驱动程序的环境信息和阶段关联句柄的值重新分配内存 *\*OutputHandlePtr*参数。 应用程序传递 *\*OutputHandle*要求环境句柄参数的所有后续调用中的值。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驱动程序管理器的环境句柄，如果已存在的驱动程序的环境句柄，然后**SQLAllocHandle**与*HandleType*中该驱动程序未调用设为 SQL_HANDLE_ENV 时建立连接后，仅**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC。 如果驱动程序管理器的环境句柄下，驱动程序的环境句柄不存在，驱动程序中调用使用 SQL_HANDLE_ENV HandleType SQLAllocHandle 和与 SQL_HANDLE_DBC HandleType SQLAllocHandle 时第一个连接句柄的环境连接到该驱动程序。  
  
 驱动程序管理器进行处理时**SQLAllocHandle**起作用*HandleType*设为 SQL_HANDLE_ENV，它会检查**跟踪**系统的 [ODBC] 部分中的关键字信息。 如果设置为 1，驱动程序管理器启用当前应用程序的跟踪。 如果设置了跟踪标志，跟踪时开始第一个环境句柄分配结束时释放最后一个环境句柄。 有关详细信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 分配环境句柄之后, 应用程序必须调用**SQLSetEnvAttr**环境句柄设置 SQL_ATTR_ODBC_VERSION 环境属性上。 如果之前未设置此属性，则**SQLAllocHandle**调用以分配连接句柄在环境中，用于分配连接的调用将返回 SQLSTATE HY010 （函数序列错误）。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>分配的连接池在共享环境  
 可以在单个进程上的多个组件之间共享的环境。 在同一时间，可以由多个组件使用共享的环境。 当一个组件使用共享的环境时，它可以使用已入池的连接，这允许它分配并使用现有连接，而无需重新创建该连接。  
  
 应用程序分配一个共享的环境可用于连接池之前，必须调用**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 环境属性设置为 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 **SQLSetEnvAttr**这种情况下使用调用*EnvironmentHandle*设置为 null，这使得进程级别属性的属性。  
  
 已启用连接池后，应用程序调用**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_ENV。 此调用分配的环境将隐式的共享的环境，因为已启用连接池。  
  
 当分配共享的环境中时，只有不确定将使用的环境**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 调用。 此时，驱动程序管理器将尝试查找与请求的应用程序环境特性相匹配的现有环境。 如果不存在任何此类环境，是作为共享环境中创建一个。 驱动程序管理器维护每个共享环境中; 引用的计数首次创建环境时，计数设置为 1。 如果找到匹配的环境，则该环境的句柄返回给应用程序和引用计数会递增。 可在任何接受环境句柄作为输入参数的 ODBC 函数以这种方式分配环境句柄。  
  
## <a name="allocating-a-connection-handle"></a>分配连接句柄  
 连接句柄可以访问的有效语句之类的信息和描述符句柄上连接和事务的目前是否打开。 有关连接句柄的常规信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 若要请求连接句柄，应用程序调用**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC。 *InputHandle*参数设置为返回到调用的环境句柄**SQLAllocHandle**分配该句柄。 该驱动程序的连接信息和阶段关联句柄的值重新分配内存 *\*OutputHandlePtr*。 应用程序传递 *\*OutputHandlePtr*要求连接句柄的所有后续调用中的值。 有关详细信息，请参阅[分配连接处理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 驱动程序管理器将处理**SQLAllocHandle**函数，并调用在驱动程序**SQLAllocHandle**函数时应用程序调用**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**。 (有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。)  
  
 如果之前未设置 SQL_ATTR_ODBC_VERSION 环境属性，则**SQLAllocHandle**调用以分配连接句柄在环境中，用于分配连接的调用将返回 SQLSTATE HY010 （函数序列错误）。  
  
 当应用程序调用**SQLAllocHandle**与*InputHandle*参数设置为 SQL_HANDLE_DBC 并且还将设置为共享的环境句柄，驱动程序管理器将尝试查找的现有共享应用程序设置的环境属性匹配的环境。 如果不存在任何此类环境，创建一个，引用计数 1 （维护的驱动程序管理器）。 如果匹配共享找到环境，该句柄返回给应用程序和其引用计数会递增。  
  
 将使用的实际连接不确定的驱动程序管理器直到**SQLConnect**或**SQLDriverConnect**调用。 驱动程序管理器对的调用中使用的连接选项**SQLConnect** (或在调用连接关键字**SQLDriverConnect**) 并连接到分配后设置连接属性确定应使用哪个连接池中。 有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>分配语句句柄  
 语句句柄提供了用于执行 SQL 语句处理语句的信息，如错误消息、 游标名称和状态信息的访问权限。 语句句柄的常规信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 若要请求语句句柄，应用程序连接到数据源，然后调用**SQLAllocHandle**提交 SQL 语句之前。 在此调用中， *HandleType*应设置为 SQL_HANDLE_STMT，并*InputHandle*应设置为连接句柄返回到调用**SQLAllocHandle**该数值分配该句柄。 驱动程序分配内存的语句的信息、 指定的连接，并传递回关联句柄的值相关联的语句句柄 *\*OutputHandlePtr*。 应用程序传递 *\*OutputHandlePtr*在需要语句句柄的所有后续调用中的值。 有关详细信息，请参阅[分配的语句句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 分配语句句柄后，该驱动程序自动分配一组四个描述符并将这些描述符句柄分配给 SQL_ATTR_APP_ROW_DESC、 SQL_ATTR_APP_PARAM_DESC、 SQL_ATTR_IMP_ROW_DESC 和 SQL_ATTR_IMP_PARAM_DESC语句属性。 这些称为*隐式*分配描述符。 若要显式分配应用程序描述符，请参阅以下部分中，"分配描述符句柄。"  
  
## <a name="allocating-a-descriptor-handle"></a>分配描述符句柄  
 当应用程序调用**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_DESC，驱动程序分配了应用程序描述符。 这些称为*显式*分配描述符。 应用程序指示驱动程序即可通过调用而不是一个自动分配为给定的语句句柄使用显式分配应用程序描述符**SQLSetStmtAttr** SQL_ATTR_APP_ROW_DESC 函数或 SQL_ATTR_APP_PARAM_DESC 属性。 不能显式分配的实现描述符也可以在中指定实现描述符**SQLSetStmtAttr**函数调用。  
  
 显式分配的描述符与相关联的连接句柄而不是语句句柄 （如自动分配的描述符）。 仅当应用程序实际连接到数据库时，保持已分配描述符。 因为显式分配的描述符与连接句柄相关联，则应用程序可以与连接中的多个语句关联显式分配的描述符。 但是，不是隐式分配的应用程序描述符，能与多个语句句柄相关联。 （它不能与任何语句句柄而不是它已分配给相关联。）可以显式释放显式分配的描述符句柄由应用程序或通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC，或隐式连接时已关闭。  
  
 释放显式分配的描述符，隐式分配的描述符时再次与该语句相关联。 （适用于该语句的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 属性重新设置为隐式分配的描述符句柄。）这是与在连接上显式分配的描述符相关联的所有语句，则返回 true。  
  
 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)， [SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)，以及[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放环境、 连接、 语句或描述符句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置一个环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
