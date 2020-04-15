---
title: SQLDriver连接功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302768"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLDriverConnect**是**SQLConnect**的替代方法。 它支持比**SQLConnect**中的三个参数（用于提示用户所有连接信息的对话框）和系统信息中未定义的数据源需要更多的连接信息的数据源。  
  
 **SQLDriverConnect**提供以下连接属性：  
  
-   使用包含数据源名称、一个或多个用户密码、一个或多个密码以及数据源所需的其他信息的连接字符串建立连接。  
  
-   使用部分连接字符串或没有附加信息建立连接;在这种情况下，驱动程序管理器和驱动程序可以分别提示用户提供连接信息。  
  
-   建立与系统信息中未定义的数据源的连接。 如果应用程序提供部分连接字符串，驱动程序可以提示用户提供连接信息。  
  
-   使用从 .dsn 文件中的信息构造的连接字符串建立与数据源的连接。  
  
 建立连接后 **，SQLDriverConnect**将返回已完成的连接字符串。 应用程序可以使用此字符串执行后续连接请求。 有关详细信息，请参阅使用[SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
 *窗口句柄*  
 [输入]窗口句柄。 如果窗口句柄不适用或**SQLDriverConnect**不会显示任何对话框，则应用程序可以传递父窗口的句柄（如果适用）或空指针。  
  
 *连接字符串*  
 [输入]完整的连接字符串（请参阅"注释"中的语法）、部分连接字符串或空字符串。  
  
 *字符串长度1*  
 [输入]如果字符串为 Unicode，则长度 =*连接字符串*，或字符串为 ANSI 或 DBCS 的字节。  
  
 *外连接字符串*  
 [输出]指向已完成连接字符串的缓冲区。 成功连接到目标数据源后，此缓冲区包含已完成的连接字符串。 应用程序应为此缓冲区分配至少 1，024 个字符。  
  
 如果*OutConnectString*为 NULL，*则 StringLength2Ptr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*OutConnectionString*指向的缓冲区中返回。  
  
 *缓冲区长度*  
 [输入]**外连接字符串*缓冲区的长度（以字符表示）。  
  
 *字符串长度2Ptr*  
 [输出]指向缓冲区的指针，其中返回可在\**OutConnectString*中返回的字符总数（不包括空终止字符）。 如果可用于返回的字符数大于或等于*BufferLength，* 则\**OutConnectionString*中已完成的连接字符串将截断为*BufferLength*减去空终止字符的长度。  
  
 *驱动程序完成*  
 [输入]指示驱动程序管理器或驱动程序是否必须提示更多连接信息的标志：  
  
 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED或SQL_DRIVER_NOPROMPT。  
  
 （有关其他信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDriverConnect**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有 SQL_HANDLE_DBC 的*fHandleType*和*连接句柄*的*hHandle。* 下表列出了**SQLDriverConnect**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*不够大，无法返回整个连接字符串，因此连接字符串被截断。 未压缩的连接字符串的长度在 [*字符串长度2Ptr*中返回] （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S00|无效的连接字符串属性|在连接字符串 *（InConnectionString）* 中指定了无效属性关键字，但驱动程序无论如何都能够连接到数据源。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持**SQLSetConnectAttr**中的*ValuePtr*参数指向的指定值，并替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S08|错误保存文件 DSN|* \*InConnectString*中的字符串包含一个**FILESN**关键字，但 .dsn 文件未保存。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S09|无效关键字|（DM） * \*InConnectString*中的字符串包含**SAVEFILE**关键字，但不包含**驱动程序**或**FILESN**关键字。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08001|客户端无法建立连接|驱动程序无法与数据源建立连接。|  
|08002|正在使用的连接名称|（DM） 指定的*ConnectHandle*已用于与数据源建立连接，并且连接仍处于打开状态。|  
|08004|服务器拒绝连接|数据源出于实现定义的原因拒绝建立连接。|  
|08S01|通信链路故障|在**SQLDriverConnect**函数完成处理之前，驱动程序与驱动程序尝试连接到的数据源之间的通信链路失败。|  
|28000|无效的授权规范|用户标识符或授权字符串，或连接字符串 *（InConnectionString）* 中指定的两者都违反了数据源定义的限制。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*szMessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY000|一般错误：文件 dsn 无效|（DM） =*InConnectString*中的字符串包含一个 FILESN 关键字，但找不到 .dsn 文件的名称。|  
|HY000|一般错误：无法创建文件缓冲区|（DM） =*InConnectString*中的字符串包含一个 FILESN 关键字，但 .dsn 文件不可读。|  
|HY001|内存分配错误|驱动程序管理器无法分配支持执行或完成**SQLDriverConnect**函数所需的内存。<br /><br /> 驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|为*连接句柄*启用了异步处理。 调用该函数，在完成执行之前，在*ConnectHandle*上调用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，然后在*ConnectHandle*上再次调用**SQLDriverConnect**函数。<br /><br /> 或者 **，SQLDriverConnect**函数被调用，在完成执行之前，SQLCancelHandle 是从多线程应用程序中的不同线程调用的**ConnectHandle。** *ConnectionHandle*|  
|HY010|函数序列错误|（DM） 另一个异步执行函数（不是**SQLDriverConnect）** 被调用为*ConnectHandle，* 并且在调用**SQLDriverConnect**函数时仍在执行。|  
|HY013|内存管理错误|无法处理**SQLDriverConnect**函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*StringLength1*指定的值小于 0，不等于SQL_NTS。<br /><br /> （DM） 为参数*BufferLength*指定的值小于 0。|  
|HY092|无效属性/选项标识符|（DM）*驱动程序完成*参数*SQL_DRIVER_PROMPT，WindowHandle*参数为空指针。|  
|HY110|驱动程序完成无效|（DM） 为参数 *"驱动程序完成"* 指定的值不等于SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED或SQL_DRIVER_NOPROMPT。<br /><br /> （DM） 连接池已启用，为参数*Driver 完成*指定的值不等于SQL_DRIVER_NOPROMPT。|  
|HYC00|未实现可选功能|驱动程序不支持应用程序请求的 ODBC 行为版本。|  
|HYT00|超时时间已到|与数据源的连接完成之前，登录超时期限已过期。 超时期间通过**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 对应于指定数据源名称的驱动程序不支持该函数。|  
|IM002|找不到数据源，未指定默认驱动程序|（DM） 在系统信息中找不到连接字符串 *（InConnectionString）* 中指定的数据源名称，并且没有默认驱动程序规范。<br /><br /> （DM） ODBC 数据源和默认驱动程序信息在系统信息中找不到。|  
|IM003|无法加载指定的驱动程序|（DM） 由于其他原因找不到或无法加载**DRIVER**关键字中数据源规范中列出的驱动程序。|  
|IM004|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_ENV 失败|（DM） 在**SQLDriverConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，该函数具有*fHandleType* SQL_HANDLE_ENV，驱动程序返回了错误。|  
|IM005|驱动程序的**SQLAllocHandle**上SQL_HANDLE_DBC失败。|（DM） 在**SQLDriverConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，该函数具有*fHandleType* SQL_HANDLE_DBC，驱动程序返回了错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|（DM） 在**SQLDriverConnect**期间，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数，驱动程序返回错误。|  
|IM007|未指定数据源或驱动程序;禁止对话|连接字符串中未指定数据源名称或驱动程序，并且*驱动程序完成*SQL_DRIVER_NOPROMPT。|  
|IM008|对话失败|驱动程序尝试显示其登录对话框，但失败。<br /><br /> *WindowHandle*是一个空指针，*并且驱动程序完成*不是SQL_DRIVER_NO_PROMPT。|  
|IM009|无法加载转换 DLL|驱动程序无法加载为数据源或连接指定的转换 DLL。|  
|IM010|数据源名称太长|（DM） DSN 关键字的属性值大于SQL_MAX_DSN_LENGTH个字符。|  
|IM011|驱动程序名称太长|（DM） **DRIVER**关键字的属性值超过 255 个字符。|  
|IM012|驱动程序关键字语法错误|（DM） **DRIVER**关键字的关键字值对包含语法错误。<br /><br /> （DM） * \*InConnectString*中的字符串包含**一个 FILESN**关键字，但 .dsn 文件不包含**DRIVER**关键字或**DSN**关键字。|  
|IM014|指定的 DSN 包含驱动程序和应用程序之间的体系结构不匹配|（DM） 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM015|驱动程序的 SQLDriver 连接SQL_HANDLE_DBC_INFO_HANDLE失败|如果驱动程序返回SQL_ERROR，驱动程序管理器将返回SQL_ERROR到应用程序，连接将失败。<br /><br /> 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，无法设置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 连接字符串具有以下语法：  
  
 *连接字符串*：：**空字符串*{;&#124;*属性*{;] &#124;*属性*;*连接字符串*  
  
 *空字符串*：：**属性*：：：**属性关键字*=*属性值*&#124; DRIVER_*属性值*{}}  
  
 *属性关键字*：：* DSN &#124; UID &#124; PWD &#124;*驱动程序定义的属性关键字*  
  
 *属性值*：：**字符字符串*  
  
 *驱动程序定义的属性关键字*：：**标识符*  
  
 *其中字符字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*属性关键字*不区分大小写;*属性值*可能区分大小写;**DSN**关键字的值不只包含空白。  
  
 由于连接字符串和初始化文件语法，包含字符的关键字和属性值 ***（）、？？{}应避免\*** 用大括号括起来的 [！] 。 **DSN**关键字的值不能仅包含空白，并且不应包含前导空格。 由于系统信息的语法，关键字和数据源名称不能包含反斜杠 （\\） 字符。  
  
 应用程序不必在**DRIVER**关键字之后在属性值周围添加大括号，除非该属性包含分号（;)，在这种情况下需要大括号。 如果驱动程序接收的属性值包括大括号，则驱动程序不应删除它们，但它们应是返回的连接字符串的一部分。  
  
 包含任何字符的{}**{}DSN 或连接字符串值，包含括号 （;？\**！]** 完好无损地传递给驱动程序。 但是，在关键字中使用这些字符时，驱动程序管理器在使用文件 DSN 时返回一个错误，但将连接字符串传递给驱动程序以进行常规连接字符串。 避免在关键字值中使用嵌入大括号。  
  
 连接字符串可能包括任意数量的驱动程序定义的关键字。 由于**DRIVER**关键字不使用系统信息中的信息，因此驱动程序必须定义足够的关键字，以便驱动程序只能使用连接字符串中的信息连接到数据源。 （有关详细信息，请参阅本节后面的"驾驶员指南"。驱动程序定义连接到数据源所需的关键字。  
  
 下表描述了 DSN、FILEDSN、DRIVER、UID、PWD**UID**和**SAVEFILE**关键字的属性值。 **DSN** **FILEDSN** **DRIVER** **PWD**  
  
