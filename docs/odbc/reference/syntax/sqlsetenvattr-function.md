---
title: "SQLSetEnvAttr 函数 |Microsoft 文档"
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
apiname: SQLSetEnvAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetEnvAttr
helpviewer_keywords: SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
caps.latest.revision: "38"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad246dc337b57eb97b588c1ed08bb380cc4d6185
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetEnvAttr**设置控制方面的环境的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>参数  
 *EnvironmentHandle*  
 [输入]环境句柄。  
  
 *Attribute*  
 [输入]要设置，属性列在"注释"。  
  
 *ValuePtr*  
 [输入]指向要与之关联的值*属性*。 根据值*属性*， *ValuePtr*将 32 位整数值或指向以 null 结尾的字符串。  
  
 *StringLength*  
 [输入]如果*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度 **ValuePtr*。 对于字符串数据，此自变量应包含在字符串中的字节数。  
  
 如果*ValuePtr*是一个整数， *StringLength*将被忽略。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetEnvAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_ENV 和*处理*的*EnvironmentHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetEnvAttr**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。 如果驱动程序不支持的环境属性，则可以仅在连接时返回的错误。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|该驱动程序不支持在指定的值*ValuePtr*和替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY009|不允许使用 null 指针|特性自变量标识所需的字符串值，环境属性和*ValuePtr*自变量是空指针。|  
|HY010|函数序列错误|(DM) 上分配了连接句柄*EnvironmentHandle*。<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION**尚未设置与**SQLSetEnvAttr**和*属性*是否不等于**SQL_ATTR_ODBC_VERSION**。 不需要设置**SQL_ATTR_ODBC_VERSION**显式如果你使用**SQLAllocHandleStd**。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY024|无效属性值|给出指定*属性*中值，指定无效的值是*ValuePtr*。|  
|HY090|字符串或缓冲区长度无效|*StringLength*自变量为小于 0，但未 sql_nts 以。|  
|HY092|属性/选项标识符无效|(DM) 值的参数的指定*属性*对 ODBC 驱动程序支持的版本无效。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*属性*是有效的 ODBC 环境属性的 ODBC 版本所支持的驱动程序，但该驱动程序不支持。<br /><br /> (DM)*属性*自变量为 SQL_ATTR_OUTPUT_NTS，和*ValuePtr*已 SQL_FALSE。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetEnvAttr**仅当在环境上分配没有连接句柄。 已成功设置环境的应用程序的所有环境属性都保留直到**SQLFreeHandle**在环境上调用。 ODBC 3 中可以同时分配多个环境句柄*.x*。  
  
 通过设置信息的格式*ValuePtr*取决于指定*属性*。 **SQLSetEnvAttr**将接受两个不同的格式之一的特性信息： 以 null 结尾的字符串或 32 位整数值。 每个格式将其记录在该特性的说明。  
  
 没有特定于驱动程序的环境属性。  
  
 连接属性不能通过调用设置**SQLSetEnvAttr**。 尝试执行此操作将返回 SQLSTATE HY092 （无效的属性/选项标识符）。  
  
