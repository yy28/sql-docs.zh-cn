---
title: SQLBrowseConnect 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe1b9c7d3d93604e2f19de754ff25517ef23cb07
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211707"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支持发现和枚举的属性和属性值连接到数据源所需的迭代方法。 每次调用**SQLBrowseConnect**返回连续级别的属性和属性值。 在所有级别都已都枚举，完成与数据源的连接并且返回完整的连接字符串**SQLBrowseConnect**。 返回代码为 SQL_SUCCESS 或 sql_success_with_info 以指示已指定所有连接信息和应用程序现在已连接到数据源。  
  
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
 [输入]浏览请求连接字符串 (请参阅"*InConnectionString*参数"中"注释")。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*以字符为单位。  
  
 *OutConnectionString*  
 [输出]指向用于返回浏览结果连接字符串的字符缓冲区 (请参阅"*OutConnectionString*参数"中"注释")。  
  
 如果*OutConnectionString*为 NULL， *StringLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于在缓冲区中返回指向*OutConnectionString*。  
  
 *BufferLength*  
 [输入]长度，以字符为单位的 **OutConnectionString*缓冲区。  
  
 *StringLength2Ptr*  
 [输出]字符 （不包括 null 终止） 可用于在返回总数\* *OutConnectionString*。 可用于返回的字符数是否大于或等于*BufferLength*中的连接字符串\* *OutConnectionString*截断为*BufferLength*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBrowseConnect**返回 SQL_ERROR，SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*ConnectionHandle 的句柄*。 下表列出了通常返回的 SQLSTATE 值**SQLBrowseConnect** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*是否不足够大以返回整个浏览结果连接字符串，因此已截断。 缓冲区 **StringLength2Ptr*包含未截断的浏览结果连接字符串的长度。 （函数返回 SQL_NEED_DATA。）|  
