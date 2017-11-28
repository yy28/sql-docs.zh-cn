---
title: "SQLDriverConnect 函数 |Microsoft 文档"
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
apiname: SQLDriverConnect
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDriverConnect
helpviewer_keywords: SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
caps.latest.revision: "50"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6c5eaaa0580d718ecfa3b57c2c4b0aa7da5cda41
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLDriverConnect**是一种替代方法**SQLConnect**。 它支持需要更多的连接信息中的三个自变量比数据源的**SQLConnect**，对话框以提示用户输入所有连接信息和系统中未定义的数据源信息。  
  
 **SQLDriverConnect**提供以下连接属性：  
  
-   建立连接使用数据源的连接字符串包含数据源名称、 一个或多个用户 Id、 一个或多个密码和其他所需的信息。  
  
-   建立连接使用部分连接字符串或任何其他信息;在这种情况下，驱动程序管理器和驱动程序每个可以提示用户输入连接信息。  
  
-   建立与未定义的系统信息中的数据源的连接。 如果应用程序提供部分连接字符串，该驱动程序会提示用户输入连接信息。  
  
-   建立与使用从.dsn 文件中的信息构造的连接字符串的数据源的连接。  
  
 建立连接后， **SQLDriverConnect**返回已完成的连接字符串。 应用程序可以将此字符串用于后续连接请求。 有关详细信息，请参阅[使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *WindowHandle*  
 [输入]窗口句柄。 应用程序有可能的话，可以将父窗口的句柄的传递或 null 指针，如果任一的窗口句柄不适用或**SQLDriverConnect**将不显示任何对话框。  
  
 *InConnectionString*  
 [输入]完整连接字符串 （请参阅"注释"中的语法），部分连接字符串或空字符串。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*，以如果字符串为 Unicode 或字节，如果字符串为 ANSI 或 DBCS 字符为单位。  
  
 *OutConnectionString*  
 [输出]指向已完成的连接字符串的缓冲区的指针。 在成功连接到目标数据源时，此缓冲区包含已完成的连接字符串。 应用程序应为此缓冲区分配至少 1024 个字符。  
  
 如果*OutConnectionString*为 NULL， *StringLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回在缓冲区中指向*OutConnectionString*。  
  
 *BufferLength*  
 [输入]长度 **OutConnectionString*缓冲区，以字符为单位。  
  
 *StringLength2Ptr*  
 [输出]指向要返回的字符 （不包括 null 终止字符） 总数在其中缓冲区的指针可用于返回在\* *OutConnectionString*。 可用于返回的字符数是否大于或等于*BufferLength*，则完成中的连接字符串\* *OutConnectionString*截断为*BufferLength*减 null 终止字符的长度。  
  
 *DriverCompletion*  
 [输入]该标志指示是否驱动程序管理器或驱动程序必须提示输入连接的详细信息：  
  
 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 或 SQL_DRIVER_NOPROMPT。  
  
 （有关更多信息，请参阅"注释"。）  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE，或 SQL_STILL_EXECUTING 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDriverConnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可能会通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*fHandleType*的 SQL_HANDLE_DBC 和*hHandle*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDriverConnect**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*不是否足够大以返回整个连接字符串，因此连接字符串已被截断。 在中返回未截断的连接字符串的长度 **StringLength2Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S00|无效的连接字符串属性|连接字符串中指定了无效的属性关键字 (*InConnectionString*)，但该驱动程序时能够是否仍要连接到数据源。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|该驱动程序不支持指定的值的指向*ValuePtr*中的参数**SQLSetConnectAttr**和替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S08|保存文件 DSN 时出错|中的字符串 *\*InConnectionString*包含**FILEDSN**关键字，但.dsn 文件未保存。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S09|无效的关键字|(DM) 中的字符串 *\*InConnectionString*包含**SAVEFILE**关键字而不是**驱动程序**或**FILEDSN**关键字。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|连接名称已在使用|(DM) 指定*ConnectionHandle*已用于建立与数据源的连接，并且连接已仍处于打开状态。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已尝试连接到的数据源之间的通信链接失败之前**SQLDriverConnect**函数完成处理。|  
|28000|无效的授权说明|用户标识符或授权字符串中，或是两者，作为连接字符串中指定 (*InConnectionString*)，违反数据源定义的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*szMessageText*缓冲区描述错误以及其可能的原因。|  
|HY000|常规错误： 无效的文件 dsn|(DM) 中的字符串 **InConnectionString*包含 FILEDSN 关键字，但找不到.dsn 文件的名称。|  
|HY000|常规错误： 无法创建文件缓冲区|(DM) 中的字符串 **InConnectionString*包含 FILEDSN 关键字，但不可读.dsn 文件。|  
|HY001|内存分配错误|驱动程序管理器无法分配内存支持执行或完成所需**SQLDriverConnect**函数。<br /><br /> 该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*ConnectionHandle*。 已调用函数，和它之前完成执行， [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，，然后**SQLDriverConnect**在再次调用函数*ConnectionHandle*。<br /><br /> 或者， **SQLDriverConnect**调用函数，并且它之前完成执行， **SQLCancelHandle**上调用了*ConnectionHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 另一个以异步方式执行的函数 (不**SQLDriverConnect**) 曾为*ConnectionHandle*和仍在执行时**SQLDriverConnect**调用函数。|  
|HY013|内存管理错误|**SQLDriverConnect**无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*StringLength1*小于 0 并且不等于 sql_nts 以。<br /><br /> (DM) 参数指定的值*BufferLength*小于 0。|  
|HY092|属性/选项标识符无效|(DM) *DriverCompletion*自变量为 SQL_DRIVER_PROMPT，和*WindowHandle*自变量是空指针。|  
|HY110|无效的驱动程序完成|(DM) 值的参数的指定*DriverCompletion*未等于 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 或 SQL_DRIVER_NOPROMPT。<br /><br /> (DM) 启用连接池，并指定自变量的值*DriverCompletion*未等于 SQL_DRIVER_NOPROMPT。|  
|HYC00|未实现的可选功能|该驱动程序不支持 ODBC 应用程序请求的行为的版本。|  
|HYT00|超时时间已到|登录超时期限过期之前完成数据源的连接。 通过设置的超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应于指定的数据源名称的驱动程序不支持该函数。|  
|IM002|找不到的数据源和未指定的默认驱动程序|(DM) 的数据源连接字符串中指定的名称 (*InConnectionString*) 已在系统信息中，找不到，并且存在任何默认驱动程序规范。<br /><br /> (DM) 的系统信息中找不到 ODBC 数据源和默认驱动程序信息。|  
|IM003|无法加载指定的驱动程序|(DM) 驱动程序中的系统信息的数据源规范中列出，或者通过指定**驱动程序**关键字找不到或无法加载其他原因。|  
|IM004|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_ENV 失败|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*fHandleType* SQL_HANDLE_ENV 和驱动程序的返回错误。|  
|IM005|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_DBC 失败。|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*fHandleType* SQL_HANDLE_DBC 和驱动程序的返回错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数和驱动程序返回了一个错误。|  
|IM007|没有数据源或驱动程序指定任何引用;禁止的对话框|连接字符串中指定了任何数据源名称或驱动程序和*DriverCompletion*已 SQL_DRIVER_NOPROMPT。|  
|IM008|失败的对话框|该驱动程序尝试显示其登录对话框中，但失败。<br /><br /> *WindowHandle*是空指针，和*DriverCompletion*未 SQL_DRIVER_NO_PROMPT。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为数据源或目标的连接指定的 DLL。|  
|IM010|数据源名称太长|(DM) DSN 关键字的特性值长于 SQL_MAX_DSN_LENGTH 字符。|  
|IM011|驱动程序名称太长|该属性值 (DM)**驱动程序**关键字长于 255 个字符。|  
|IM012|驱动程序关键字语法错误|(DM) 的关键字值的配对**驱动程序**关键字包含语法错误。<br /><br /> (DM) 中的字符串 *\*InConnectionString*包含**FILEDSN**关键字，但.dsn 文件不包含**驱动程序**关键字或**DSN**关键字。|  
|IM014|指定的 DSN 包含的驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用连接到 64 位驱动程序; DSN反之亦然。|  
|IM015|驱动程序的 SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE 上失败|如果驱动程序返回 SQL_ERROR，驱动程序管理器将返回 SQL_ERROR 到应用程序，则连接将失败。<br /><br /> 有关 SQL_HANDLE_DBC_INFO_TOKEN 的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当该驱动程序不支持异步通知时，不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 连接字符串具有以下语法：  
  
 *连接字符串*:: =*空字符串*[;] &#124;*属性*[;] &#124;*属性*;*连接字符串*  
  
 *空字符串*:: =*属性*:: =*属性关键字*=*属性值*&#124;驱动程序 = [{}]*属性值*[}]  
  
 *零个以上*:: = DSN &#124;UID &#124;PWD &#124;*驱动程序的定义的零个以上*  
  
 *属性值*:: =*字符串*  
  
 *驱动程序的定义的零个以上*:: =*标识符*  
  
 其中*字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*属性关键字*不区分大小写;*属性值*可能区分大小写; 和的值**DSN**关键字不由单独的空格组成。  
  
 由于连接字符串和初始化文件语法、 关键字和属性值，包含字符**[] {} （)，;？\*= ！ @**不包含大括号，则应避免。 值**DSN**关键字不能只包含空格，并且不包含前导空格。 由于系统信息的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 应用程序不需要后的属性值两边添加大括号**驱动程序**关键字除非该属性包含分号 （;），在这种情况下大括号都需要。 如果驱动程序收到的属性值包含大括号，驱动程序不应删除它们，但它们应该返回的连接字符串的一部分。  
  
 DSN 或连接字符串值括在大括号 （{}） 包含的任何字符**[] {} （)，;？\*= ！ @**到驱动程序传递不变。 但是，在使用这些字符 in 关键字时，驱动程序管理器使用文件 Dsn 时返回错误，但将连接字符串传递给正则连接字符串的驱动程序。 避免使用嵌入的大括号中的关键字值。  
  
 连接字符串可能包含任意数量的驱动程序定义的关键字。 因为**驱动程序**关键字不使用中的系统信息的信息，该驱动程序必须定义足够的关键字，以使驱动程序可以连接到数据源使用的连接字符串中仅的信息。 （有关详细信息，请参阅"驱动程序指南"本部分中更高版本）。该驱动程序定义的关键字所需连接到数据源。  
  
 下表描述的属性值**DSN**， **FILEDSN**，**驱动程序**， **UID**， **PWD**，和**SAVEFILE**关键字。  
  