|关键字|属性值描述|  
|-------------|---------------------------------|  
|**Dsn**|**SQLDataSources**或**SQLDriverConnect**的数据源对话框返回的数据源的名称。|  
|**备案**|.dsn 文件的名称，从中将为数据源生成连接字符串。 这些数据源称为文件数据源。|  
|**司机**|**SQLDriver**函数返回的驱动程序的说明。 例如，Rdb 或 SQL 服务器。|  
|**UID**|用户 ID。|  
|**PWD**|与用户 ID 对应的密码，或空字符串（如果用户 ID 没有密码）（PWD=;)。|  
|**保存文件**|应保存 .dsn 文件的文件名，其中应保存用于建立当前成功连接时使用的关键字的属性值。|  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果在连接字符串中重复任何关键字，驱动程序将使用与关键字的第一次出现关联的值。 如果**DSN**和**DRIVER**关键字包含在相同的连接字符串中，则驱动程序管理器和驱动程序首先使用哪个关键字出现。  
  
 **FILEDSN**和**DSN**关键字是互斥的：使用哪个关键字先出现，而出现第二个关键字的关键字将被忽略。 另一方面 **，FILEDSN**和**DRIVER**关键字不是相互排斥的。 如果任何关键字出现在与**FILESN**的连接字符串中，则使用连接字符串中关键字的属性值，而不是 .dsn 文件中同一关键字的属性值。  
  
 如果使用**FILESN**关键字，则 .dsn 文件中指定的关键字将用于创建连接字符串。 （有关详细信息，请参阅本节后面的"文件数据源"。**UID**关键字是可选的;但是，UID 关键字是可选的。可以仅使用**DRIVER**关键字创建 .dsn 文件。 **PWD**关键字不存储在 .dsn 文件中。 保存和加载 .dsn 文件的默认目录是 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Windows_Windows_当前版本和"ODBC_数据源"中**由 CommonFileDir**指定的路径的组合。 （如果通用 FileDir 是"C：*程序文件\公共文件"，则默认目录为"C：程序文件\常见文件\ODBC_数据源"。  
  
