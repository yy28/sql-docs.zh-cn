---
title: SQLBrowse连接功能 |微软文档
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301337"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支持一种迭代方法，用于发现和枚举连接到数据源所需的属性和属性值。 对**SQLBrowseConnect**的每个调用都返回连续的属性和属性值级别。 枚举所有级别后，完成与数据源的连接 **，SQLBrowseConnect**返回完整的连接字符串。 SQL_SUCCESS或SQL_SUCCESS_WITH_INFO的返回代码表示已指定所有连接信息，并且应用程序现在已连接到数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
 *连接字符串*  
 [输入]浏览请求连接字符串（请参阅"注释"中的"*连接字符串*参数"）。  
  
 *字符串长度1*  
 [输入]字符中的 *"连接字符串"* 的长度。  
  
 *外连接字符串*  
 [输出]指向要返回浏览结果连接字符串的字符缓冲区的指针（请参阅"注释"中的 *"OutConnectString*参数"）。  
  
 如果*OutConnectString*为 NULL，*则 StringLength2Ptr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*OutConnectionString*指向的缓冲区中返回。  
  
 *缓冲区长度*  
 [输入]**外连接字符串*缓冲区的长度（以字符表示）。  
  
 *字符串长度2Ptr*  
 [输出]可在\**OutConnectionString*中返回的字符总数（不包括空终止）。 如果可用于返回的字符数大于或等于*BufferLength，* 则\**OutConnectionString*中的连接字符串将截断为*BufferLength*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBrowseConnect**返回SQL_ERROR、SQL_SUCCESS_WITH_INFO 或SQL_NEED_DATA时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*连接句柄的句柄*。 下表列出了**SQLBrowseConnect**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*不够大，无法返回整个浏览结果连接字符串，因此该字符串被截断。 缓冲区 =*StringLength2Ptr*包含未压缩的浏览结果连接字符串的长度。 （函数返回SQL_NEED_DATA。|  
