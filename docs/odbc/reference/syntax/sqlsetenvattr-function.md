---
title: SQLSetEnvAttr 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299537"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetEnvAttr**设置管理环境方面的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *环境处理*  
 [输入]环境句柄。  
  
 *特性*  
 [输入]要设置的属性，列在"注释"中。  
  
 *ValuePtr*  
 [输入]指向要与*属性*关联的值的指针。 根据*属性*的值 *，ValuePtr*将是一个 32 位整数值或指向 null 端接的字符串。  
  
 *字符串长度*  
 [输入]如果*ValuePtr*指向字符串或二进制缓冲区，则此参数应为 **ValuePtr*的长度。 对于字符串数据，此参数应包含字符串中的字节数。  
  
 如果*ValuePtr*是整数，则忽略*字符串长度*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetEnvAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_ENV的处理*类型*和环境*句柄**句柄。* 下表列出了**SQLSetEnvAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。 如果驱动程序不支持环境属性，则只能在连接期间返回错误。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持*ValuePtr*中指定的值，并替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY009|无效使用空指针|属性参数标识了需要字符串值的环境属性 *，ValuePtr*参数为空指针。|  
|HY010|函数序列错误|（DM） 已在*环境句柄*上分配了连接句柄。<br /><br /> （DM） **SQL_ATTR_ODBC_VERSION**尚未使用**SQLSetEnvAttr**设置，*属性*不等于**SQL_ATTR_ODBC_VERSION**。 如果使用**SQLAllocHandleStd，** 则无需显式设置**SQL_ATTR_ODBC_VERSION。**|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY024|无效属性值|给定指定的*属性*值，在*ValuePtr*中指定了无效值。|  
|HY090|无效的字符串或缓冲区长度|*字符串长度*参数小于 0，但没有SQL_NTS。|  
|HY092|无效属性/选项标识符|（DM） 为参数*属性*指定的值对驱动程序支持的 ODBC 版本无效。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 环境属性，但驱动程序不支持该属性。<br /><br /> （DM）*属性*参数*SQL_ATTR_OUTPUT_NTS，ValuePtr* SQL_FALSE。|  
  
## <a name="comments"></a>注释  
 仅当未在环境中分配连接句柄时，应用程序才能调用**SQLSetEnvAttr。** 应用程序为环境成功设置的所有环境属性将一直持续到在环境上调用**SQLFreeHandle**为止。 可以在 ODBC *3.x*中同时分配多个环境句柄。  
  
 通过*ValuePtr*设置的信息格式取决于指定的*属性*。 **SQLSetEnvAttr**将接受两种不同格式之一的属性信息：空端字符字符串或 32 位整数值。 每个格式在属性的说明中注明。  
  
 没有特定于驱动程序的环境属性。  
  
 连接属性不能通过调用**SQLSetEnvAttr**来设置。 尝试执行此操作将返回 SQLSTATE HY092（无效属性/选项标识符）。  
  