> [!NOTE]  
>  通过调用安装程序 DLL 中的[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)和[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)函数，可以直接操作 .dsn 文件。  
  
 如果使用**SAVEFILE**关键字，则用于进行当前成功连接的关键字的属性值将保存为 .dsn 文件，该文件的名称为**SAVEFILE**关键字的属性值。 **SAVEFILE**关键字必须与**DRIVER**关键字 **、FILESN**关键字或两者结合使用，否则函数返回SQL_SUCCESS_WITH_INFO SQLSTATE 01S09（无效关键字）。 **SAVEFILE**关键字必须出现在连接字符串中的**DRIVER**关键字之前，否则结果将未定义。  
  
## <a name="driver-manager-guidelines"></a>驾驶员经理指南  
 驱动程序管理器构造一个连接字符串，以传递给驱动程序的**SQLDriverConnect**函数的*InConnectionString*参数中的驱动程序。 驱动程序管理器不会修改应用程序传递给它的*InConnectionString*参数。  
  
 驱动程序管理器的操作基于*驱动程序完成*参数的值：  
  
-   SQL_DRIVER_PROMPT：如果连接字符串不包含**DRIVER、DSN**或**DRIVER****"已提交"** 关键字，则驱动程序管理器将显示"数据源"对话框。 它构造一个连接字符串，从对话框返回的数据源名称以及应用程序传递给它的任何其他关键字。 如果对话框返回的数据源名称为空，则驱动程序管理器指定关键字值对 DSN_Default。 （此对话框不会显示名称为"默认"的数据源。  
  