|01S00|无效的连接字符串属性|在浏览请求连接字符串 *（InConnectString）* 中指定了无效的属性关键字。 （函数返回SQL_NEED_DATA。<br /><br /> 在浏览请求连接字符串 （*InConnectionString*） 中指定了不适用于当前连接级别的属性关键字。 （函数返回SQL_NEED_DATA。|  
|01S02|值已更改|驱动程序不支持**SQLSetConnectAttr**中*ValuePtr*参数的指定值，并替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08001|客户端无法建立连接|驱动程序无法与数据源建立连接。|  
|08002|正在使用的连接名称|（DM） 指定的连接已用于与数据源建立连接，并且连接已打开。|  
|08004|服务器拒绝连接|数据源出于实现定义的原因拒绝建立连接。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序尝试连接到的数据源之间的通信链路失败。|  
|28000|无效的授权规范|用户标识符或授权字符串或两者（如浏览请求连接字符串 *（InConnectionString）* 中指定）都违反了数据源定义的限制。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|（DM） 驱动程序管理器无法分配支持执行或完成函数所需的内存。<br /><br /> 驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|通过调用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，异步操作被取消。 然后，在*ConnectHandle*上再次调用原始函数。<br /><br /> 通过在*连接句柄*上从多线程应用程序中的不同线程调用**SQLCancelHandle，** 操作被取消。|  
|HY010|函数序列错误|（DM） 为*ConnectHandle*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*StringLength1*指定的值小于 0，不等于SQL_NTS。<br /><br /> （DM） 为参数*BufferLength*指定的值小于 0。|  
|HY114|驱动程序不支持连接级异步功能执行|（DM） 在进行连接之前，应用程序在连接句柄上启用了异步操作。 但是，驱动程序不支持对连接句柄进行异步操作。|  
|HYT00|超时时间已到|与数据源的连接完成之前，登录超时期限已过期。 超时期间通过**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 对应于指定数据源名称的驱动程序不支持该函数。|  
|IM002|找不到数据源，未指定默认驱动程序|（DM） 在系统信息中找不到浏览请求连接字符串 *（InConnectionString）* 中指定的数据源名称，也没有默认驱动程序规范。<br /><br /> （DM） ODBC 数据源和默认驱动程序信息在系统信息中找不到。|  
|IM003|无法加载指定的驱动程序|（DM） 由于其他原因找不到或无法加载**DRIVER**关键字中数据源规范中列出的驱动程序。|  
|IM004|驱动程序的**SQLAllocHandle**上SQL_HANDLE_ENV失败|（DM） 在**SQLBrowseConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，该*函数的句柄类型*为 SQL_HANDLE_ENV，驱动程序返回了错误。|  
|IM005|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_DBC 失败|（DM） 在**SQLBrowseConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，具有SQL_HANDLE_DBC的*句柄类型*，驱动程序返回了错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|（DM） 在**SQLBrowseConnect**期间，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数，驱动程序返回错误。|  
|IM009|无法加载转换 DLL|驱动程序无法加载为数据源或连接指定的转换 DLL。|  
|IM010|数据源名称太长|（DM） DSN 关键字的属性值大于SQL_MAX_DSN_LENGTH个字符。|  
|IM011|驱动程序名称太长|（DM） DRIVER 关键字的属性值超过 255 个字符。|  
|IM012|驱动程序关键字语法错误|（DM） DRIVER 关键字的关键字值对包含语法错误。|  
|IM014|指定的 DSN 包含驱动程序和应用程序之间的体系结构不匹配|（DM） 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，无法设置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>连接字符串参数  
 浏览请求连接字符串具有以下语法：  
  
 *连接字符串*：：**属性*`;`= &#124;*属性*`;`*连接字符串*;<br>
 *属性*：：**属性关键字*`=`*属性值*&#124; `DRIVER=`=`{`属性*值*|`}`<br>
 *属性关键字*：：* `DSN` `UID` &#124;&#124;&#124;`PWD`*驱动程序定义的属性关键字*<br>
 *属性值*：：**字符字符串*<br>
 *驱动程序定义的属性关键字*：：**标识符*<br>
  
 *其中字符字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*属性关键字*不区分大小写;*属性值*可能区分大小写;**DSN**关键字的值不只包含空白。 由于连接字符串和初始化文件语法，包含字符的关键字和属性值 ***（）、？？{}应\*避免[！]** 。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 （\\） 字符。 对于 ODBC 2。*x*驱动程序，在 DRIVER 关键字的属性值周围需要大括号。  
  
 如果在浏览请求连接字符串中重复任何关键字，驱动程序将使用与关键字的第一次出现关联的值。 如果**DSN**和**DRIVER**关键字包含在相同的浏览请求连接字符串中，则驱动程序管理器和驱动程序首先使用哪个关键字出现。  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>外连接字符串参数  
 浏览结果连接字符串是连接属性的列表。 连接属性由属性关键字和相应的属性值组成。 浏览结果连接字符串具有以下语法：  
  
 *连接字符串*：：**attribute*属性`;`= &#124;*属性*`;`*连接字符串*<br>
 *属性*：：*`*`=*属性关键字*`=`*属性值*<br>
 *属性关键字*：：* *ODBC 属性关键字*&#124;*驱动程序定义属性关键字*<br>
 *ODBC 属性关键字*=`UID` &#124; `PWD`=`:`*本地化标识符*=*驱动程序定义的属性关键字*：：：**标识符*=`:`*本地化标识符*=*属性值* `{` ：：：**属性值列表*`}`&#124;（`?`大括号是文本的;它们由驱动程序返回。<br>
 *属性值列表*：：**字符串*`:`=*本地化字符串*= &#124;*字符串*`:`=*本地化字符串*= `,` *属性值列表*<br>
  
 *其中字符字符串*和*本地化字符串*具有零个或多个字符;*标识符*和*本地化标识符*具有一个或多个字符;*属性关键字*不区分大小写;和*属性值*可能区分大小写。 由于连接字符串和初始化文件语法、关键字、本地化标识符和包含字符 ***（）、？？{}应\*避免[！]** 。 由于系统信息中的语法，关键字和数据源名称不能包含反斜杠 （\\） 字符。  
  
 浏览结果连接字符串语法根据以下语义规则使用：  
  
-   如果星号\*（ ） 在*属性关键字*之前，*则属性*是可选的，可以在**SQLBrowseConnect**的下一次调用中省略 。  
  
