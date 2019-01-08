---
title: SQLDriverConnect 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d80de6087997b6af0202dafae7576ba442514abf
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212386"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLDriverConnect**是一种替代方法**SQLConnect**。 它支持需要比在三个参数的更多连接信息的数据源**SQLConnect**，对话框以提示用户输入的所有连接信息和不在系统中定义的数据源信息。  
  
 **SQLDriverConnect**提供了以下连接属性：  
  
-   建立连接使用数据源的连接字符串，其中包含数据源名称、 一个或多个用户 Id、 一个或多个密码和其他所需的信息。  
  
-   使用部分连接字符串或任何其他信息; 建立连接在这种情况下，驱动程序管理器和驱动程序每个可以提示用户输入连接信息。  
  
-   建立与系统信息中未定义的数据源的连接。 如果应用程序提供了一个部分连接字符串，该驱动程序可以提示用户输入连接信息。  
  
-   建立与使用从.dsn 文件中的信息构造的连接字符串的数据源的连接。  
  
 建立连接后， **SQLDriverConnect**返回已完成的连接字符串。 应用程序可以使用此字符串的后续连接请求。 有关详细信息，请参阅[使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
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
 [输入]窗口句柄。 应用程序可以通过父窗口的句柄，如果适用，或如果是 null 指针的窗口句柄不适用或**SQLDriverConnect**将不显示任何对话框。  
  
 *InConnectionString*  
 [输入]完整的连接字符串 （请参阅"注释"中的语法），部分连接字符串或为空字符串。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*，如果该字符串为 Unicode 或字节数，如果字符串为 ANSI 或 DBCS 字符中。  
  
 *OutConnectionString*  
 [输出]已完成的连接字符串的缓冲区的指针。 在成功连接到目标数据源，此缓冲区包含已完成的连接字符串。 应用程序应为此缓冲区分配至少 1,024 个字符。  
  
 如果*OutConnectionString*为 NULL， *StringLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于在缓冲区中返回指向*OutConnectionString*。  
  
 *BufferLength*  
 [输入]长度 **OutConnectionString*缓冲区，以字符为单位。  
  
 *StringLength2Ptr*  
 [输出]指向用于返回的字符 （不包括 null 终止字符） 总数的缓冲区可用于在中返回\* *OutConnectionString*。 可用于返回的字符数是否大于或等于*BufferLength*，则已完成中的连接字符串\* *OutConnectionString*截断为*BufferLength*减去 null 终止字符的长度。  
  
 *DriverCompletion*  
 [输入]该标志指示驱动程序管理器或驱动程序必须提示输入连接的详细信息：  
  
 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 时或 SQL_DRIVER_NOPROMPT。  
  
 （有关其他信息，请参阅"注释"。）  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDriverConnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*fHandleType*设为 SQL_HANDLE_DBC 和一个*hHandle*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDriverConnect** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutConnectionString*是否不足够大以返回整个连接字符串，以便连接字符串已被截断。 在返回未截断的连接字符串的长度 **StringLength2Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S00|连接字符串属性无效|在连接字符串中指定一个无效的属性的关键字 (*InConnectionString*)，但该驱动程序无法继续连接到数据源。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持指定的值由指向*ValuePtr*中的参数**SQLSetConnectAttr**和替换一个相近的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S08|保存文件 DSN 时出错|中的字符串 *\*InConnectionString*包含**FILEDSN**关键字，但.dsn 文件未保存。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S09|无效的关键字|(DM) 中的字符串 *\*InConnectionString*包含**SAVEFILE**关键字而非**驱动程序**或**FILEDSN**关键字。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|在使用的连接名称|(DM) 指定*ConnectionHandle*已用于建立与数据源的连接，并且连接已打开。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已尝试连接到的数据源之间的通信链接失败之前**SQLDriverConnect**函数已完成处理。|  
|28000|无效的授权说明|用户标识符或授权字符串，或同时在连接字符串中指定 (*InConnectionString*)，违反定义的数据源的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*szMessageText*缓冲区描述错误以及其原因。|  
|HY000|常规错误：无效的文件 dsn|(DM) 中的字符串 **InConnectionString*包含 FILEDSN 关键字，但找不到.dsn 文件的名称。|  
|HY000|常规错误：无法创建文件缓冲区|(DM) 中的字符串 **InConnectionString*包含 FILEDSN 关键字，但.dsn 文件不可读。|  
|HY001|内存分配错误|驱动程序管理器无法分配内存支持执行或完成所需**SQLDriverConnect**函数。<br /><br /> 该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*ConnectionHandle*。 调用该函数，和之前执行完毕[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，然后**SQLDriverConnect**在再次调用函数*ConnectionHandle*。<br /><br /> 或者， **SQLDriverConnect**调用函数，和之前执行完毕**SQLCancelHandle**上调用了*ConnectionHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 另一个以异步方式执行的函数 (不**SQLDriverConnect**) 的调用*ConnectionHandle*和仍在执行时**SQLDriverConnect**调用函数。|  
|HY013|内存管理错误|**SQLDriverConnect**无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*StringLength1*小于 0 且不等于 SQL_NTS。<br /><br /> (DM) 为参数指定的值*BufferLength*小于 0。|  
|HY092|属性/选项标识符无效|（数据挖掘） *DriverCompletion*参数为 SQL_DRIVER_PROMPT，并且*WindowHandle*参数是空指针。|  
|HY110|驱动程序完成无效|(DM) 的参数指定的值*DriverCompletion*不是等于 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 时或 SQL_DRIVER_NOPROMPT。<br /><br /> (DM) 已启用连接池，并为该参数指定的值*DriverCompletion*不是等于 SQL_DRIVER_NOPROMPT。|  
|HYC00|未实现的可选功能|该驱动程序不支持的 ODBC 行为的应用程序请求的版本。|  
|HYT00|超时时间已到|登录超时期限过期之前完成的数据源的连接。 通过设置超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 与指定的数据源名称对应的驱动程序不支持该函数。|  
|IM002|找不到数据源和未指定的默认驱动程序|(DM) 的数据源连接字符串中指定的名称 (*InConnectionString*) 已在系统信息中，找不到但却没有默认的驱动程序规范。<br /><br /> (DM) 的系统信息中找不到 ODBC 数据源和默认驱动程序信息。|  
|IM003|无法加载指定的驱动程序|(DM) 驱动程序的系统信息中的数据源规范中列出或由指定**驱动程序**关键字找不到或无法加载某些其他原因。|  
|IM004|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_ENV 失败|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*fHandleType* SQL_HANDLE_ENV 和驱动程序返回出现错误。|  
|IM005|驱动程序的**SQLAllocHandle**上 SQL_HANDLE_DBC 失败。|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*fHandleType* SQL_HANDLE_DBC 和驱动程序返回出现错误。|  
|IM006|驱动程序的**SQLSetConnectAttr**失败|(DM) 期间**SQLDriverConnect**，驱动程序管理器调用的驱动程序**SQLSetConnectAttr**函数和驱动程序返回了错误。|  
|IM007|任何数据源或驱动程序指定任何引用;禁止的对话框|连接字符串中指定的任何数据源名称或驱动程序和*DriverCompletion*已 SQL_DRIVER_NOPROMPT。|  
|IM008|对话失败|该驱动程序尝试显示其登录对话框，但失败。<br /><br /> *WindowHandle*是空指针，并*DriverCompletion*未 SQL_DRIVER_NO_PROMPT。|  
|IM009|无法加载转换 DLL|该驱动程序无法加载转换为数据源或为连接指定的 DLL。|  
|IM010|数据源名称太长|(DM) DSN 关键字的特性值已超过 SQL_MAX_DSN_LENGTH 个字符。|  
|IM011|驱动程序的名称太长|该属性值 （数据挖掘）**驱动程序**关键字的长度大于 255 个字符。|  
|IM012|驱动程序关键字语法错误|关键字值对 （数据挖掘）**驱动程序**关键字包含语法错误。<br /><br /> (DM) 中的字符串 *\*InConnectionString*包含**FILEDSN**关键字，但.dsn 文件不包含**驱动程序**关键字或**DSN**关键字。|  
|IM014|指定的 DSN 包含驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM015|驱动程序的 SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE 上失败|如果驱动程序将返回 SQL_ERROR，驱动程序管理器将向应用程序返回 SQL_ERROR，并且连接将失败。<br /><br /> 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，您不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 连接字符串具有以下语法：  
  
 *连接字符串*:: =*空字符串*[;]&#124; *特性*[;]&#124; *特性*;*连接字符串*  
  
 *空字符串*:: =*特性*:: =*特性关键字*=*属性值*&#124;驱动程序 = [{}]*属性值*[}]  
  
 *零个以上*:: = DSN &#124; UID &#124; PWD &#124; *驱动程序的定义的属性的关键字*  
  
 *属性值*:: =*字符字符串*  
  
 *驱动程序的定义的零个以上*:: =*标识符*  
  
 其中*字符串*具有零个或多个字符;*标识符*具有一个或多个字符;*特性关键字*不区分大小写;*属性值*可能是区分大小写; 和的值**DSN**关键字不会包含单独的空格。  
  
 由于连接字符串和初始化文件语法、 关键字和属性值包含字符 **[]{}（)，;？\*= ！ @** 不放在大括号，则应避免。 值**DSN**关键字不能只包含空格，且不应包含前导空格。 由于系统信息的语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 应用程序不需要添加大括号后的属性值两边**驱动程序**关键字属性包含一个分号 （;），除非在此情况下大括号是必需。 如果驱动程序收到的属性值包含大括号，驱动程序不应删除它们，但它们应是返回的连接字符串的一部分。  
  
 用大括号括起来的 DSN 或连接字符串值 ({}) 包含的任何字符 **[]{}（)，;？\*= ！ @** 到驱动程序传递不变。 但是，当使用这些字符中的关键字，驱动程序管理器使用文件 Dsn 时将返回错误，但将连接字符串传递给正则连接字符串的驱动程序。 避免使用嵌入的大括号中的关键字值。  
  
 连接字符串可能包含任意数量的驱动程序定义的关键字。 因为**驱动程序**关键字不使用系统信息中的信息，该驱动程序必须定义足够的关键字，以便驱动程序可以连接到数据源连接字符串中使用的信息。 （有关详细信息，请参阅"驱动程序指南"稍后在本部分中）。该驱动程序定义到数据源连接所需的关键字。  
  
 下表描述的属性值**DSN**， **FILEDSN**，**驱动程序**， **UID**， **PWD**，并**SAVEFILE**关键字。  
  