-   SQL_DRIVER_COMPLETE或SQL_DRIVER_COMPLETE_REQUIRED：如果应用程序指定的连接字符串包含**DSN**关键字，则驱动程序管理器将复制应用程序指定的连接字符串。 否则，它采取的操作与*SQL_DRIVER_PROMPT驱动程序完成*时相同的操作。  
  
-   SQL_DRIVER_NOPROMPT：驱动程序管理器复制应用程序指定的连接字符串。  
  
 如果应用程序指定的连接字符串包含**DRIVER**关键字，则驱动程序管理器将复制应用程序指定的连接字符串。  
  
 使用它构造的连接字符串，驱动程序管理器确定要使用的驱动程序，连接到该驱动程序，并将它构造的连接字符串传递给驱动程序;有关驱动程序管理器和驱动程序交互的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)中的"注释"部分。 如果连接字符串不包含**DRIVER**关键字，驱动程序管理器将确定要使用的驱动程序，如下所示：  
  
1.  如果连接字符串包含**DSN**关键字，驱动程序管理器将从系统信息中检索与数据源关联的驱动程序。  
  
2.  如果连接字符串不包含**DSN**关键字或找不到数据源，驱动程序管理器将从系统信息中检索与默认数据源关联的驱动程序。 （有关详细信息，请参阅[默认子键](../../../odbc/reference/install/default-subkey.md)。驱动程序管理器将连接字符串中的**DSN**关键字的值更改为"DEFAULT"。  
  
3.  如果连接字符串中的**DSN**关键字设置为"DEFAULT"，驱动程序管理器将从系统信息中检索与默认数据源关联的驱动程序。  
  
4.  如果未找到数据源，并且找不到默认数据源，则驱动程序管理器将返回 SQL_ERROR SQLSTATE IM002（找不到数据源，未指定默认驱动程序）。  
  
## <a name="file-data-sources"></a>文件数据源  
 如果应用程序在调用**SQLDriverConnect**中指定的连接字符串包含**FILESN**关键字，并且此关键字未被**DSN**或**DRIVER**关键字取代，则驱动程序管理器将使用 .dsn 文件和*InConnectString*参数中的信息创建连接字符串。 驱动程序管理器继续如下：  
  
1.  检查 .dsn 文件的文件名是否有效。 如果没有，它将返回SQL_ERROR SQLSTATE IM014（文件 DSN 的无效名称）。 如果文件名是空字符串 （""）且未指定SQL_DRIVER_NOPROMPT，则显示 **"文件打开"** 对话框。 如果文件名包含有效的路径但没有文件名或无效的文件名，并且未指定SQL_DRIVER_NOPROMPT，则"**文件打开**"对话框将显示当前目录设置为文件名中指定的目录。 如果文件名是空字符串 （""）或文件名包含有效的路径，但没有文件名或无效的文件名，并且SQL_DRIVER_NOPROMPT指定，则使用 SQLSTATE IM014（文件 DSN 的无效名称）返回SQL_ERROR。  
  