|*Attribute*|*ValuePtr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|一个 32 位 SQLUINTEGER 值，启用或禁用连接池环境级别。 使用以下值：<br /><br /> SQL_CP_OFF = 连接池已关闭。 这是默认设置。<br /><br /> SQL_CP_ONE_PER_DRIVER = 单个连接池支持为每个驱动程序。 池中的每个连接都使用一个驱动程序相关联。<br /><br /> SQL_CP_ONE_PER_HENV = 单个连接池支持为每个环境。 池中的每个连接都与一个环境相关联。<br /><br /> SQL_CP_DRIVER_AWARE = 使用该驱动程序，连接池感知功能是否可用。 如果该驱动程序不支持连接池感知，忽略 SQL_CP_DRIVER_AWARE，而 SQL_CP_ONE_PER_HENV。 有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。 在某些驱动程序支持，其中某些驱动程序不支持连接池感知的环境，SQL_CP_DRIVER_AWARE 可以启用连接池感知功能上是支持驱动程序，但它相当于 SQL_CP_ONE_PER_HENV 上的设置这些驱动程序不支持连接池感知功能。<br /><br /> 通过调用启用连接池**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 特性设置为 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 应用程序分配的连接池是启用的共享的环境之前，必须进行此调用。 对的调用中的环境句柄**SQLSetEnvAttr**设置为 null，这样 SQL_ATTR_CONNECTION_POOLING 了进程级别属性。 然后，应用程序启用连接池后，通过调用分配隐式的共享的环境**SQLAllocHandle**与*InputHandle*参数设置为 SQL_HANDLE_ENV。<br /><br /> 已启用连接池且已为应用程序选择了共享的环境后，SQL_ATTR_CONNECTION_POOLING 无法重置为该环境中，因为**SQLSetEnvAttr**称为 null 环境句柄时将此属性设置。 如果在共享环境上已启用连接池时设置此属性，该属性会影响仅随后分配的共享的环境。<br /><br /> 还有可能要启用连接池在该环境。 请注意下列有关环境连接池：<br /><br /> -启用连接池在 NULL 句柄是的进程级属性。 随后分配的环境将共享的环境中，并且将继承进程级连接池设置。<br />-分配环境后，应用程序仍可更改其连接池设置。<br />-如果启用环境连接池和连接的驱动程序使用驱动程序池，环境池采用首选项。<br /><br /> SQL_ATTR_CONNECTION_POOLING 实现驱动程序管理器内部。 驱动程序不需要实现 SQL_ATTR_CONNECTION_POOLING。 ODBC 2.0 和 3.0 的应用程序可以将此环境属性设置。<br /><br /> 有关详细信息，请参阅[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|32 位 SQLUINTEGER 值，该值确定如何从连接池中选择一个连接。 当**SQLConnect**或**SQLDriverConnect**是驱动程序管理器调用，确定从池中重复使用的连接。 驱动程序管理器尝试匹配该呼叫，设置了关键字和连接属性连接的应用程序池中的连接属性中的连接选项。 此属性的值确定匹配条件的精度的级别。<br /><br /> 以下值用于设置此属性的值：<br /><br /> SQL_CP_STRICT_MATCH = 完全匹配的调用中的连接选项的唯一连接和应用程序设置的特性会重复使用的连接。 这是默认设置。<br /><br /> SQL_CP_RELAXED_MATCH = 具有匹配，可以使用关键字的连接字符串的连接。 关键字必须匹配，但并非所有连接特性必须都匹配。<br /><br /> 有关如何驱动程序管理器在连接到已入池连接中执行匹配时的详细信息，请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。 有关连接池的详细信息，请参阅[ODBC 连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|一个 32 位整数，它确定某些功能是否出现 ODBC 2*.x*行为或 ODBC 3*.x*行为。 以下值用于设置此属性的值：<br /><br /> SQL_OV_ODBC3_80 = 驱动程序管理器和驱动程序展示以下 ODBC 3.8 行为：<br /><br /> -驱动程序返回，并且期望 ODBC 3。*x*日期、 时间和时间戳的代码。<br />-驱动程序返回 ODBC 3。*x* SQLSTATE 代码时**SQLError**， **SQLGetDiagField**，或**SQLGetDiagRec**调用。<br />- *CatalogName*对的调用中的自变量**SQLTables**接受搜索模式。<br />-驱动程序管理器支持 C 数据类型可扩展性。 有关 C 数据类型扩展性的详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。<br /><br /> 有关详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。<br /><br /> SQL_OV_ODBC3 = 驱动程序管理器和驱动程序展示以下 ODBC 3*.x*行为：<br /><br /> -驱动程序返回，并且期望 ODBC 3*.x*日期、 时间和时间戳的代码。<br />-驱动程序返回 ODBC 3*.x* SQLSTATE 代码时**SQLError**， **SQLGetDiagField**，或**SQLGetDiagRec**调用。<br />- *CatalogName*对的调用中的自变量**SQLTables**接受搜索模式。<br />-驱动程序管理器不支持 C 数据类型可扩展性。<br /><br /> SQL_OV_ODBC2 = 驱动程序管理器和驱动程序展示以下 ODBC 2*.x*行为。 这是非常适合 ODBC 2*.x*应用程序使用 ODBC 3*.x*驱动程序。<br /><br /> -驱动程序返回，并且期望 ODBC 2*.x*日期、 时间和时间戳的代码。<br />-驱动程序返回 ODBC 2*.x* SQLSTATE 代码时**SQLError**， **SQLGetDiagField**，或**SQLGetDiagRec**调用。<br />- *CatalogName*对的调用中的自变量**SQLTables**不接受的搜索模式。<br />-驱动程序管理器不支持 C 数据类型可扩展性。<br /><br /> 应用程序必须设置此环境属性，然后才能调用任何函数具有 SQLHENV 自变量，或调用将返回 SQLSTATE HY010 （函数序列错误）。 它是特定于驱动程序的额外的行为是否存在这些环境的标志。<br /><br /> -有关详细信息，请参阅[声明应用程序的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|一个 32 位整数，它确定如何驱动程序返回字符串数据。 如果 SQL_TRUE，驱动程序返回以 null 结尾的字符串数据。 如果 SQL_FALSE，驱动程序不返回以 null 结尾的字符串数据。<br /><br /> 此属性默认为 SQL_TRUE。 调用**SQLSetEnvAttr**将它设置为 SQL_TRUE 返回 SQL_SUCCESS。 调用**SQLSetEnvAttr**将它设置为 SQL_FALSE 返回 SQL_ERROR 和 SQLSTATE HYC00 （未实现的可选功能）。|  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|返回环境属性的设置|[SQLGetEnvAttr 函数](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