|01S00|连接字符串属性无效|浏览请求连接字符串中指定一个无效的属性的关键字 (*InConnectionString*)。 （函数返回 SQL_NEED_DATA。）<br /><br /> 浏览请求连接字符串中指定一个属性的关键字 (*InConnectionString*)，不适用于当前连接级别。 （函数返回 SQL_NEED_DATA。）|  
|01S02|值已更改|该驱动程序不支持的指定的值*ValuePtr*中的参数**SQLSetConnectAttr**和替换一个相近的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|在使用的连接名称|(DM) 指定的连接已用于建立与数据源的连接，并且连接已打开。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已尝试连接到的数据源之间的通信链接失败之前函数已完成处理。|  
|28000|无效的授权说明|用户标识符或授权字符串或同时在中，浏览指定请求的连接字符串 (*InConnectionString*)，违反定义的数据源的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|无法分配内存支持执行或完成该函数所需的驱动程序管理器中 (DM)。<br /><br /> 该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步操作已取消通过调用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。 然后，原始函数上再次调用*ConnectionHandle*。<br /><br /> 操作已取消通过调用**SQLCancelHandle**上*ConnectionHandle*从多线程应用程序中不同的线程。|  
|HY010|函数序列错误|(DM) 的调用以异步方式执行的函数 （不是此类似） *ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*StringLength1*小于 0 且不等于 SQL_NTS。<br /><br /> (DM) 为参数指定的值*BufferLength*小于 0。|  
|HY114|驱动程序不支持连接级别的异步函数执行|(DM) 应用程序启用对连接句柄之前建立的连接的异步操作。 但是，该驱动程序不支持连接句柄上的异步操作。|  
|HYT00|超时时间已到|登录超时期限过期之前完成的数据源的连接。 通过设置超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 与指定的数据源名称对应的驱动程序不支持该函数。|  
|IM002|找不到数据源和未指定的默认驱动程序|(DM) 的数据源浏览请求连接字符串中指定的名称 (*InConnectionString*) 系统信息中未找到，也没有默认驱动程序规范。<br /><br /> (DM) 的系统信息中找不到 ODBC 数据源和默认驱动程序信息。|  
|IM003|无法加载指定的驱动程序|(DM) 驱动程序的系统信息中的数据源规范中列出或由指定**驱动程序**关键字找不到或无法加载某些其他原因。|  
|IM004|驱动程序的**SQLAllocHandle**上 SQL_HANDLE _ENV 失败|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*HandleType* SQL_HANDLE_ENV 和驱动程序返回出现错误。|  
|IM005|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_DBC 失败|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*HandleType* SQL_HANDLE_DBC 和驱动程序返回出现错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|(DM) 期间**SQLBrowseConnect**，驱动程序管理器调用的驱动程序**SQLSetConnectAttr**函数和驱动程序返回了错误。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为数据源或为连接指定的 DLL。|  
|IM010|数据源名称太长|(DM) DSN 关键字的特性值已超过 SQL_MAX_DSN_LENGTH 个字符。|  
|IM011|驱动程序的名称太长|(DM) 驱动程序关键字的特性值已超过 255 个字符。|  
|IM012|驱动程序关键字语法错误|(DM) 驱动程序关键字的关键字值对包含语法错误。|  
|IM014|指定的 DSN 包含驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，您不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 参数  
 浏览请求连接字符串具有以下语法：  
  
 *连接字符串*:: =*特性*[`;`] &#124; *特性* `;` *连接字符串*;<br>
 *特性*:: =*特性关键字*`=`*属性值* &#124; `DRIVER=`[`{`]*属性-值*[`}`]<br>
 *零个以上*:: = `DSN` &#124; `UID` &#124; `PWD` &#124; *驱动程序的定义的属性的关键字*<br>
 *属性值*:: =*字符字符串*<br>
 *驱动程序的定义的零个以上*:: =*标识符*<br>
  
 其中*字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*特性关键字*不区分大小写;*属性值*可能是区分大小写; 和的值**DSN**关键字不会包含单独的空格。 由于连接字符串和初始化文件语法、 关键字和属性值包含字符 **[]{}（)，;？\*= ！ @** 应避免使用。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。 适用于 ODBC 2。*x*驱动程序，大括号，则必须在 DRIVER 关键字的特性值。  
  
 如果在浏览请求连接字符串中有重复任何关键字，驱动程序将使用与关键字的第一个匹配项关联的值。 如果**DSN**并**驱动程序**包括在相同浏览请求连接字符串中的关键字，驱动程序管理器和驱动程序使用任何关键字将出现第一个。  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 参数  
 浏览结果连接字符串是连接属性的列表。 连接属性包括特性关键字和相应的属性值。 浏览结果连接字符串具有以下语法：  
  
 *连接字符串*:: =*特性*[`;`] &#124; *特性* `;` *连接字符串*<br>
 *特性*:: = [`*`]*特性关键字*`=`*属性值*<br>
 *零个以上*:: = *ODBC 属性关键字* &#124; *驱动程序的定义的属性的关键字*<br>
 *ODBC 属性关键字*= {`UID` &#124; `PWD`} [`:`*本地化标识符*]*驱动程序的定义的零个以上*:: = *标识符*[`:`*本地化标识符*]*属性值*:: = `{` *属性值列表* `}` &#124; `?` （大括号都是文本; 中返回的驱动程序。）<br>
 *属性值列表*:: =*字符串*[`:`*本地化字符的字符串*] &#124; *字符串*[`:`*本地化字符的字符串*] `,` *属性值列表*<br>
  
 其中*字符串*并*本地化字符的字符串*具有零个或多个字符;*标识符*并*本地化标识符*具有一个或多个字符;*特性关键字*不区分大小写; 并*属性值*可能区分大小写。 由于连接字符串和初始化文件语法、 关键字、 本地化的标识符和属性值包含字符 **[]{}（)，;？\*= ！ @** 应避免使用。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 按照以下的语义规则使用的浏览结果连接字符串语法：  
  
-   如果星号 (\*) 之前*特性关键字*，则*特性*是可选的可以在的后续调用中省略**SQLBrowseConnect**。  
  
