---
title: SQLBrowseConnect 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34fbd05bcdec421ee9a00474f939d54219f7b321
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支持发现和枚举的属性和连接到数据源所需的属性值的迭代方法。 每次调用**SQLBrowseConnect**返回连续级别的属性和属性值。 当所有级别具有都枚举，完成与数据源的连接并且完整的连接字符串由**SQLBrowseConnect**。 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 的返回代码指示已指定所有连接信息和应用程序现已连接到数据源。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *InConnectionString*  
 [输入]浏览请求连接字符串 (请参阅"*InConnectionString*自变量"中"注释")。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*以字符为单位。  
  
 *OutConnectionString*  
 [输出]指向字符缓冲区中要返回浏览结果连接字符串 (请参阅"*OutConnectionString*自变量"中"注释")。  
  
 如果*OutConnectionString*为 NULL， *StringLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回在缓冲区中指向*OutConnectionString*。  
  
 *BufferLength*  
 [输入]长度，以字符为单位的 **OutConnectionString*缓冲区。  
  
 *StringLength2Ptr*  
 [输出]字符 （不包括 null 终止） 可用于在中返回的总数\* *OutConnectionString*。 可用于返回的字符数是否大于或等于*BufferLength*中的连接字符串\* *OutConnectionString*截断为*BufferLength*减 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE，或 SQL_STILL_EXECUTING 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBrowseConnect**返回 SQL_ERROR、 SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*ConnectionHandle 句柄*。 下表列出了通常返回的 SQLSTATE 值**SQLBrowseConnect**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*不是否足够大以返回整个浏览结果连接字符串，因此字符串被截断。 缓冲区 **StringLength2Ptr*包含未截断的浏览结果连接字符串的长度。 （函数返回 SQL_NEED_DATA。）|  