2.  读取 .dsn 文件的 [ODBC] 部分中的所有关键字。 如果**DRIVER**关键字不存在，则返回 SQL_ERROR SQLSTATE IM012（驱动程序关键字语法错误），除非 .dsn 文件不可共享，因此仅包含**DSN**关键字。  
  
     如果文件数据源不可共享，驱动程序管理器将读取**DSN**关键字的值，并根据需要连接到不可共享文件数据源指向的用户或系统数据源。 步骤 3 到 5 未执行。  
  
3.  为驱动程序构造连接字符串。 驱动程序连接字符串是 .dsn 文件中指定的关键字和原始应用程序连接字符串中指定的关键字的合并。 关键字重叠的驱动程序连接字符串的构造规则如下所示：  
  
    -   如果应用程序连接字符串中存在**DRIVER**关键字，并且**DRIVER**关键字指定的驱动程序在 .dsn 文件和应用程序连接字符串中不同，则忽略 .dsn 文件中的驱动程序信息，并使用应用程序连接字符串中的驱动程序信息。 如果**DRIVER**关键字指定的驱动程序在 .dsn 文件和应用程序的连接字符串中相同，则当所有关键字重叠时，应用程序连接字符串中指定的驱动程序优先于 .dsn 文件中指定的驱动程序。  
  
    -   在新的连接字符串中，将消除 **"已提交"** 关键字。  
  
4.  通过在注册表项HKEY_LOCAL_MACHINE_软件_ODBC_ODBCINST 中查找驱动程序。INI\\<驱动程序\>名称 \\<驱动程序，其中驱动程序名称>由**DRIVER**关键字指定。  
  
5.  传递驱动程序的新连接字符串。  
  
 有关 .dsn 文件的示例，请参阅[使用文件数据源进行连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)。  
  
## <a name="savefile-keyword"></a>保存文件关键字  
 如果应用程序指定的连接字符串包含**SAVEFILE**关键字，则驱动程序管理器将连接字符串保存在 .dsn 文件中。 驱动程序管理器继续如下：  
  
1.  检查作为**SAVEFILE**关键字的属性值包含的 .dsn 文件的文件名是否有效。 如果没有，它将返回SQL_ERROR SQLSTATE IM014（文件 DSN 的无效名称）。 文件名的有效性由标准系统命名规则确定。 如果文件名是空字符串 （""）并且*驱动程序完成*参数不SQL_DRIVER_NOPROMPT，则文件名有效。 如果文件名已存在，则如果*SQL_DRIVER_NOPROMPT驱动程序完成*，则文件将被覆盖。 如果 *"驱动程序完成"* 是SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE或SQL_DRIVER_COMPLETE_REQUIRED，则一个对话框会提示用户指定是否应覆盖该文件。 如果输入"否"，则将显示 **"文件保存**"对话框。  
  
2.  如果驱动程序返回SQL_SUCCESS并且文件名不是空字符串，则驱动程序管理器将*OutConnectionString*参数中返回的连接信息写入指定文件，其格式位于本节前面的"连接字符串"部分中。  
  
3.  如果驱动程序返回SQL_SUCCESS并且文件名是空字符串 （"），则驱动程序管理器调用指定*hwnd* **的文件保存**公共对话框，并将*在 OutConnectString 中*返回的连接信息写入"文件保存公共对话框"中指定的文件，该格式在本节中稍早的"连接字符串"部分中指定。  
  
4.  如果驱动程序返回SQL_SUCCESS，它将返回包含与应用程序的连接字符串*的 OutConnectString*参数。  
  
5.  如果驱动程序返回SQL_SUCCESS_WITH_INFO或SQL_ERROR，则驱动程序管理器将 SQLSTATE 返回到应用程序。  
  
## <a name="driver-guidelines"></a>驾驶员指南  
 驱动程序检查驱动程序管理器传递给它的连接字符串是否包含**DSN**或**DRIVER**关键字。 如果连接字符串包含**DRIVER**关键字，则驱动程序无法从系统信息中检索有关数据源的信息。 如果连接字符串包含**DSN**关键字或不包含**DSN**或**DRIVER**关键字，驱动程序可以从系统信息中检索有关数据源的信息，如下所示：  
  
1.  如果连接字符串包含**DSN**关键字，驱动程序将检索指定数据源的信息。  
  