|关键字|属性值说明|  
|-------------|---------------------------------|  
|**DSN**|返回的数据源名称**SQLDataSources**或数据源对话框中的**SQLDriverConnect**。|  
|**FILEDSN**|数据源的.dsn 文件将从中生成连接字符串的名称。 这些数据源称为文件数据源。|  
|**驱动程序**|返回由驱动程序的说明**SQLDrivers**函数。 例如，Rdb 或 SQL Server。|  
|**UID**|用户 id。|  
|**PWD**|如果没有针对的用户 ID 的密码与用户 ID 或空字符串相对应的密码 (PWD =;）。|  
|**SAVEFILE**|应在其中保存中建立的存在、 成功的连接使用关键字的属性值的.dsn 文件的文件名。|  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果任何关键字都重复连接字符串中显示，驱动程序将使用与关键字的第一个匹配项关联的值。 如果**DSN**和**驱动程序**相同的连接字符串中包含关键字，驱动程序管理器和驱动程序使用任何关键字将出现第一个。  
  
 **FILEDSN**和**DSN**关键字互斥： 使用任何关键字将出现第一个，则忽略显示第二个。 **FILEDSN**和**驱动程序**关键字，另一方面，并不互相排斥。 如果任何关键字出现在连接字符串与**FILEDSN**，则连接字符串中的关键字的属性值使用而不是同一关键字.dsn 文件中的属性值。  
  
 如果**FILEDSN**使用关键字、.dsn 文件中指定的关键字用于创建连接字符串。 （有关详细信息，请参阅"文件数据源，"本部分中更高版本）。**UID**关键字是可选的;.dsn 文件可能仅使用创建**驱动程序**关键字。 **PWD**关键字不存储在.dsn 文件。 保存和加载.dsn 文件的默认目录将是指定的路径的组合**CommonFileDir** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion 和"ODBC\DataSources"中。 （如果 CommonFileDir 是"C:\Program Files\Common 文件"，默认目录将是"C:\Program Files\Common Files\ODBC\Data 源"。）  
  
> [!NOTE]  
>  可以直接通过调用操作.dsn 文件[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)和[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)安装 DLL 中的函数。  
  
 如果**SAVEFILE**使用关键字，关键字中建立的存在、 成功的连接使用的属性值将保存为.dsn 文件同名的属性值的**SAVEFILE**关键字。 **SAVEFILE**关键字必须与结合使用**驱动程序**关键字， **FILEDSN**关键字，或两者，或该函数将返回与 SQL_SUCCESS_WITH_INFOSQLSTATE 01S09 （无效的关键字）。 **SAVEFILE**关键字必须出现在之前**驱动程序**关键字在连接字符串或结果将是未定义。  
  
## <a name="driver-manager-guidelines"></a>驱动程序管理器准则  
 驱动程序管理器构造一个连接字符串以传递给在驱动程序*InConnectionString*的驱动程序的自变量**SQLDriverConnect**函数。 驱动程序管理器不会修改*InConnectionString*自变量传递给它的应用程序。  
  
 值基于操作的驱动程序管理器*DriverCompletion*自变量：  
  
-   SQL_DRIVER_PROMPT： 如果连接字符串不包含任一**驱动程序**， **DSN**，或**FILEDSN**关键字，驱动程序管理器将显示数据源对话框。 构造从对话框中返回的数据源名称和传递给它的应用程序的其他任何关键字的连接字符串。 如果返回对话框中的数据源名称为空，驱动程序管理器指定的关键字 / 值对 DSN = 默认值。 （此对话框中将不显示具有名称为"Default"的数据源。）  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED： 如果应用程序所指定的连接字符串包括**DSN**关键字，驱动程序管理器正在复制应用程序所指定的连接字符串。 否则，它采用相同的操作方式与其时*DriverCompletion*是 SQL_DRIVER_PROMPT。  
  
-   SQL_DRIVER_NOPROMPT： 驱动程序管理器将复制的应用程序所指定的连接字符串。  
  
 如果应用程序所指定的连接字符串包含**驱动程序**关键字，驱动程序管理器正在复制应用程序所指定的连接字符串。  
  
 使用已构造的连接字符串，驱动程序管理器确定使用哪个驱动程序，连接到该驱动程序，并将已构造的连接字符串传递给该驱动程序;有关驱动程序管理器和驱动程序的交互的详细信息，请参阅中的"注释"部分[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。 如果连接字符串不包含**驱动程序**关键字，驱动程序管理器确定，如下所示使用哪个驱动程序：  
  
1.  如果连接字符串包含**DSN**关键字，驱动程序管理器检索与数据源中的系统信息关联的驱动程序。  
  
2.  如果连接字符串不包含**DSN**关键字或数据源找不到，驱动程序管理器将检索与中的系统信息的默认数据源关联的驱动程序。 (有关详细信息，请参阅[默认子项](../../../odbc/reference/install/default-subkey.md)。)驱动程序管理器的值更改**DSN** "DEFAULT"的连接字符串中的关键字。  
  
3.  如果**DSN**中的连接字符串关键字设置为"默认值"时，驱动程序管理器将检索与中的系统信息的默认数据源关联的驱动程序。  
  
4.  如果找不到数据源，找不到默认数据源，驱动程序管理器将返回与 SQLSTATE IM002 SQL_ERROR （找不到的数据源和未指定的默认驱动程序）。  
  
## <a name="file-data-sources"></a>文件数据源  
 如果应用程序的调用中指定的连接字符串**SQLDriverConnect**包含**FILEDSN**关键字，然后此关键字不会取代通过以下任一方法**DSN**或**驱动程序**关键字，则驱动程序管理器创建使用.dsn 文件中的信息的连接字符串和*InConnectionString*自变量。 驱动程序管理器将继续，如下所示：  
  
1.  检查.dsn 文件的文件名称是否有效。 如果不是，它返回与 SQLSTATE IM014 SQL_ERROR （无效名称的文件 DSN）。 如果文件名称为空字符串 ("") 和 SQL_DRIVER_NOPROMPT 不指定，则**文件打开**对话框随即显示。 如果文件名包含有效的路径，但任何文件名或无效的文件名称，且未指定 SQL_DRIVER_NOPROMPT，则**文件打开**对话框中将显示与当前目录设置为一个文件名称中指定。 如果文件名称为空字符串 ("") 或文件名称包含有效的路径，但任何文件名或无效的文件名称，并指定 SQL_DRIVER_NOPROMPT，然后随 SQLSTATE IM014 返回 SQL_ERROR （无效名称的文件 DSN）。  
  
2.  读取.dsn 文件的 [ODBC] 部分中的所有关键字。 如果**驱动程序**关键字不存在，它将返回与 SQLSTATE IM012 SQL_ERROR （驱动程序关键字语法错误），其中.dsn 文件是共享，因此只包含除**DSN**关键字。  
  
     如果共享文件数据源，驱动程序管理器中读取的值**DSN**关键字并连接到用户或系统数据源的非共享的文件数据源指向根据需要。 未执行步骤 3 至 5。  
  
3.  构造该驱动程序的连接字符串。 驱动程序连接字符串是.dsn 文件中指定的关键字和原始的应用程序连接字符串中指定的联合。 有关构造的驱动程序的连接字符串关键字的重叠处的规则如下所示：  
  
    -   如果**驱动程序**应用程序连接字符串和指定的驱动程序中存在关键字**驱动程序**关键字不中.dsn 文件和应用程序连接字符串，相同则忽略.dsn 文件中的驱动程序信息和使用应用程序连接字符串中的驱动程序信息。 如果通过指定的驱动程序**驱动程序**关键字是相同的.dsn 文件和应用程序的连接字符串，然后其中所有关键字都重叠，应用程序连接字符串中指定的那些具有优先于.dsn 文件中指定。  
  
    -   在新的连接字符串中， **FILEDSN**消除关键字。  
  
4.  通过查看注册表条目 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 中将加载驱动程序。INI\\< 驱动程序名称\>\Driver 其中\<驱动程序名称 > 指定**驱动程序**关键字。  
  
5.  将驱动程序传递新的连接字符串。  
  
 .Dsn 文件的示例，请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)。  
  
## <a name="savefile-keyword"></a>SAVEFILE 关键字  
 如果应用程序所指定的连接字符串包含**SAVEFILE**关键字，则驱动程序管理器将连接字符串保存在.dsn 文件。 驱动程序管理器将继续，如下所示：  
  
1.  检查.dsn 文件的文件名称是否包含作为其属性值的**SAVEFILE**关键字无效。 如果不是，它返回与 SQLSTATE IM014 SQL_ERROR （无效名称的文件 DSN）。 由标准系统命名规则确定的文件名称的有效性。 如果文件名称为空字符串 ("") 和*DriverCompletion*自变量不是 SQL_DRIVER_NOPROMPT，则该文件名称是否有效。 如果文件名称已存在，然后如果*DriverCompletion*是 SQL_DRIVER_NOPROMPT，则会覆盖文件。 如果*DriverCompletion*是 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE，还是 SQL_DRIVER_COMPLETE_REQUIRED，对话框会提示用户指定是否应覆盖该文件。 如果不输入，则**文件保存**对话框随即出现。  
  
2.  如果驱动程序返回 SQL_SUCCESS 和文件名称不是空字符串，则驱动程序管理器将在中返回的连接信息写入*OutConnectionString*参数中指定的格式与指定的文件此部分中前面的"连接字符串"部分。  
  
3.  如果驱动程序返回 SQL_SUCCESS 且文件名称为空字符串 ("")，则驱动程序管理器调用**文件保存**与常见对话框*hwnd*指定和写入的连接信息在中返回*OutConnectionString*文件保存通用对话框中指定使用此部分中前面的"连接字符串"部分中指定的格式的文件。  
  
4.  如果驱动程序将返回 SQL_SUCCESS，它将返回*OutConnectionString*包含应用程序的连接字符串自变量。  
  
5.  如果该驱动程序返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，驱动程序管理器对到应用程序返回的 SQLSTATE。  
  
## <a name="driver-guidelines"></a>驱动程序准则  
 该驱动程序检查传递给它的驱动程序管理器的连接字符串是否包含**DSN**或**驱动程序**关键字。 如果连接字符串包含**驱动程序**关键字，该驱动程序无法从系统信息中检索有关数据源的信息。 如果连接字符串包含**DSN**关键字或不包含**DSN**或**驱动程序**关键字，该驱动程序可以检索有关数据源的信息从，如下所示的系统信息：  
  
1.  如果连接字符串包含**DSN**关键字，该驱动程序检索指定的数据源的信息。  
  
2.  如果连接字符串不包含**DSN**关键字，未找到指定的数据源，或**DSN**关键字设置为"DEFAULT"，该驱动程序检索默认数据源的信息.  
  
 驱动程序使用它从来加强连接字符串中传递给它的信息的系统信息中检索任何信息。 如果系统信息中的信息复制连接字符串中的信息，该驱动程序连接字符串中使用的信息。  
  
 基于值*DriverCompletion*，驱动程序提示用户输入连接信息，例如用户 ID 和密码，并连接到数据源：  
  
-   SQL_DRIVER_PROMPT： 驱动程序显示一个对话框，并使用作为初始值中的连接字符串和系统信息的值 （如果有）。 当用户退出对话框时，该驱动程序连接到数据源。 它还构造连接字符串中的值**DSN**或**驱动程序**中的关键字\* *InConnectionString*以及从返回的信息对话框。 它会将放置在此连接字符串 **OutConnectionString*缓冲区。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED： 如果连接字符串包含足够的信息，并且该信息是否正确，该驱动程序连接到的数据源和副本\* *InConnectionString*到\* *OutConnectionString*。 如果任何信息缺失或不正确，该驱动程序采用相同的操作方式与其时*DriverCompletion*除外，如果是 SQL_DRIVER_PROMPT， *DriverCompletion*是 SQL_DRIVER_COMPLETE_必需的该驱动程序禁用不需要连接到数据源的任何信息的控件。  
  
-   SQL_DRIVER_NOPROMPT： 如果连接字符串包含足够的信息，该驱动程序连接到的数据源和副本\* *InConnectionString*到\* *OutConnectionString*. 否则，该驱动程序将返回有关 SQL_ERROR **SQLDriverConnect**。  
  
 在成功连接到数据源时，该驱动程序还将设置\* *StringLength2Ptr*可用于在中返回的输出连接字符串的长度 **OutConnectionString*。  
  
 如果用户取消对话框中提供的驱动程序管理器或驱动程序， **SQLDriverConnect**返回 SQL_NO_DATA。  
  
 有关驱动程序管理器和驱动程序在连接过程中的交互方式的信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果驱动程序支持**SQLDriverConnect**，驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**与第二个字符的关键字设置为"Y"。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>连接时启用连接池  
 连接池允许应用程序重复使用已创建的连接。 当**SQLDriverConnect**调用时，驱动程序管理器尝试建立连接使用的是已指派给连接池的环境中的连接池的一部分的连接。 有关连接池的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 应用程序可以在其中启用了连接池的连接上调用 SQLDisconnect 之前设置 SQL_ATTR_RESET_CONNECTION。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 以下限制适用时应用程序调用**SQLDriverConnect**连接到已入池连接：  
  
-   执行没有连接池处理时**SAVEFILE**关键字指定连接字符串中。  
  
-   如果启用了连接池， **SQLDriverConnect**可以仅使用调用*DriverCompletion* SQL_DRIVER_NOPROMPT 自变量; 如果**SQLDriverConnect**称为与任何其他*DriverCompletion*，SQLSTATE HY110 将返回 （无效的驱动程序完成）。  
  
## <a name="connection-attributes"></a>连接属性  
 SQL_ATTR_LOGIN_TIMEOUT 连接属性，使用设置**SQLSetConnectAttr**，定义的登录请求的成功连接完成由驱动程序返回到应用程序之前等待的秒数。 如果系统会提示用户完成连接字符串，每个登录名请求等待一段时间将开始时驱动程序启动连接过程。  
  
 默认情况下，该驱动程序打开 SQL_MODE_READ_WRITE access 模式中的连接。 若要设置的访问模式为 SQL_MODE_READ_ONLY，应用程序必须调用**SQLSetConnectAttr**使用之前调用 SQL_ATTR_ACCESS_MODE 特性**SQLDriverConnect**。  
  
 如果数据源的系统信息中指定默认转换库，则该驱动程序将加载它。 可以通过调用加载不同的翻译库**SQLSetConnectAttr**具有 SQL_ATTR_TRANSLATE_LIB 属性。 转换选项只能指定通过调用**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 选项。  
  
 有关详细信息，请参阅[使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
```  
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
  
 另请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举连接到数据源所需值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|从数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|返回驱动程序说明和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