|01S00|无效的连接字符串属性|浏览请求连接字符串中指定了无效的属性关键字 (*InConnectionString*)。 （函数返回 SQL_NEED_DATA。）<br /><br /> 在浏览请求连接字符串中指定的属性关键字 (*InConnectionString*) 不适用于当前的连接级别。 （函数返回 SQL_NEED_DATA。）|  
|01S02|值已更改|该驱动程序不支持的指定的值*ValuePtr*中的参数**SQLSetConnectAttr**和替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|连接名称已在使用|(DM) 指定的连接已用于建立与数据源的连接，并且连接已打开。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已尝试连接到数据源之间的通信链接。|  
|28000|无效的授权说明|用户标识符或授权字符串或是两者，指定在中，浏览请求连接字符串 (*InConnectionString*)，违反数据源定义的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|(DM) 驱动程序管理器无法分配支持执行或函数完成所需的内存。<br /><br /> 该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|异步操作已取消通过调用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。 然后，原始函数上调用了再次*ConnectionHandle*。<br /><br /> 操作被取消通过调用**SQLCancelHandle**上*ConnectionHandle*从多线程应用程序中的不同线程。|  
|HY010|函数序列错误|(DM) 以异步方式执行的函数 （而不是此的一个） 曾为*ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*StringLength1*小于 0 并且不等于 sql_nts 以。<br /><br /> (DM) 参数指定的值*BufferLength*小于 0。|  
|HY114|驱动程序不支持连接级别的异步函数执行|(DM) 启用应用程序上连接句柄之前建立的连接的异步操作。 但是，该驱动程序不支持连接句柄上的异步操作。|  
|HYT00|超时时间已到|登录超时期限过期之前完成数据源的连接。 通过设置的超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应于指定的数据源名称的驱动程序不支持该函数。|  
|IM002|找不到的数据源和未指定的默认驱动程序|(DM) 的数据源浏览请求连接字符串中指定的名称 (*InConnectionString*) 中的系统信息中，未找到，也没有默认驱动程序规范。<br /><br /> (DM) 的系统信息中找不到 ODBC 数据源和默认驱动程序信息。|  
|IM003|无法加载指定的驱动程序|(DM) 驱动程序中的系统信息的数据源规范中列出，或者通过指定**驱动程序**关键字找不到或无法加载其他原因。|  
|IM004|驱动程序的**SQLAllocHandle**上失败的 SQL 句柄 _ENV|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*HandleType* SQL_HANDLE_ENV 和驱动程序的返回错误。|  
|IM005|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_DBC 失败|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*HandleType* SQL_HANDLE_DBC 和驱动程序的返回错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数和驱动程序返回了一个错误。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为数据源或目标的连接指定的 DLL。|  
|IM010|数据源名称太长|(DM) DSN 关键字的特性值长于 SQL_MAX_DSN_LENGTH 字符。|  
|IM011|驱动程序名称太长|(DM) 驱动程序关键字的特性值长于 255 个字符。|  
|IM012|驱动程序关键字语法错误|(DM) 驱动程序关键字的关键字 / 值对包含语法错误。|  
|IM014|指定的 DSN 包含的驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用连接到 64 位驱动程序; DSN反之亦然。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当该驱动程序不支持异步通知时，不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 自变量  
 浏览请求连接字符串具有以下语法：  
  
 *连接字符串*:: =*属性*[`;`] &#124; *属性* `;` *连接字符串*;<br>
 *属性*:: =*属性关键字*`=`*属性值* &#124; `DRIVER=`[`{`]*属性-值*[`}`]<br>
 *零个以上*:: = `DSN` &#124; `UID` &#124; `PWD` &#124; *驱动程序的定义的零个以上*<br>
 *属性值*:: =*字符串*<br>
 *驱动程序的定义的零个以上*:: =*标识符*<br>
  
 其中*字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*属性关键字*不区分大小写;*属性值*可能区分大小写; 和的值**DSN**关键字不由单独的空格组成。 由于连接字符串和初始化文件语法、 关键字和属性值，包含字符 **[]{}（)，;？\*= ！ @** 应当避免。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。 适用于 ODBC 2。*x*驱动程序，大括号所需的驱动程序关键字在属性值。  
  
 如果任何关键字都重复浏览请求连接字符串中显示，驱动程序将使用与关键字的第一个匹配项关联的值。 如果**DSN**和**驱动程序**相同的浏览请求连接字符串中包含关键字，驱动程序管理器和驱动程序使用任何关键字将出现第一个。  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 自变量  
 浏览结果连接字符串是连接属性的列表。 连接属性由属性关键字和相应的属性值组成。 浏览结果连接字符串具有以下语法：  
  
 *连接字符串*:: =*属性*[`;`] &#124; *属性* `;` *连接字符串*<br>
 *属性*:: = [`*`]*属性关键字*`=`*属性值*<br>
 *零个以上*:: = *ODBC 属性关键字* &#124; *驱动程序的定义的零个以上*<br>
 *ODBC 属性关键字*= {`UID` &#124; `PWD`} [`:`*本地化标识符*]*驱动程序的定义的零个以上*:: = *标识符*[`:`*本地化标识符*]*属性值*:: = `{` *属性值列表* `}` &#124; `?` （大括号是文本的; 它们返回由驱动程序）。<br>
 *属性值列表*:: =*字符串*[`:`*本地化字符串*] &#124; *字符串*[`:`*本地化字符串*] `,` *属性值列表*<br>
  
 其中*字符串*和*本地化字符串*有零个或多个字符;*标识符*和*本地化标识符*具有一个或多个字符;*属性关键字*不区分大小写; 和*属性值*可能区分大小写。 由于连接字符串和初始化文件语法、 关键字、 本地化的标识符和属性包含字符的值，则 **[]{}（)，;？\*= ！ @** 应当避免。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 浏览结果连接字符串语法可根据以下语义规则：  
  
-   如果一个星号 (\*) 之前*属性关键字*、*属性*是可选的可以在的后续调用中省略**SQLBrowseConnect**。  
  