-   属性关键字**UID**并**PWD**中定义具有相同的含义**SQLDriverConnect**。  
  
-   一个*驱动程序的定义的零个以上*名称可能会提供的属性值的属性的类型。 例如，可能**服务器**，**数据库**，**主机**，或者**DBMS**。  
  
-   *ODBC 属性关键字*并*驱动程序的定义的属性的关键字*包含关键字的本地化或用户友好版本。 这可能用作应用程序的对话框中的标签。 但是， **UID**， **PWD**，或*标识符*单独时，必须使用将浏览请求字符串传递给驱动程序。  
  
-   {*属性值列表*} 是一个枚举，实际值的有效相应*特性关键字*。 请注意，大括号 ({}) 未指示进行的选择列表; 中返回的驱动程序。 例如，它可能是服务器名称的列表或数据库名称的列表。  
  
-   如果*属性值*是一个问号 （？），单个值对应于*特性关键字*。 例如，UID = 约翰;PWD = Sesame。  
  
-   每次调用**SQLBrowseConnect**返回仅将满足下一级别的连接过程所需的信息。 该驱动程序相关联的状态信息的连接句柄，以便始终可以确定在每次调用的上下文。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect**需要分配的连接。 驱动程序管理器将加载驱动程序中未指定或对应于初始浏览请求连接字符串; 中指定的数据源名称在这种情况的信息，请参阅中的"注释"部分[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。 该驱动程序可能会建立与数据源在浏览过程中的连接。 如果**SQLBrowseConnect**返回 SQL_ERROR，未完成连接都将终止并且连接返回到未连接状态。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支持连接池。 如果**SQLBrowseConnect**启用连接池时，称为 SQLSTATE HY000 将返回 （常规错误）。  
  
 当**SQLBrowseConnect**称为第一次连接上，浏览请求连接字符串必须包含**DSN**关键字或**驱动程序**关键字。 如果浏览请求连接字符串包含**DSN**关键字，驱动程序管理器的系统信息中查找相应的数据源说明：  
  
-   如果驱动程序管理器找到相应的数据源规范，它将加载 DLL; 关联的驱动程序该驱动程序可以检索有关数据源的信息中的系统信息。  
  
-   如果驱动程序管理器找不到相应的数据源规范，它查找默认数据源说明，并将加载 DLL; 关联的驱动程序该驱动程序可以检索有关默认数据源的信息中的系统信息。 "DEFAULT"被传递给驱动程序的 DSN。  
  
-   如果驱动程序管理器找不到相应的数据源规范并且没有任何默认数据源的规范，它将返回 SQL_ERROR 具有 SQLSTATE IM002 （找不到数据源和未指定的默认驱动程序）。  
  
 如果浏览请求连接字符串包含**驱动程序**关键字，驱动程序管理器加载指定的驱动程序; 它不会尝试查找数据源中的系统信息。 因为**驱动程序**关键字不使用系统信息中的信息，该驱动程序必须定义足够的关键字，以便驱动程序可以连接到数据源在浏览请求连接字符串中使用的信息。  
  
 每次调用**SQLBrowseConnect**，应用程序浏览请求连接字符串中指定连接属性值。 驱动程序返回属性和属性值的连续的级别中浏览结果连接字符串;只要有没有被列举浏览请求连接字符串中的连接属性，它将返回 SQL_NEED_DATA。 应用程序使用浏览结果连接字符串的内容来生成浏览请求连接字符串的下一个调用到**SQLBrowseConnect**。 所有必需的属性 (与前面没有一个星号*OutConnectionString*参数) 的后续调用中必须包括**SQLBrowseConnect**。 请注意，生成当前浏览请求的连接字符串; 时，应用程序不能使用的上一个浏览结果连接字符串的内容也就是说，它不能指定不同的值在上一级别中设置的属性。  
  
 连接和及其相关的属性的所有级别都已都枚举，驱动程序返回 SQL_SUCCESS，与数据源的连接完成，并且完整的连接字符串返回到应用程序。 连接字符串是适合使用结合**SQLDriverConnect**，建立另一个连接的 SQL_DRIVER_NOPROMPT 选项。 不能对另一个调用中使用的完整连接字符串**SQLBrowseConnect**，但是; 如果**SQLBrowseConnect**再次，整个调用的调用序列将不得不重复。  
  
 **SQLBrowseConnect**如果期间浏览过程; 例如，一个无效密码或应用程序所提供的属性关键字有可恢复的、 非致命错误也会返回 SQL_NEED_DATA。 当将返回 SQL_NEED_DATA 和浏览结果连接字符串是不变，出现错误时，应用程序可以调用**SQLGetDiagRec**返回浏览时错误的 SQLSTATE。 这允许要更正该属性并继续浏览的应用程序。  
  
 应用程序可以终止浏览进程在任何时候通过调用**SQLDisconnect**。 驱动程序将终止任何未完成的连接，并将连接返回到未连接状态。  
  
 如果连接句柄上, 启用了异步操作**SQLBrowseConnect**可能也会返回 SQL_STILL_EXECUTING。 应用程序时它将返回 SQL_NEED_DATA，必须使用**SQLDisconnect**取消浏览过程。 如果**SQLBrowseConnect**返回 SQL_STILL_EXECUTING，应用程序应使用**SQLCancelHandle**取消正在进行的操作。 调用**SQLCancelHandle**该函数将返回 sql_need_data，这不起作用后。  
  
 有关详细信息，请参阅[使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驱动程序支持**SQLBrowseConnect**，该驱动程序的系统信息中的驱动程序关键字部分必须包含**ConnectFunctions**与第三个字符的关键字设置为"Y"。  
  
## <a name="code-example"></a>代码示例  
  
> [!NOTE]  
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定`Trusted_Connection=yes`而不是在连接字符串中的用户 ID 和密码信息。  
  
 在以下示例中，应用程序调用**SQLBrowseConnect**重复。 每次**SQLBrowseConnect**返回 SQL_NEED_DATA，它将传递中需要的数据后信息\* *OutConnectionString*。 应用程序传递*OutConnectionString*到其例程**GetUserInput** （未显示）。 **GetUserInput**分析信息、 生成和显示一个对话框，并返回在用户输入的信息\* *InConnectionString*。 应用程序将用户的信息传递给下一个调用中的驱动程序**SQLBrowseConnect**。 应用程序提供了驱动程序连接到数据源的所有必要信息后**SQLBrowseConnect**返回 SQL_SUCCESS 和应用程序将继续。  
  
 有关通过调用连接到 SQL Server 驱动程序的更详细的示例**SQLBrowseConnect**，请参阅[SQL Server 浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，若要连接到数据源销售，以下操作可能会出现。 首先，应用程序传递到下面的字符串**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 驱动程序管理器将加载驱动程序与数据源销售相关联。 然后，它调用的驱动程序**SQLBrowseConnect**与它来自应用程序的相同自变量的函数。 驱动程序将返回以下字符串中的 **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 应用程序传递到此字符串及其**GetUserInput**例程，哪些生成一个对话框，要求用户选择红色、 蓝色和绿色服务器并输入用户 ID 和密码。 常规传递以下用户指定信息重新\* *InConnectionString*，该应用程序将传递给**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**使用此信息来使用密码 Sesame，作为 Smith 连接到红色的服务器，然后返回中的以下字符串 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 应用程序传递到此字符串及其**GetUserInput**例程，哪些生成一个对话框，要求用户选择一个数据库。 用户选择 empdata 和应用程序调用**SQLBrowseConnect**最后一次使用此字符串：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 这是信息的驱动程序连接到数据源; 所需的最后一个部分**SQLBrowseConnect**始终返回 SQL_SUCCESS，和 **OutConnectionString*包含已完成的连接字符串：  
  
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
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回驱动程序说明和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放连接句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
