---
title: SQLAllocHandle 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290206"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLAllocHandle**分配环境、连接、语句或描述符句柄。  
  
> [!NOTE]  
>  此函数是用于分配句柄的通用函数，用于替换 ODBC 2.0 函数**SQLAllocConnect、SQLAllocEnv**和**SQLAllocStmt。** **SQLAllocEnv** 允许调用**SQLAllocHandle 的应用程序**使用 ODBC 2。*x*驱动程序，对**SQLAllocHandle 的**调用在驱动程序管理器中映射到**SQLAllocConnect、SQLAllocEnv**或**SQLAllocStmt（** 视情况而定）。 **SQLAllocEnv** 有关详细信息，请参阅"注释"。 有关驱动程序管理器将此功能映射到 ODBC 3 时的详细信息。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射应用程序向后兼容性的替代函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要由**SQLAllocHandle**分配的句柄的类型。 必须是以下值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄仅由驱动程序管理器和驱动程序使用。 应用程序不应使用此句柄类型。 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *输入手柄*  
 [输入]要在上下文中分配新句柄的输入句柄。 如果*HandleType*是SQL_HANDLE_ENV，则这是SQL_NULL_HANDLE。 如果*HandleType* SQL_HANDLE_DBC，则它必须是环境句柄，如果是SQL_HANDLE_STMT或SQL_HANDLE_DESC，则必须是连接句柄。  
  
 *输出手柄*  
 [输出]指向要将句柄返回到新分配的数据结构的缓冲区的指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_INVALID_HANDLE 或SQL_ERROR。  
  
 分配环境句柄以外的句柄时，如果**SQLAllocHandle**返回SQL_ERROR，它将*OutputHandlePtr*设置为SQL_NULL_HDBC、SQL_NULL_HSTMT或SQL_NULL_HDESC，具体取决于*HandleType 的值*，除非输出参数是空指针。 然后，应用程序可以从与*InputHandle*参数中的句柄关联的诊断数据结构获取其他信息。  
  
## <a name="environment-handle-allocation-errors"></a>环境处理分配错误  
 环境分配既发生在驱动程序管理器内，也发生在每个驱动程序中。 **SQLAllocHandle**返回的错误带有SQL_HANDLE_ENV*的句柄类型*，具体取决于发生错误的级别。  
  
 如果调用具有*SQL_HANDLE_ENV的* **SQLAllocHandle**时驱动程序管理器无法为*\*输出句柄分配*内存，或者应用程序为*OutputHandlePtr*提供空指针，**则 SQLAllocHandle**返回SQL_ERROR。 驱动程序管理器将输出*句柄设置*到SQL_NULL_HENV（除非应用程序提供了一个空指针，该指针返回SQL_ERROR）。 没有关联其他诊断信息的句柄。  
  
 在应用程序调用**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect**之前**SQLConnect**，驱动程序管理器不会调用驱动程序级环境句柄分配函数。 如果驱动程序级**SQLAllocHandle**函数中出现错误，则驱动程序管理器级别的**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect**函数将返回SQL_ERROR。 **SQLBrowseConnect** 诊断数据结构包含 SQLSTATE IM004（驱动程序的**SQLAllocHandle**失败）。 在连接句柄上返回错误。  
  
 有关驱动程序管理器和驱动程序之间函数调用流的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLAllocHandle**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获得关联的 SQLSTATE 值，并将相应的*句柄Type*和*句柄*设置为*InputHandle*的值。 可以为*输出处理*参数返回SQL_SUCCESS_WITH_INFO（但不是SQL_ERROR）。 下表列出了**SQLAllocHandle**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|（DM） *HandleType*参数SQL_HANDLE_STMT或SQL_HANDLE_DESC，但*InputHandle*参数指定的连接未打开。 连接过程必须成功完成（连接必须打开），驱动程序才能分配语句或描述符句柄。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在 @*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|（DM） 驱动程序管理器无法为指定的句柄分配内存。<br /><br /> 驱动程序无法为指定的句柄分配内存。|  