-   属性关键字**UID**和**PWD**中定义具有相同的含义**SQLDriverConnect**。  
  
-   A*驱动程序的定义的零个以上*名称可能会为其提供的属性值的属性的类型。 例如，它可能是**服务器**，**数据库**，**主机**，或**DBMS**。  
  
-   *ODBC 属性关键字*和*驱动程序的定义的属性的关键字*包括关键字的本地化或用户友好版本。 这可能用作应用程序的对话框中的标签。 但是， **UID**， **PWD**，或*标识符*单独时，必须使用将浏览请求字符串传递给该驱动程序。  
  
-   {*属性值列表*} 是实际值的枚举有效相应*属性关键字*。 请注意，大括号 ({}) 不会指示的选择列表的; 它们返回由驱动程序。 例如，它可能是服务器名称的列表或数据库名称的列表。  
  
-   如果*属性值*是一个问号 （？），单个值对应于*属性关键字*。 例如，UID = 约翰;PWD = 芝麻。  
  
-   每次调用**SQLBrowseConnect**返回仅需满足连接过程的下一个级别的信息。 以便可以始终在每次调用中确定上下文，该驱动程序将与连接句柄关联的状态信息。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect**需要分配的连接。 驱动程序管理器将加载驱动程序中指定或相对应的初始浏览请求连接字符串; 中指定的数据源名称有关在这种情况的信息，请参阅中的"注释"部分[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。 该驱动程序可能需要建立与数据源的连接在浏览过程。 如果**SQLBrowseConnect**返回 SQL_ERROR，未完成连接将终止，并且连接返回到未连接状态。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支持连接池。 如果**SQLBrowseConnect**时启用了连接池，称为 SQLSTATE HY000 将返回 （常规错误）。  
  
 当**SQLBrowseConnect**称为第一次在连接上，浏览请求连接字符串必须包含**DSN**关键字或**驱动程序**关键字。 如果浏览请求连接字符串包含**DSN**关键字，驱动程序管理器在系统信息中找到相应的数据源说明：  
  
-   如果驱动程序管理器找到相应的数据源规范，它将加载相关的驱动程序 DLL;该驱动程序可以从系统信息中检索有关数据源的信息。  
  
-   如果驱动程序管理器无法找到相应的数据源规范，它查找默认数据源说明并加载 DLL; 关联的驱动程序该驱动程序可以从系统信息中检索有关默认数据源的信息。 为 DSN 情况下，"默认"传递到该驱动程序中。  
  
-   如果驱动程序管理器找不到相应的数据源规范并且没有任何默认数据源规范，它将返回与 SQLSTATE IM002 SQL_ERROR （找不到的数据源和未指定的默认驱动程序）。  
  
 如果浏览请求连接字符串包含**驱动程序**关键字，驱动程序管理器加载指定的驱动程序; 它不会尝试找到数据源中的系统信息。 因为**驱动程序**关键字不使用中的系统信息的信息，该驱动程序必须定义足够的关键字，以使驱动程序可以连接到数据源使用浏览请求连接字符串中仅的信息。  
  
 每次调用**SQLBrowseConnect**，应用程序浏览请求连接字符串中指定的连接属性值。 该驱动程序返回属性和属性值的连续的级别中浏览结果连接字符串;只要有具有未尚未被枚举浏览请求连接字符串中的连接属性，它返回 SQL_NEED_DATA。 应用程序使用浏览结果连接字符串的内容生成的后续调用浏览请求连接字符串**SQLBrowseConnect**。 所有必选的属性 (那些在星号前面没有*OutConnectionString*自变量) 中的后续调用都必须包含**SQLBrowseConnect**。 请注意，生成当前浏览请求的连接字符串; 时，应用程序不能使用的以前浏览结果连接字符串的内容也就是说，它不能指定不同的值在上一级别中设置的属性。  
  
 连接和其关联的属性的所有级别具有都枚举，该驱动程序返回 SQL_SUCCESS、 到数据源的连接已完成，并完成连接字符串返回到应用程序。 使用，结合适合的连接字符串**SQLDriverConnect**，并 SQL_DRIVER_NOPROMPT 可以建立其他连接。 完整的连接字符串不能在另一个调用**SQLBrowseConnect**，但是; 如果**SQLBrowseConnect**再次，整个调用者必须重复调用的顺序。  
  
 **SQLBrowseConnect**也会返回 SQL_NEED_DATA 如果期间浏览过程; 例如，一个无效密码或应用程序提供的属性关键字有可恢复的、 非致命错误。 当返回 SQL_NEED_DATA 和浏览结果连接字符串未发生更改，出现错误和应用程序可以调用**SQLGetDiagRec**返回浏览时错误的 SQLSTATE。 这允许应用程序，此属性更正并继续浏览。  
  
 应用程序可以终止浏览进程在任何时候通过调用**SQLDisconnect**。 该驱动程序将终止任何未完成连接数，并将连接返回到未连接状态。  
  
 如果连接句柄上, 启用了异步操作**SQLBrowseConnect**也可能返回 SQL_STILL_EXECUTING。 当此方法返回 SQL_NEED_DATA 时，应用程序必须使用**SQLDisconnect**取消要浏览过程。 如果**SQLBrowseConnect**返回 SQL_STILL_EXECUTING，应用程序应使用**SQLCancelHandle**取消正在进行的操作。 调用**SQLCancelHandle**函数返回 SQL_NEED_DATA 不起作用后。  
  
 有关详细信息，请参阅[使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驱动程序支持**SQLBrowseConnect**，驱动程序的系统信息中的驱动程序关键字部分必须包含**ConnectFunctions**与第三个字符的关键字设置为"Y"。  
  
## <a name="code-example"></a>代码示例  
  
> [!NOTE]  
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定`Trusted_Connection=yes`而不是连接字符串中的用户 ID 和密码信息。  
  
 在下面的示例中，应用程序调用**SQLBrowseConnect**重复。 每次**SQLBrowseConnect**返回 SQL_NEED_DATA，它将传递它需要的数据后信息\* *OutConnectionString*。 应用程序传递*OutConnectionString*到其例程**GetUserInput** （未显示）。 **GetUserInput**分析信息、 生成并显示一个对话框，并返回中的用户输入的信息\* *InConnectionString*。 应用程序将用户的信息传递给的后续调用中的驱动程序**SQLBrowseConnect**。 应用程序提供了驱动程序连接到数据源中，所有所需的信息后**SQLBrowseConnect**返回 SQL_SUCCESS 和应用程序将继续。  
  
 有关通过调用连接到 SQL Server 驱动程序的更多详细示例**SQLBrowseConnect**，请参阅[SQL 服务器浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，若要连接到数据源销售，可能会执行下列操作。 首先，应用程序传递的下列字符串**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 驱动程序管理器将加载驱动程序与数据源销售相关联。 然后，它调用驱动程序的**SQLBrowseConnect**与它从应用程序收到的相同自变量的函数。 驱动程序返回中的以下字符串 **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 应用程序传递此字符串到其**GetUserInput**例程，哪些生成一个对话框，询问用户能够选择红色、 蓝色，或绿色服务器并输入用户 ID 和密码。 以下用户指定信息重新例程传递\* *InConnectionString*，应用程序传递给**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**使用此信息来使用密码芝麻，作为 Smith 连接到红色的服务器，然后返回中的以下字符串 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 应用程序传递此字符串到其**GetUserInput**例程，哪些生成一个对话框，要求用户选择一个数据库。 用户选择 empdata 和应用程序调用**SQLBrowseConnect**最后一次与此字符串：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 这是最后一段信息该驱动程序必须连接到数据源;**SQLBrowseConnect**返回 SQL_SUCCESS，和 **OutConnectionString*包含已完成的连接字符串：  
  
```  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配连接句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|从数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回驱动程序说明和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放连接句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