|*特性*|*价值 Ptr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING （ODBC 3.8）|32 位 SQLUINTEGER 值，可在环境级别启用或禁用连接池。 使用以下值：<br /><br /> SQL_CP_OFF = 连接池已关闭。 这是默认值。<br /><br /> SQL_CP_ONE_PER_DRIVER = 每个驱动程序都支持单个连接池。 池中的每个连接都与一个驱动程序相关联。<br /><br /> SQL_CP_ONE_PER_HENV = 每个环境都支持单个连接池。 池中的每个连接都与一个环境相关联。<br /><br /> SQL_CP_DRIVER_AWARE = 如果驱动程序可用，请使用驱动程序的连接池感知功能。 如果驱动程序不支持连接池感知，则忽略SQL_CP_DRIVER_AWARE，并使用SQL_CP_ONE_PER_HENV。 有关详细信息，请参阅[驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。 在某些驱动程序支持并且某些驱动程序不支持连接池感知的环境中，SQL_CP_DRIVER_AWARE可以在支持驱动程序上启用连接池感知功能，但它等效于将设置为SQL_CP_ONE_PER_HENV不支持连接池感知功能的驱动程序。<br /><br /> 通过调用**SQLSetEnvAttr**将SQL_ATTR_CONNECTION_POOLING属性设置为SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV，从而启用连接池。 在应用程序分配要为其启用连接池的共享环境之前，必须进行此调用。 **SQLSetEnvAttr**调用中的环境句柄设置为 null，这使得SQL_ATTR_CONNECTION_POOLING进程级属性。 启用连接池后，应用程序将调用**SQLAllocHandle**并设置为 SQL_HANDLE_ENV的 *"输入句柄*"参数来分配隐式共享环境。<br /><br /> 启用连接池并为应用程序选择共享环境后，无法为该环境重置SQL_ATTR_CONNECTION_POOLING，因为在设置此属性时使用空环境句柄调用**SQLSetEnvAttr。** 如果在共享环境中启用连接池时设置了此属性，则该属性仅影响随后分配的共享环境。<br /><br /> 还可以在环境中启用连接池。 请注意以下有关环境连接池：<br /><br /> - 在 NULL 句柄上启用连接池是进程级属性。 随后分配的环境将是一个共享环境，并将继承进程级连接池设置。<br />- 分配环境后，应用程序仍可以更改其连接池设置。<br />- 如果启用了环境连接池，并且连接的驱动程序使用驱动程序池，则环境池将优先。<br /><br /> SQL_ATTR_CONNECTION_POOLING在驱动程序管理器内实现。 驱动程序不需要实现SQL_ATTR_CONNECTION_POOLING。 ODBC 2.0 和 3.0 应用程序可以设置此环境属性。<br /><br /> 有关详细信息，请参阅 [ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_CP_MATCH （ODBC 3.0）|32 位 SQLUINTEGER 值，用于确定如何从连接池中选择连接。 当调用**SQLConnect**或**SQLDriverConnect**时，驱动程序管理器确定从池中重用哪个连接。 驱动程序管理器尝试将调用中的连接选项以及应用程序设置的连接属性与池中连接的关键字和连接属性相匹配。 此属性的值确定匹配条件的精度级别。<br /><br /> 以下值用于设置此属性的值：<br /><br /> SQL_CP_STRICT_MATCH = 仅重复使用与调用中的连接选项和应用程序设置的连接属性完全匹配的连接。 这是默认值。<br /><br /> SQL_CP_RELAXED_MATCH = 可以使用具有匹配连接字符串关键字的连接。 关键字必须匹配，但不是所有连接属性都必须匹配。<br /><br /> 有关驱动程序管理器在连接到池连接时如何执行匹配的详细信息，请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。 有关连接池的详细信息，请参阅[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_ODBC_VERSION （ODBC 3.0）|32 位整数，用于确定某些功能是否显示 ODBC *2.x*行为还是 ODBC *3.x*行为。 以下值用于设置此属性的值：<br /><br /> SQL_OV_ODBC3_80 = 驱动程序管理器和驱动程序表现出以下 ODBC 3.8 行为：<br /><br /> - 驱动程序返回并期望 ODBC *3.x*日期、时间和时间戳的代码。<br />- 当调用**SQLError、SQLGetDiagField**或**SQLGetDiagRec**时，驱动程序返回 ODBC *3.x* SQLSTATE 代码。 **SQLError**<br />- 对**SQLTables**的调用中的*目录名称*参数接受搜索模式。<br />- 驱动程序管理器支持 C 数据类型扩展性。 有关 C 数据类型扩展性的详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。<br /><br /> 有关详细信息，请参阅[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。<br /><br /> SQL_OV_ODBC3 = 驱动程序管理器和驱动程序表现出以下 ODBC *3.x*行为：<br /><br /> - 驱动程序返回并期望 ODBC *3.x*日期、时间和时间戳的代码。<br />- 当调用**SQLError、SQLGetDiagField**或**SQLGetDiagRec**时，驱动程序返回 ODBC *3.x* SQLSTATE 代码。 **SQLError**<br />- 对**SQLTables**的调用中的*目录名称*参数接受搜索模式。<br />- 驱动程序管理器不支持 C 数据类型扩展性。<br /><br /> SQL_OV_ODBC2 = 驱动程序管理器和驱动程序表现出以下 ODBC *2.x*行为。 这对于使用 ODBC *3.x*驱动程序的 ODBC *2.x*应用程序特别有用。<br /><br /> - 驱动程序返回并期望 ODBC *2.x*日期、时间和时间戳的代码。<br />- 当调用**SQLError、SQLGetDiagField**或**SQLGetDiagRec**时，驱动程序返回 ODBC *2.x* SQLSTATE 代码。 **SQLError**<br />- 调用**SQLTables**中的*目录名称*参数不接受搜索模式。<br />- 驱动程序管理器不支持 C 数据类型扩展性。<br /><br /> 应用程序在调用具有 SQLHENV 参数的任何函数之前必须设置此环境属性，否则调用将返回 SQLSTATE HY010（函数序列错误）。 这些环境标志是否存在其他行为是特定于驱动程序的。<br /><br /> - 有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)[和行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。|  
|SQL_ATTR_OUTPUT_NTS （ODBC 3.0）|一个 32 位整数，用于确定驱动程序返回字符串数据的方式。 如果SQL_TRUE，驱动程序返回字符串数据为 null 终止。 如果SQL_FALSE，驱动程序不会返回字符串数据为 null 终止。<br /><br /> 此属性默认为SQL_TRUE。 调用**SQLSetEnvAttr**将其设置为SQL_TRUE返回SQL_SUCCESS。 调用**SQLSetEnvAttr**将其设置为SQL_FALSE返回SQL_ERROR和 SQLSTATE HYC00（未实现可选功能）。|  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|返回环境属性的设置|[SQLGetEnvAttr 函数](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