-   属性关键字**UID**和**PWD**的含义与**SQLDriverConnect**中定义的含义相同。  
  
-   *驱动程序定义的属性关键字*为可以提供属性值的属性类型命名。 例如，它可能是**服务器**、**数据库**、**主机**或**DBMS**。  
  
-   *ODBC 属性关键字*和*驱动程序定义的属性关键字*包括关键字的本地化或用户友好版本。 应用程序可能会将其用作对话框中的标签。 但是，在将浏览请求字符串传递给驱动程序时，必须单独使用**UID** **、PWD**或*标识符*。  
  
-   [*属性-值列表*] 是对相应*属性关键字*有效的实际值的枚举。 请注意，大括号 （{}） 不指示选项列表;因此，如果大括号 （ ） 不指示选项列表。它们由司机返回。 例如，它可能是服务器名称的列表或数据库名称的列表。  
  
-   如果*属性值*是单个问号 （？），则单个值对应于*属性关键字*。 例如，UID_JohnS;PWD_芝麻。  
  
-   每次对**SQLBrowseConnect**的调用都仅返回满足连接过程下一个级别所需的信息。 驱动程序将状态信息与连接句柄关联，以便始终可以在每次调用时确定上下文。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowse 连接  
 **SQLBrowseConnect**需要分配的连接。 驱动程序管理器加载在初始浏览请求连接字符串中指定或对应于初始浏览请求连接字符串中指定的数据源名称的驱动程序;有关发生这种情况的信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)中的"注释"部分。 在浏览过程中，驱动程序可能与数据源建立连接。 如果**SQLBrowseConnect**返回SQL_ERROR，则未完成的连接将终止，连接将返回到未连接状态。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支持连接池。 如果在启用连接池时调用**SQLBrowseConnect，** 则返回 SQLSTATE HY000（常规错误）。  
  
 首次在连接上调用**SQLBrowseConnect**时，浏览请求连接字符串必须包含**DSN**关键字或**DRIVER**关键字。 如果浏览请求连接字符串包含**DSN**关键字，驱动程序管理器在系统信息中找到相应的数据源规范：  
  
-   如果驱动程序管理器找到相应的数据源规范，它将加载关联的驱动程序 DLL;如果驱动程序管理器找到相应的数据源规范，则加载相应的驱动程序 DLL。驱动程序可以从系统信息中检索有关数据源的信息。  
  
-   如果驱动程序管理器找不到相应的数据源规范，它将查找默认数据源规范并加载关联的驱动程序 DLL;驱动程序可以从系统信息中检索有关默认数据源的信息。 "DEFAULT"传递给 DSN 的驱动程序。  
  