|关键字|属性值说明|  
|-------------|---------------------------------|  
|**DSN**|所返回的数据源的名称**SQLDataSources**或的数据源对话框**SQLDriverConnect**。|  
|**FILEDSN**|数据源的.dsn 文件将从其生成连接字符串的名称。 这些数据源称为文件数据源。|  
|**驱动程序**|通过返回的驱动程序的说明**SQLDrivers**函数。 例如，Rdb 或 SQL Server。|  
|**UID**|用户 id。|  
|**PWD**|对应的用户 ID 或为空字符串，如果没有密码的用户 ID 的密码 (PWD =;）。|  
|**SAVEFILE**|要在其中保存属性值中存在，成功连接使用的关键字.dsn 文件的文件名。|  
  
 有关应用程序如何选择数据源或驱动程序的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果在连接字符串中有重复任何关键字，驱动程序将使用与该关键字的第一个匹配项关联的值。 如果**DSN**并**驱动程序**关键字包括在相同的连接字符串后，驱动程序管理器和驱动程序使用任何关键字将出现第一个。  
  
 **FILEDSN**并**DSN**关键字互相排斥： 使用任何关键字将出现第一个，并且所显示第二个将被忽略。 **FILEDSN**并**驱动程序**关键字，但是，不能互相排斥。 如果在使用连接字符串中出现任何关键字**FILEDSN**，则连接字符串中的关键字的特性值使用而不是.dsn 文件中的相同关键字的特性值。  
  
 如果**FILEDSN**使用关键字、.dsn 文件中指定的关键字用于创建连接字符串。 （有关详细信息，请参阅"文件数据源，"更高版本在本部分中）。**UID**关键字是可选的;.dsn 文件可能只使用创建**驱动程序**关键字。 **PWD** .dsn 文件中不存储关键字。 保存和加载.dsn 文件的默认目录将是指定的路径的组合**CommonFileDir** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion 和"ODBC\DataSources"中。 （如果 CommonFileDir"C:\Program Files\Common Files"，默认目录会为"C:\Program Files\Common Files\ODBC\Data 源"。）  
  
> [!NOTE]  
>  可以直接通过调用操作.dsn 文件[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)并[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)中安装程序 DLL 的函数。  
  
 如果**SAVEFILE**关键字，关键字中存在，成功连接使用的属性值将保存为.dsn 文件的属性值的名称**SAVEFILE**关键字。 **SAVEFILE**必须与结合使用关键字**驱动程序**关键字**FILEDSN**关键字，或两者，或该函数将返回 SQL_SUCCESS_WITH_INFO 与SQLSTATE 01S09 （无效的关键字）。 **SAVEFILE**关键字必须出现之前**驱动程序**关键字在连接字符串，则结果将是未定义。  
  
## <a name="driver-manager-guidelines"></a>驱动程序管理器指导原则  
 驱动程序管理器构造要传递给驱动程序中的连接字符串*InConnectionString*驱动程序的参数**SQLDriverConnect**函数。 驱动程序管理器不会修改*InConnectionString*自变量传递给它的应用程序。  
  
 操作的驱动程序管理器基于的值*DriverCompletion*参数：  
  
-   SQL_DRIVER_PROMPT:如果连接字符串不包含**驱动程序**， **DSN**，或**FILEDSN**关键字，驱动程序管理器将显示数据源对话框。 它构造连接字符串对话框的返回的数据源名称和传递给它的应用程序的其他任何关键字。 驱动程序管理器对话框的返回的数据源名称为空，如果指定的关键字值对，DSN = 默认值。 （此对话框将显示数据源命名为"Default"）。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED:如果应用程序指定的连接字符串包含**DSN**关键字，驱动程序管理器将复制的应用程序指定的连接字符串。 否则将采用相同的操作方式与其何时*DriverCompletion*是 SQL_DRIVER_PROMPT。  
  
-   SQL_DRIVER_NOPROMPT:驱动程序管理器将复制该应用程序指定的连接字符串。  
  
 如果应用程序指定的连接字符串包含**驱动程序**关键字，驱动程序管理器将复制的应用程序指定的连接字符串。  
  
 使用已构造的连接字符串，驱动程序管理器确定使用哪个驱动程序，连接到该驱动程序，并将已构造的连接字符串传递给驱动程序;驱动程序管理器和驱动程序交互的详细信息，请参阅中的"注释"部分[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。 如果连接字符串不包含**驱动程序**关键字，驱动程序管理器确定哪些驱动程序使用，如下所示：  
  
1.  如果连接字符串包含**DSN**关键字，驱动程序管理器将检索与数据源中的系统信息关联的驱动程序。  
  
2.  如果连接字符串不包含**DSN**关键字或数据源找不到，驱动程序管理器检索具有默认数据源中的系统信息关联的驱动程序。 (有关详细信息，请参阅[默认子项](../../../odbc/reference/install/default-subkey.md)。)驱动程序管理器的值更改**DSN**中为"DEFAULT"的连接字符串关键字。  
  
3.  如果**DSN**中的连接字符串关键字设置为"DEFAULT"，驱动程序管理器检索具有默认数据源中的系统信息关联的驱动程序。  
  
4.  如果找不到数据源，找不到默认数据源驱动程序管理器将返回具有 SQLSTATE IM002 SQL_ERROR （找不到数据源和未指定的默认驱动程序）。  
  
## <a name="file-data-sources"></a>文件数据源  
 如果在调用应用程序指定的连接字符串**SQLDriverConnect**包含**FILEDSN**关键字，并且此关键字不会取代通过以下任一方法**DSN**或**驱动程序**关键字，则驱动程序管理器创建使用.dsn 文件中的信息的连接字符串和*InConnectionString*参数。 驱动程序管理器将继续，如下所示：  
  
1.  检查.dsn 文件的文件名称是否有效。 如果不是，它将返回 SQL_ERROR 具有 SQLSTATE IM014 （文件 DSN 的名称无效）。 如果文件名为空字符串 ("") 和 SQL_DRIVER_NOPROMPT 不指定，则**文件打开**显示对话框。 如果文件名包含有效的路径，但任何文件名或无效的文件名称，且未指定 SQL_DRIVER_NOPROMPT，则**文件打开**对话框显示与当前设置为一个文件名称中指定的目录。 如果文件名为空字符串 ("") 或文件名包含有效的路径，但任何文件名或无效的文件名称，并指定 SQL_DRIVER_NOPROMPT 时，然后返回 SQL_ERROR，其中 SQLSTATE IM014 （文件 DSN 的名称无效）。  
  
2.  读取.dsn 文件的 [ODBC] 部分中的所有关键字。 如果**驱动程序**关键字不存在，则返回 SQL_ERROR 具有 SQLSTATE IM012 （驱动程序关键字语法错误），其中.dsn 文件是共享，因此只包含除**DSN**关键字。  
  
     如果非共享文件数据源，驱动程序管理器读取的值**DSN**关键字，并根据需要对用户或系统数据源指向共享的文件数据源的连接。 未执行步骤 3 至 5。  
  
3.  构造的驱动程序连接字符串。 驱动程序连接字符串为.dsn 文件中指定的关键字和原始应用程序连接字符串中指定的联合。 驱动程序连接字符串关键字与发生重叠的构造规则如下所示：  
  
    -   如果**驱动程序**应用程序连接字符串和由指定的驱动程序中存在关键字**驱动程序**关键字不能在.dsn 文件和应用程序连接字符串，则忽略.dsn 文件中的驱动程序信息和使用应用程序连接字符串中的驱动程序信息。 如果通过指定的驱动程序**驱动程序**关键字在.dsn 文件和应用程序的连接字符串，则其中的所有关键字都重叠，应用程序连接字符串中指定的具有优先级高于.dsn 文件中指定。  
  
    -   在新的连接字符串中， **FILEDSN**消除关键字。  
  
4.  通过查看注册表条目 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 中加载该驱动程序。INI\\< 驱动程序名称\>\Driver 其中\<驱动程序名称 > 指定的**驱动程序**关键字。  
  
5.  将驱动程序传递新的连接字符串。  
  
 .Dsn 文件的示例，请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)。  
  
## <a name="savefile-keyword"></a>SAVEFILE 关键字  
 如果应用程序指定的连接字符串包含**SAVEFILE**关键字，则驱动程序管理器将连接字符串保存在.dsn 文件中。 驱动程序管理器将继续，如下所示：  
  
1.  检查是否.dsn 文件的文件名称包含的属性值作为**SAVEFILE**关键字是否有效。 如果不是，它将返回 SQL_ERROR 具有 SQLSTATE IM014 （文件 DSN 的名称无效）。 文件名称的有效性取决于标准系统命名规则。 如果文件名为空字符串 ("") 和*DriverCompletion*参数不为 SQL_DRIVER_NOPROMPT，则文件名称是否有效。 如果文件名称已存在，则如果*DriverCompletion*为 SQL_DRIVER_NOPROMPT，覆盖该文件。 如果*DriverCompletion*为 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED 时，对话框会提示用户指定是否应覆盖该文件。 如果不需要输入，则**文件保存**对话框随即出现。  
  
2.  如果驱动程序返回 SQL_SUCCESS，并且文件名称不为空字符串，则驱动程序管理器将在中返回的连接信息写入*OutConnectionString*参数中指定的格式与指定的文件本节前面的"连接字符串"部分。  
  
3.  如果驱动程序返回 SQL_SUCCESS，且文件名称为空字符串 ("")，然后，驱动程序管理器会调用**文件保存**使用的公共对话框*hwnd*指定和写入的连接信息在中返回*OutConnectionString*前面在本部分中的"连接字符串"部分中指定的格式与在文件保存通用对话框中指定的文件。  
  
4.  如果驱动程序返回 SQL_SUCCESS，它将返回*OutConnectionString*参数，其中包含应用程序的连接字符串。  
  
5.  如果驱动程序将返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，驱动程序管理器对应用程序返回的 SQLSTATE。  
  
## <a name="driver-guidelines"></a>驱动程序指南  
 该驱动程序检查传递给它的驱动程序管理器的连接字符串是否包含**DSN**或**驱动程序**关键字。 如果连接字符串包含**驱动程序**关键字，驱动程序不能从系统信息中检索有关数据源的信息。 如果连接字符串包含**DSN**关键字或不包含**DSN**或**驱动程序**关键字，驱动程序可以检索有关数据源的信息按如下所示的系统信息：  
  
1.  如果连接字符串包含**DSN**关键字，驱动程序将检索指定的数据源的信息。  
  
2.  如果连接字符串不包含**DSN**关键字，未找到指定的数据源，或**DSN**关键字设置为"DEFAULT"，该驱动程序检索默认数据源的信息.  
  
 驱动程序使用它从要在连接字符串中传递给它的信息做出补充的系统信息中检索任何信息。 如果系统信息中的信息复制连接字符串中的信息，该驱动程序连接字符串中使用的信息。  
  
 值的基础*DriverCompletion*，驱动程序提示用户输入连接信息，如用户 ID 和密码，并连接到数据源：  
  
-   SQL_DRIVER_PROMPT:该驱动程序显示一个对话框，作为初始值 （如果有） 使用的连接字符串和系统信息中的值。 当在用户退出对话框中时，驱动程序连接到数据源。 并且还构建了中的值的连接字符串**DSN**或**驱动程序**中的关键字\* *InConnectionString*以及从返回的信息对话框。 它会将此连接字符串中的放置 **OutConnectionString*缓冲区。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED:如果连接字符串包含足够的信息，并且该信息正确无误，驱动程序连接到数据源和副本\* *InConnectionString*到\* *OutConnectionString*. 如果信息缺失或不正确，该驱动程序采用相同的操作方式与其何时*DriverCompletion*除外，如果是 SQL_DRIVER_PROMPT *DriverCompletion*是 SQL_DRIVER_COMPLETE_必需的该驱动程序禁用不需要连接到数据源的任何信息的控件。  
  
-   SQL_DRIVER_NOPROMPT:如果连接字符串包含足够的信息，该驱动程序连接到数据源和副本\* *InConnectionString*到\* *OutConnectionString*。 否则，该驱动程序返回的 SQL_ERROR **SQLDriverConnect**。  
  
 成功连接到数据源，驱动程序还设置\* *StringLength2Ptr*可用于在返回的输出连接字符串的长度 **OutConnectionString*。  
  
 如果用户取消由驱动程序管理器或驱动程序，提供一个对话框**SQLDriverConnect**返回 sql_no_data 为止。  
  
 有关驱动程序管理器和驱动程序在连接过程的交互方式的信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果驱动程序支持**SQLDriverConnect**，该驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**与第二个字符的关键字设置为"Y"。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>连接时启用连接池  
 连接池允许应用程序以重复使用已创建的连接。 当**SQLDriverConnect**调用时，驱动程序管理器尝试建立连接使用的是已被指定为连接池的环境中的连接池的一部分的连接。 有关连接池的详细信息，请参阅[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 应用程序可以在其中启用了连接池连接上调用 SQLDisconnect 之前设置 SQL_ATTR_RESET_CONNECTION。 有关详细信息，请参阅[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 当应用程序调用，以下限制适用**SQLDriverConnect**连接到已入池连接：  
  
-   执行没有连接池处理时**SAVEFILE**连接字符串中指定关键字。  
  
-   如果启用连接池，则**SQLDriverConnect**可以仅使用调用*DriverCompletion* SQL_DRIVER_NOPROMPT 参数; 如果**SQLDriverConnect**称为与任何其他*DriverCompletion*，SQLSTATE HY110 将返回 （无效的驱动程序完成）。  
  
## <a name="connection-attributes"></a>连接属性  
 使用设置的 SQL_ATTR_LOGIN_TIMEOUT 连接属性**SQLSetConnectAttr**，定义要等待的时间由驱动程序返回到应用程序之前完成成功建立连接的登录请求的秒数。 如果系统提示用户完成的连接字符串，每个登录名请求的等待期开始时，驱动程序将启动连接进程。  
  
 该驱动程序默认情况下，在 SQL_MODE_READ_WRITE 访问模式下打开连接。 若要设置的访问模式为 SQL_MODE_READ_ONLY，应用程序必须调用**SQLSetConnectAttr** SQL_ATTR_ACCESS_MODE 属性在调用之前**SQLDriverConnect**。  
  
 如果数据源的系统信息中指定默认转换库，则该驱动程序将其加载。 可以通过调用加载不同的转换库**SQLSetConnectAttr**使用 SQL_ATTR_TRANSLATE_LIB 属性。 可以通过调用指定转换选项**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 选项。  
  
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
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举值来连接到数据源|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|返回驱动程序说明和属性|[SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