|HY009|无效使用空指针|（DM）*输出句柄Ptr*参数是一个空指针。|  
|HY010|函数序列错误|（DM） *handleType*参数SQL_HANDLE_DBC，并且尚未调用**SQLSetEnvAttr**来设置SQL_ODBC_VERSION环境属性。<br /><br /> （DM） 为**InputHandle**调用了异步执行函数，并且在使用**HandleType**设置为SQL_HANDLE_STMT或SQL_HANDLE_DESC调用**SQLAllocHandle**函数时仍在执行。|  
|HY013|内存管理错误|*HandleType*参数SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC;无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY014|超过控点的控点数量限制|已达到为*HandleType*参数指示的句柄类型可分配的句柄数的驱动程序定义限制。|  
|HY092|无效属性/选项标识符|（DM） *HandleType*参数不是：SQL_HANDLE_ENV、SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|*HandleType*参数SQL_HANDLE_DESC，驱动程序是 ODBC 2。*x*驱动程序。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） *HandleType*参数SQL_HANDLE_STMT，驱动程序不是有效的 ODBC 驱动程序。<br /><br /> （DM） *handleType*参数SQL_HANDLE_DESC，驱动程序不支持分配描述符句柄。|  
  
## <a name="comments"></a>注释  
 **SQLAllocHandle**用于为环境、连接、语句和描述符分配句柄，如以下各节所述。 有关句柄的一般信息，请参阅[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驱动程序支持多个分配，应用程序可以一次分配多个环境、连接或语句句柄。 在 ODBC 中，对可在任何时间分配的环境、连接、语句或描述符句柄的数量不定义任何限制。 驱动程序可能会限制一次可以分配的某种类型的句柄的数量;有关详细信息，请参阅驱动程序文档。  
  
 如果应用程序使用*\*OutputHandlePtr*调用**SQLAllocHandle，** 并将该句柄设置为已经存在的环境、连接、语句或描述符句柄，则驱动程序将覆盖与*句柄*关联的信息，除非应用程序正在使用连接池（请参阅本节后面的"为连接池分配环境属性"）。 驱动程序管理器不检查在*\*OutputHandlePtr*中输入的*句柄*是否已被使用，也不会在覆盖句柄之前检查句柄的先前内容。  
  
> [!NOTE]  
>  使用为*\*OutputHandlePtr*定义的相同应用程序变量调用**SQLAllocHandle**两次，而不调用**SQLFreeHandle**以释放句柄，然后再重新分配它，这是不正确的 ODBC 应用程序编程。 以这种方式覆盖 ODBC 句柄可能会导致 ODBC 驱动程序的行为不一致或错误。  
  
 在支持多个线程的操作系统上，应用程序可以在不同的线程上使用相同的环境、连接、语句或描述符句柄。 因此，驱动程序必须支持对此信息的安全多线程访问;例如，实现此目的的一种方法是使用关键部分或信号量。 有关线程的详细信息，请参阅[多线程](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**在调用环境句柄时不设置SQL_ATTR_ODBC_VERSION环境属性;但是，在调用它时，它未设置该属性。环境属性必须由应用程序设置，或者当调用**SQLAllocHandle**分配连接句柄时，将返回 SQLSTATE HY010（函数序列错误）。  
  
 对于符合标准的应用程序 **，SQLAllocHandle**在编译时映射到**SQLAllocHandleStd。** 这两个函数之间的区别是 **，SQLAllocHandleStd**将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3，当使用*HandleType*参数设置为SQL_HANDLE_ENV时，将环境属性设置为SQL_OV_ODBC3。 之所以这样做，是因为符合标准的应用程序始终是 ODBC 3。*x*应用程序。 此外，标准不要求注册应用程序版本。 这是这两个函数之间的唯一区别;否则，它们是相同的。 **SQLAllocHandleStd**映射到驱动程序管理器内的**SQLAllocHandle。** 因此，第三方驱动程序不必实现**SQLAllocHandleStd**。  
  
 ODBC 3.8 应用程序应使用：  
  
-   **SQLAllocHandle 而不是 SQLAllocHandleStd**来分配环境句柄。  
  
-   **SQLSetEnvAttr**将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>分配环境句柄  
 环境句柄提供对全局信息（如有效连接句柄和活动连接句柄）的访问。 有关环境句柄的一般信息，请参阅[环境句柄](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 要请求环境句柄，应用程序调用**SQLAllocHandle，** 具有 SQL_HANDLE_ENV的*句柄类型*和 SQL_NULL_HANDLE的*输入句柄*。 驱动程序为环境信息分配内存，并将关联的句柄的值传回*\*OutputHandlePtr*参数中。 应用程序在所有需要环境句柄参数的后续调用中传递*\*OutputHandle*值。 有关详细信息，请参阅[分配环境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驱动程序管理器的环境句柄下，如果已存在驱动程序的环境句柄，则在建立连接时，该驱动程序中不会调用具有*句柄类型的*SQL_HANDLE_ENV **SQLAllocHandle，** 只有具有*SQL_HANDLE_DBC的* **SQLAllocHandle。** 如果驱动程序的环境句柄在驱动程序管理器的环境句柄下不存在，则当环境的第一个连接句柄连接到驱动程序时，驱动程序中会调用具有SQL_HANDLE_ENV句柄类型的 SQLAllocHandle 和具有 SQL_HANDLE_DBC的 SQLAllocHandle。  
  
 当驱动程序管理器使用 SQL_HANDLE_ENV 的*句柄类型*处理**SQLAllocHandle**函数时，它会检查系统信息 [ODBC] 部分中的**Trace**关键字。 如果设置为 1，驱动程序管理器将启用对当前应用程序的跟踪。 如果设置了跟踪标志，则跟踪在分配第一个环境句柄时开始，并在释放最后一个环境句柄时结束。 有关详细信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 分配环境句柄后，应用程序必须在环境句柄上调用**SQLSetEnvAttr**来设置SQL_ATTR_ODBC_VERSION环境属性。 如果在调用**SQLAllocHandle**在环境中分配连接句柄之前未设置此属性，则分配连接的调用将返回 SQLSTATE HY010（函数序列错误）。 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>为连接池分配共享环境  
 环境可以在单个进程中在多个组件之间共享。 共享环境可以同时由多个组件使用。 当组件使用共享环境时，它可以使用池连接，从而允许它分配和使用现有连接，而无需重新创建该连接。  
  
 在分配可用于连接池的共享环境之前，应用程序必须调用**SQLSetEnvAttr**将SQL_ATTR_CONNECTION_POOLING环境属性设置为SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV。 在这种情况下 **，SQLSetEnvAttr**调用*环境处理设置为*null，这使得属性成为进程级属性。  
  
 启用连接池后，应用程序将**SQLAllocHandle**调用，*句柄类型*参数设置为SQL_HANDLE_ENV。 此调用分配的环境将是隐式共享环境，因为连接池已启用。  
  
 分配共享环境后，在调用具有*SQL_HANDLE_DBC*的**SQLAllocHandle**之前，不会确定将使用的环境。 此时，驱动程序管理器尝试查找与应用程序请求的环境属性匹配的现有环境。 如果不存在此类环境，则创建一个环境作为共享环境。 驱动程序管理器维护每个共享环境的引用计数;首次创建环境时，计数设置为 1。 如果找到匹配的环境，该环境的句柄将返回到应用程序，并且引用计数将递增。 以这种方式分配的环境句柄可用于接受环境句柄作为输入参数的任何 ODBC 函数。  
  
## <a name="allocating-a-connection-handle"></a>分配连接句柄  
 连接句柄提供对连接上的有效语句和描述符句柄以及事务当前是否打开等信息的访问。 有关连接句柄的一般信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 要请求连接句柄，应用程序使用*SQL_HANDLE_DBC的句柄类型*调用**SQLAllocHandle。** *InputHandle*参数设置为调用分配给该句柄的**SQLAllocHandle**返回的环境句柄。 驱动程序为连接信息分配内存，并将关联的句柄的值传回*\*OutputHandlePtr*中。 应用程序在所有*\** 需要连接句柄的后续调用中传递 OutputHandlePtr 值。 有关详细信息，请参阅[分配连接句柄](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 驱动程序管理器处理**SQLAllocHandle**函数，并在应用程序调用**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect****SQLBrowseConnect**时调用驱动程序的**SQLAllocHandle**函数。 （有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果在调用**SQLAllocHandle**在环境中分配连接句柄之前未设置SQL_ATTR_ODBC_VERSION环境属性，则分配连接的调用将返回 SQLSTATE HY010（函数序列错误）。  
  
 当应用程序调用**SQLAllocHandle**时，*输入句柄*参数设置为SQL_HANDLE_DBC并设置为共享环境句柄，驱动程序管理器将尝试查找与应用程序设置的环境属性匹配的现有共享环境。 如果不存在此类环境，则创建一个环境，引用计数（由驱动程序管理器维护）为 1。 如果找到匹配的共享环境，该句柄将返回到应用程序，其引用计数将递增。  
  
 在调用**SQLConnect**或**SQLDriverConnect**之前，驱动程序管理器不会确定将使用的实际连接。 驱动程序管理器在调用**SQLConnect**时使用连接选项（或**SQLDriverConnect**调用中的连接关键字）和连接分配后设置的连接属性来确定应在池中使用哪个连接。 有关详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>分配语句句柄  
 语句句柄提供对语句信息（如错误消息、游标名称和 SQL 语句处理的状态信息）的访问。 有关语句句柄的一般信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 要请求语句句柄，应用程序连接到数据源，然后在提交 SQL 语句之前调用**SQLAllocHandle。** 在此调用中 *，HandleType*应设置为SQL_HANDLE_STMT，*并且输入句柄*应设置为调用分配给该句柄的**SQLAllocHandle**返回的连接句柄。 驱动程序为语句信息分配内存，将语句句柄与指定的连接关联，并在*\*OutputHandlePtr*中传递关联句柄的值。 应用程序在所有*\** 需要语句句柄的后续调用中传递 OutputHandlePtr 值。 有关详细信息，请参阅[分配语句句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 分配语句句柄时，驱动程序会自动分配一组四个描述符，并将这些描述符的句柄分配给SQL_ATTR_APP_ROW_DESC、SQL_ATTR_APP_PARAM_DESC、SQL_ATTR_IMP_ROW_DESC 和SQL_ATTR_IMP_PARAM_DESC语句属性。 这些称为*隐式*分配的描述符。 要显式分配应用程序描述符，请参阅以下部分"分配描述符句柄"。  
  
## <a name="allocating-a-descriptor-handle"></a>分配描述符句柄  
 当应用程序使用 SQL_HANDLE_DESC 的*句柄类型*调用**SQLAllocHandle**时，驱动程序分配应用程序描述符。 这些称为*显式*分配的描述符。 应用程序指示驱动程序使用显式分配的应用程序描述符，而不是通过使用 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 属性调用**SQLSetStmtAttr**函数来为给定语句句柄自动分配的应用程序描述符。 不能显式分配实现描述符，也不能在**SQLSetStmtAttr**函数调用中指定实现描述符。  
  
 显式分配的描述符与连接句柄而不是语句句柄相关联（自动分配的描述符是）。 仅当应用程序实际连接到数据库时，才会分配描述符。 由于显式分配的描述符与连接句柄相关联，因此应用程序可以将显式分配的描述符与连接中的多个语句相关联。 另一方面，隐式分配的应用程序描述符不能与多个语句句柄关联。 （它不能与分配给它的任何语句句柄以外的任何语句句柄相关联。显式分配的描述符句柄可以通过应用程序或使用SQL_HANDLE_DESC*的句柄类型*调用**SQLFreeHandle**或连接关闭时隐式释放。  
  
 释放显式分配的描述符时，隐式分配的描述符将再次与 语句关联。 （该语句SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC属性将再次设置为隐式分配的描述符句柄。对于与连接上显式分配的描述符关联的所有语句，这都是如此。  
  
 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)[、SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)[、SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLSetCursor 名称函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放环境、连接、语句或描述符句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|准备执行语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