-   如果驱动程序管理器找不到相应的数据源规范，并且没有默认数据源规范，它将返回 SQL_ERROR SQLSTATE IM002（找不到数据源，未指定默认驱动程序）。  
  
 如果浏览请求连接字符串包含 DRIVER 关键字，则驱动程序管理器将加载指定的驱动程序;如果浏览请求连接字符串包含**DRIVER**关键字，则驱动程序管理器将加载指定的驱动程序。它不尝试在系统信息中查找数据源。 由于**DRIVER**关键字不使用系统信息中的信息，因此驱动程序必须定义足够的关键字，以便驱动程序只能使用浏览请求连接字符串中的信息连接到数据源。  
  
 每次调用**SQLBrowseConnect**时，应用程序都会在浏览请求连接字符串中指定连接属性值。 驱动程序返回浏览结果连接字符串中连续的属性和属性值级别;如果驱动程序，则返回这些值和属性值。只要浏览请求连接字符串中尚未枚举连接属性，它SQL_NEED_DATA返回。 应用程序使用浏览结果连接字符串的内容来构建下一次调用**SQLBrowseConnect**的浏览请求连接字符串。 所有必需属性（在*OutConnectionString*参数中未带有星号的属性）必须包含在**SQLBrowseConnect**的下一次调用中。 请注意，在生成当前浏览请求连接字符串时，应用程序无法使用以前的浏览结果连接字符串的内容;也就是说，它不能为以前级别中设置的属性指定不同的值。  
  
 枚举所有级别的连接及其关联属性后，驱动程序将返回SQL_SUCCESS，与数据源的连接已完成，并且将返回一个完整的连接字符串到应用程序。 连接字符串适合与**SQLDriverConnect**结合使用，SQL_DRIVER_NOPROMPT选项来建立另一个连接。 但是，在**SQLBrowseConnect**的另一个调用中，无法使用完整的连接字符串;如果再次调用**SQLBrowseConnect，** 则必须重复整个调用序列。  
  
 如果浏览过程中存在可恢复的非致命错误 **，SQLBrowseConnect**还会返回SQL_NEED_DATA;例如，应用程序提供的无效密码或属性关键字。 返回SQL_NEED_DATA且浏览结果连接字符串保持不变时，将发生错误，应用程序可以调用**SQLGetDiagRec**返回 SQLSTATE 以获取浏览时间错误。 这允许应用程序更正属性并继续浏览。  
  
 应用程序可以随时通过调用**SQLDisconnect**终止浏览过程。 驱动程序将终止任何未完成的连接，并将连接返回到未连接状态。  
  
 如果在连接句柄上启用了异步操作 **，SQLBrowseConnect**也可能返回SQL_STILL_EXECUTING。 当它返回SQL_NEED_DATA时，应用程序必须使用**SQLDisconnect**来取消浏览过程。 如果**SQLBrowseConnect**返回SQL_STILL_EXECUTING，则应用程序应使用**SQLCancelHandle**取消正在进行的操作。 在函数返回SQL_NEED_DATA返回后调用**SQLCancelHandle**不起作用。  
  
 有关详细信息，请参阅使用[SQLBrowse 连接连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驱动程序支持**SQLBrowseConnect，** 则驱动程序的系统信息中的驱动程序关键字部分必须包含**ConnectFunctions**关键字，第三个字符设置为"Y"。  
  
## <a name="code-example"></a>代码示例  
  
> [!NOTE]  
>  如果要连接到支持 Windows 身份验证的数据源提供程序，则应在连接字符串中指定`Trusted_Connection=yes`而不是用户 ID 和密码信息。  
  
 在下面的示例中，应用程序重复调用**SQLBrowseConnect。** 每次**SQLBrowseConnect**返回SQL_NEED_DATA时，它都会传递有关\**OutConnectString*中所需数据的信息。 应用程序将*OutConnectString*传递给其例程**GetUserInput（** 未显示）。 **GetUserInput**解析信息，生成并显示一个对话框，并返回用户在\**InConnectionString*中输入的信息。 应用程序在下一次调用**SQLBrowseConnect**时将用户的信息传递给驱动程序。 在应用程序为驱动程序连接到数据源提供了所有必要的信息后 **，SQLBrowseConnect**返回SQL_SUCCESS，应用程序将继续。  
  
 有关通过调用**SQLBrowseConnect**连接到 SQL Server 驱动程序的更详细的示例，请参阅[SQL Server 浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，要连接到数据源 Sales，可能会执行以下操作。 首先，应用程序将以下字符串传递给**SQLBrowseConnect**：  
  
```  
"DSN=Sales"  
```  
  
 驱动程序管理器加载与数据源销售关联的驱动程序。 然后，它将调用驱动程序的**SQLBrowseConnect**函数，其参数与从应用程序接收的相同参数相同。 驱动程序返回以下字符串在 +*外连接字符串*：  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 应用程序将此字符串传递给其**GetUserInput**例程，该例程生成一个对话框，要求用户选择红色、蓝色或绿色服务器并输入用户 ID 和密码。 例程将以下用户指定的信息传递回\* *InConnectionString*中，应用程序将这些信息传递给**SQLBrowseConnect**：  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**使用此信息以 Smith 密码芝麻的身份连接到红色服务器，然后在 +*OutConnectString*中返回以下字符串 ：  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 应用程序将此字符串传递给其**GetUserInput**例程，该例程生成一个对话框，要求用户选择数据库。 用户选择 empdata，应用程序使用此字符串调用**SQLBrowse 连接**最后一次：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 这是驱动程序连接到数据源所需的最后一条信息;**SQLBrowseConnect**返回SQL_SUCCESS， 和 **外连接字符串*包含已完成的连接字符串：  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配连接句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回驱动程序描述和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放连接句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