2.  如果连接字符串不包含**DSN**关键字，则找不到指定的数据源，或者**DSN**关键字设置为"DEFAULT"，驱动程序将检索默认数据源的信息。  
  
 驱动程序使用从系统信息检索到的任何信息来增强在连接字符串中传递给它的信息。 如果系统信息中的信息复制连接字符串中的信息，则驱动程序将使用连接字符串中的信息。  
  
 根据*Driver 完成*的值，驱动程序会提示用户获取连接信息（如用户 ID 和密码）并连接到数据源：  
  
-   SQL_DRIVER_PROMPT：驱动程序显示一个对话框，使用连接字符串中的值和系统信息（如果有）作为初始值。 当用户退出对话框时，驱动程序将连接到数据源。 它还从\**InConnectionString*中的**DSN**或**DRIVER**关键字的值以及从对话框返回的信息构造连接字符串。 它将此连接字符串放在 +*外连接字符串*缓冲区中。  
  
-   SQL_DRIVER_COMPLETE或SQL_DRIVER_COMPLETE_REQUIRED：如果连接字符串包含足够的信息，并且该信息是正确的，则驱动程序连接到数据源，并将\**InConnectionString*复制到\* *OutConnectionString*。 如果缺少或不正确任何信息，驱动程序将执行与*SQL_DRIVER_PROMPT Driver 完成*时相同的操作，但如果未SQL_DRIVER_COMPLETE_REQUIRED*驱动程序完成*，则驱动程序将禁用连接到数据源所需的任何信息的控件。  
  
-   SQL_DRIVER_NOPROMPT：如果连接字符串包含足够的信息，驱动程序将连接到数据源并将\**InConnectString*复制到\* *OutConnectString*。 否则，驱动程序将返回**SQLDriverConnect**SQL_ERROR。  
  
 成功连接到数据源时，驱动程序还将\**StringLength2Ptr*设置到输出连接字符串的长度，该字符串可在 +*OutConnectString*中返回。  
  
 如果用户取消驱动程序管理器或驱动程序提供的对话框 **，SQLDriverConnect**将返回SQL_NO_DATA。  
  
 有关驱动程序管理器和驱动程序在连接过程中如何交互的信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果驱动程序支持**SQLDriverConnect，** 则驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**关键字，第二个字符设置为"Y"。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>启用连接池时连接  
 连接池允许应用程序重用已创建的连接。 调用**SQLDriverConnect**时，驱动程序管理器尝试使用已指定用于连接池的环境中的连接池中的连接。 有关连接池的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 应用程序可以在启用池的连接上调用 SQLDisconnect 之前设置SQL_ATTR_RESET_CONNECTION。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 当应用程序调用**SQLDriverConnect**连接到池连接时，将应用以下限制：  
  
-   在连接字符串中指定**SAVEFILE**关键字时，不执行连接池处理。  
  
-   如果启用了连接池，则只能使用*驱动程序完成*参数SQL_DRIVER_NOPROMPT才能调用**SQLDriverConnect;** 如果**SQLDriverConnect**与任何其他*驱动程序完成*调用，则 SQLSTATE HY110（无效驱动程序完成）将返回。  
  
## <a name="connection-attributes"></a>连接属性  
 使用**SQLSetConnectAttr**设置SQL_ATTR_LOGIN_TIMEOUT连接属性定义等待登录请求在返回应用程序之前由驱动程序成功完成连接的秒数。 如果提示用户完成连接字符串，则当驱动程序启动连接过程时，每个登录请求的等待期将开始。  
  
 默认情况下，驱动程序以SQL_MODE_READ_WRITE访问模式打开连接。 要将访问模式设置为SQL_MODE_READ_ONLY，应用程序必须在调用**SQLDriverConnect**之前使用SQL_ATTR_ACCESS_MODE属性调用**SQLSetConnectAttr。**  
  
 如果在数据源的系统信息中指定了默认翻译库，驱动程序将加载它。 可以使用SQL_ATTR_TRANSLATE_LIB属性调用**SQLSetConnectAttr**来加载不同的翻译库。 可以通过使用SQL_ATTR_TRANSLATE_OPTION选项调用**SQLSetConnectAttr**来指定转换选项。  
  
 有关详细信息，请参阅使用[SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 另请参阅[ODBC 示例计划](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举连接到数据源所需的值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|返回驱动程序描述和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放手柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
