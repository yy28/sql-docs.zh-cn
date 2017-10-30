---
title: "SQLSetDescField 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3a67508ad9e676e679f0458eef8e46960cc72737
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetDescField**设置单个字段的描述符记录的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>参数  
 *DescriptorHandle*  
 [输入]描述符句柄。  
  
 *RecNumber*  
 [输入]指示包含应用程序试图设置字段的描述符记录。 描述符记录与记录号 0 表示的书签记录编号从 0。 *RecNumber*标头字段，将忽略参数。  
  
 *FieldIdentifier*  
 [输入]表示其值是要设置的描述符字段。 有关详细信息，请参阅"*FieldIdentifier*自变量"中的"注释"部分。  
  
 *ValuePtr*  
 [输入]指向包含描述符信息中或一个整数值的缓冲区的指针。 数据类型的值取决于*FieldIdentifier*。 如果*ValuePtr*是一个整数值，它可能被视为 8 个字节 (SQLLEN)、 4 个字节 (SQLINTEGER) 或 2 个字节 (SQLSMALLINT)，具体取决于值*FieldIdentifier*自变量。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度 **ValuePtr*。 对于字符串数据，此自变量应包含在字符串中的字节数。  
  
 如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*是一个整数， *BufferLength*将被忽略。  
  
 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指明字段到驱动程序管理器的性质*BufferLength*自变量。 *BufferLength*可以具有下列值：  
  
-   如果*ValuePtr*然后是指向字符串， *BufferLength*是字符串或 sql_nts 以的长度。  
  
-   如果*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定长度的值，然后*BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetDescField**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DESC 和*处理*的*DescriptorHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetDescField**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|该驱动程序不支持在指定的值* \*ValuePtr* (如果*ValuePtr*是一个指针) 或值在*ValuePtr* (如果*ValuePtr*是一个整数值)，或* \*ValuePtr*无效由于实现工作条件，因此驱动程序替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|无效的描述符索引|*FieldIdentifier*自变量为记录字段中， *RecNumber*自变量为 0，和*DescriptorHandle*自变量引用 IPD 句柄。<br /><br /> *RecNumber*自变量为 0，小于和*DescriptorHandle* ARD 或 APD 引用自变量。<br /><br /> *RecNumber*参数为大于最大列数或数据源可以支持的参数和*DescriptorHandle*到 APD 或 ARD 引用自变量。<br /><br /> (DM) *FieldIdentifier*自变量为 SQL_DESC_COUNT，和* \*ValuePtr*自变量为小于 0。<br /><br /> *RecNumber*自变量为等于 0，和*DescriptorHandle*隐式分配 APD 引用自变量。 （具有显式分配应用程序描述符，不会出现此错误因为并不知道显式分配应用程序描述符是 APD 或直到 ARD 执行时间。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22001|字符串数据，右截断|*FieldIdentifier*自变量为 SQL_DESC_NAME，和*BufferLength*参数为大于 SQL_MAX_IDENTIFIER_LEN 的值。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) *DescriptorHandle*与关联*StatementHandle*其中一个以异步方式执行的函数 （而不此是） 调用和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*与其*DescriptorHandle*成功关联并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此异步函数仍在执行时**SQLSetDescField**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**与关联的语句句柄之一调用*DescriptorHandle*并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY016|无法修改实现行描述符|*DescriptorHandle*自变量为与 IRD 关联和*FieldIdentifier*参数不为 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段不构成有效的 ODBC SQL 类型或特定于驱动程序的 SQL 类型 （对于无效 IPDs) 或有效的 ODBC C 类型 （对于 APDs 或 ARDs）。<br /><br /> 在一致性检查过程中检查的描述符信息未一致。 (请参阅中的"一致性检查" **SQLSetDescRec**。)|  
|HY090|字符串或缓冲区长度无效|(DM) * \*ValuePtr*是一个字符串，和*BufferLength*而小于零，但不是等于 sql_nts 以。<br /><br /> (DM) 驱动程序是 ODBC 2*.x*驱动程序，该描述符已 ARD *ColumnNumber*参数已设置为 0，并为参数指定的值*BufferLength*已不等于 4。|  
|HY091|描述符字段标识符无效|为指定的值*FieldIdentifier*自变量不是一个 ODBC 定义的字段，且未实现定义的值。<br /><br /> *FieldIdentifier*自变量无效的*DescriptorHandle*自变量。<br /><br /> *FieldIdentifier*自变量为只读的、 ODBC 定义字段。|  
|HY092|属性/选项标识符无效|中的值* \*ValuePtr*对无效*FieldIdentifier*自变量。<br /><br /> *FieldIdentifier*自变量为 SQL_DESC_UNNAMED，和*ValuePtr*已 SQL_NAMED。|  
|HY105|无效的参数类型|(DM) 指定为 SQL_DESC_PARAMETER_TYPE 字段的值无效。 (有关详细信息，请参阅"*InputOutputType*自变量"部分中**SQLBindParameter**。)|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetDescField**若要将一个任何描述符字段设置一次。 一次调用**SQLSetDescField**设置单个描述符中的单个字段。 此函数可以调用以在任何描述符类型中设置任何字段，提供可以设置该字段。 （请参阅本节后面的表。）  
  
> [!NOTE]  
>  如果调用**SQLSetDescField**失败，由标识的描述符记录的内容*RecNumber*自变量是不确定。  
  
 可以调用其他函数，以设置函数一次调用的多个描述符字段。 **SQLSetDescRec**函数设置了不同的字段的数据类型和缓冲区绑定到的列或参数 （SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_PRECISION、 SQL_ 的影响DESC_SCALE、 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 字段）。 **SQLBindCol**或**SQLBindParameter**用于进行绑定的列或参数的完整规范。 这些函数将设置一个函数调用的描述符字段的特定组。  
  
 **SQLSetDescField**可以调用以通过将偏移量添加到绑定指针 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 或 SQL_DESC_OCTET_LENGTH_PTR） 更改的绑定缓冲区。 这将更改而不调用绑定缓冲区**SQLBindCol**或**SQLBindParameter**，这允许应用程序而无需更改其他字段，例如 SQL_DESC_DATA_ 更改 SQL_DESC_DATA_PTR类型。  
  
 如果应用程序调用**SQLSetDescField**若要设置 SQL_DESC_COUNT 以外的任何字段或延迟的字段 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 或 SQL_DESC_INDICATOR_PTR，记录将成为未绑定。  
  
 通过调用设置描述符标头字段**SQLSetDescField**使用相应*FieldIdentifier*。 标头的多个字段，还有一些语句特性，因此还可以通过调用设置它们**SQLSetStmtAttr**。 这允许应用程序将描述符字段设置事先未获得的描述符句柄。 当**SQLSetDescField**调用来设置的标头字段， *RecNumber*忽略自变量。  
  
 A *RecNumber* 0 的用于设置书签字段。  
  
> [!NOTE]  
>  语句属性 SQL_ATTR_USE_BOOKMARKS 应始终设置，然后再调**SQLSetDescField**设置书签字段。 虽然这不是必需的强烈建议。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>设置描述符字段的序列  
 当通过调用设置描述符字段**SQLSetDescField**，应用程序必须遵循特定的顺序：  
  
1.  应用程序必须首先设置 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 或 SQL_DESC_DATETIME_INTERVAL_CODE 字段。  
  
2.  设置这些字段之一后，应用程序可以设置的数据类型，属性和驱动程序将设置数据类型属性字段的数据类型的相应默认值。 自动将使用默认值的类型特性字段可确保描述符始终可供使用后一种数据类型指定应用程序。 如果应用程序显式设置数据类型的属性，它重写默认属性。  
  
3.  步骤 1 中列出的字段之一已被设置，并且数据类型属性已设置后，应用程序可以设置 SQL_DESC_DATA_PTR。 这将提示的一致性检查的描述符字段。 如果应用程序设置 SQL_DESC_DATA_PTR 字段后更改的数据类型或属性，该驱动程序会将 SQL_DESC_DATA_PTR 设置为 null 指针，取消绑定记录。 这将强制使应用程序描述符记录可用之前，在序列中，完成的正确步骤。  
  
## <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化  
 如果分配的描述符，描述符中的字段可以初始化为默认值、 没有默认值，初始化或是未定义类型描述符。 下表指示每种类型描述符，使用"D"，该值指示该字段被初始化默认值，和"ND"，该值指示该字段被初始化无默认值的每个字段的初始化。 如果显示一个数字，则该字段的默认值是该数字。 表还指明一个字段是否为读/写 (R/W) 或只读 (R)。  
  
 仅在已准备或执行该语句并不是在已分配的语句句柄或描述符时填充，IRD 后，IRD 字段具有默认值。 直到已填充 IRD，任何尝试访问的 IRD 字段将返回错误。  
  
 某些描述符字段定义为一个或多个，但不是全部的描述符类型 （ARDs 和 IRDs，APDs 和 IPDs）。 未定义类型描述符的字段时，不需要按任何使用该描述符的函数。  
  
 可以通过访问的字段**SQLGetDescField**不一定能通过设置**SQLSetDescField**。 可以通过设置的字段**SQLSetDescField**下表中列出。  
  
 下表概述了标头字段的初始化。  
  
|标头字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: 有关 SQL_DESC_ALLOC_AUTO 隐式或 SQL_DESC_ALLOC_USER 为显式<br /><br /> APD: 有关 SQL_DESC_ALLOC_AUTO 隐式或 SQL_DESC_ALLOC_USER 为显式<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: [1] APD: [1] IRD： 未使用的 IPD： 未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|ARD: R/W APD: R/W IRD: R/W IPD: R/W|ARD: Null ptr APD: Null ptr IRD: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD： 未使用<br /><br /> IPD： 未使用|  
SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|ARD： 未使用的 APD： 未使用的 IRD: R/W IPD: R/W|ARD： 未使用的 APD： 未使用 IRD: Null ptr IPD: Null ptr|  
  
 [只有在 IPD 自动填充由驱动程序时，将定义 1] 这些字段。 如果不是，它们是未定义。 如果应用程序尝试设置这些字段，SQLSTATE HY091 将返回 （描述符字段标识符无效）。  
  
 下表中所示，将为记录的字段的初始化。  
  
|记录字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_ 默认 APD: SQL_C_ 默认 IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用的 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_LABEL|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD： 未使用的 IPD: R/W|ARD： 未使用的 APD： 未使用的 IRD： 未使用的 IPD: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD： 未使用<br /><br /> APD： 未使用<br /><br /> IRD: R<br /><br /> IPD: R|ARD： 未使用<br /><br /> APD： 未使用<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
SQL_DESC_TYPE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
  
 [只有在 IPD 自动填充由驱动程序时，将定义 1] 这些字段。 如果不是，它们是未定义。 如果应用程序尝试设置这些字段，SQLSTATE HY091 将返回 （描述符字段标识符无效）。  
  
 [可以设置中 IPD 2] 的 SQL_DESC_DATA_PTR 字段来强制执行一致性检查。 中的后续调用**SQLGetDescField**或**SQLGetDescRec**，驱动程序不需要返回 SQL_DESC_DATA_PTR 已设置为的值。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 自变量  
 *FieldIdentifier*参数指示要设置的描述符字段。 描述符包含*描述符标头，*中下一节，"标头字段，"和零个或更多描述的标头字段组成*描述符记录*包含的记录字段节"标头字段"部分所述。  
  
## <a name="header-fields"></a>标头字段  
 每个描述符具有标头包含以下字段：  
  
 **SQL_DESC_ALLOC_TYPE [全部]**  
 此只读 SQLSMALLINT 标头字段指定显式由驱动程序或应用程序是否自动分配的描述符。 应用程序可以获取，但不是能修改此字段。 字段是设置为 SQL_DESC_ALLOC_AUTO 由驱动程序，如果描述符已自动分配由驱动程序。 如果描述符已显式分配应用程序，它是由驱动程序设置 SQL_DESC_ALLOC_USER。  
  
 **SQL_DESC_ARRAY_SIZE [应用程序描述符]**  
 在 ARDs，此 SQLULEN 标头字段指定行集中的行的数。 这是通过调用返回的行数**SQLFetch**或**SQLFetchScroll**或通过调用来操作**SQLBulkOperations**或**SQLSetPos**.  
  
 在 APDs，此 SQLULEN 标头字段指定的每个参数的值的数目。  
  
 此字段的默认值为 1。 如果 SQL_DESC_ARRAY_SIZE 大于 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 APD 或 ARD SQL_DESC_OCTET_LENGTH_PTR 指向数组。 基数的每个数组等于此字段的值。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**具有 SQL_ATTR_ROW_ARRAY_SIZE 属性。 此外可以通过调用设置此字段中 APD **SQLSetStmtAttr**具有 SQL_ATTR_PARAMSET_SIZE 属性。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [全部]**  
 对于每个描述符类型，此 SQLUSMALLINT * 标头字段指向数组的 SQLUSMALLINT 值。 这些阵列，如下所示命名： 行状态数组 (IRD)、 参数状态数组 (IPD)、 行操作数组 (ARD) 和参数操作数组 (APD)。  
  
 在 IRD，此标头字段将指向包含到调用后的状态值的行状态数组**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 数组有有行的行集中的所有元素。 应用程序必须分配 SQLUSMALLINTs 一个数组，并将此字段为指向数组设置。 默认情况下，字段设置为 null 指针。 该驱动程序将填充数组-除非 SQL_DESC_ARRAY_STATUS_PTR 字段设置为 null 指针，在这种情况下会生成无状态值，且未填充数组。  
  
> [!CAUTION]  
>  如果应用程序将设置指向 IRD SQL_DESC_ARRAY_STATUS_PTR 字段的行状态数组的元素，驱动程序行为不确定。  
  
 通过调用最初填充数组**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 如果调用未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此字段的指向数组的内容将不确定。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_SUCCESS： 行提取了成功，并且自上次提取后已不更改。  
  
-   SQL_ROW_SUCCESS_WITH_INFO： 行提取了成功，并且自上次提取后已不更改。 但是，有关行返回一条警告。  
  
-   SQL_ROW_ERROR： 提取行时出错。  
  
-   SQL_ROW_UPDATED： 的行提取了成功和自从上次提取已更新。 如果该行被再次提取，其状态将为 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED： 已删除行，因为上次提取。  
  
-   SQL_ROW_ADDED: 行所插入的**SQLBulkOperations**。 如果该行被再次提取，其状态将为 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW: 行集占用该结果集的末尾，并且会不返回任何行，对应于此元素的行状态数组。  
  
 此外可以通过调用设置此字段中 IRD **SQLSetStmtAttr**具有 SQL_ATTR_ROW_STATUS_PTR 属性。  
  
 仅已返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 后才能有效 IRD SQL_DESC_ARRAY_STATUS_PTR 字段。 如果返回的代码不是其中一种，通过 SQL_DESC_ROWS_PROCESSED_PTR 指向的位置是未定义。  
  
 在 IPD，此标头字段将指向包含状态信息的每组参数值后调用的参数状态数组**SQLExecute**或**SQLExecDirect**。 如果调用**SQLExecute**或**SQLExecDirect**未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此字段的指向数组的内容是不确定。 应用程序必须分配 SQLUSMALLINTs 一个数组，并将此字段为指向数组设置。 该驱动程序将填充数组-除非 SQL_DESC_ARRAY_STATUS_PTR 字段设置为 null 指针，在这种情况下会生成无状态值，且未填充数组。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_SUCCESS： 此参数集的已成功执行 SQL 语句。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: SQL 语句成功执行的参数; 此集但是，诊断数据结构中提供了警告信息。  
  
-   SQL_PARAM_ERROR： 在处理此组参数时出错。 中的诊断数据结构提供了其他错误信息。  
  
-   SQL_PARAM_UNUSED： 此参数集已不再使用，可能是因为，某些以前的参数集导致中止将来进行处理，出现错误，或因为 SQL_PARAM_IGNORE 已设置为该 SQL_DESC_ARRAY_ 所指定的数组中的参数集APD STATUS_PTR 字段。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE： 诊断信息不可用。 此示例是信息的驱动程序会参数的数组将作为一个整体的单元，因此不会生成此级别的错误。  
  
 此外可以通过调用设置此字段中 IPD **SQLSetStmtAttr**具有 SQL_ATTR_PARAM_STATUS_PTR 属性。  
  
 在 ARD，此标头字段将指向可以通过指示此行是否要忽略应用程序设置的值的行操作数组**SQLSetPos**操作。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_PROCEED: 行包含在大容量操作中使用**SQLSetPos**。 （此设置不保证在行上将发生，该操作。 如果该行有状态 SQL_ROW_ERROR IRD 行状态数组中的，该驱动程序可能不能在行中执行该操作。）  
  
-   SQL_ROW_IGNORE: 行从大容量操作使用排除**SQLSetPos**。  
  
 如果不设置数组的任何元素，将在大容量操作中包括所有行。 如果 ARD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为 null 指针，所有行都将都纳入大容量操作中;就像指针指向有效的数组和数组的所有元素都是 SQL_ROW_PROCEED，解释都是相同的。 如果数组中的元素设置为 SQL_ROW_IGNORE 中忽略的行的行状态数组, 值不会更改。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**具有 SQL_ATTR_ROW_OPERATION_PTR 属性。  
  
 在 APD，此标头字段将指向可以由应用程序，以指示是否将是此组参数设置的值的参数操作数组时忽略**SQLExecute**或**SQLExecDirect**调用。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_PROCEED: 参数集纳入**SQLExecute**或**SQLExecDirect**调用。  
  
-   SQL_PARAM_IGNORE： 的参数集已从排除**SQLExecute**或**SQLExecDirect**调用。  
  
 如果不设置了数组的任何元素中使用的参数数组中的所有集**SQLExecute**或**SQLExecDirect**调用。 如果 APD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为 null 指针，将使用的参数的所有集;就像指针指向有效的数组和数组的所有元素都是 SQL_PARAM_PROCEED，解释都是相同的。  
  
 此外可以通过调用设置此字段中 APD **SQLSetStmtAttr**具有 SQL_ATTR_PARAM_OPERATION_PTR 属性。  
  
 **SQL_DESC_BIND_OFFSET_PTR [应用程序描述符]**  
 此 SQLLEN * 标头字段指向绑定偏移量。 它是默认设置为 null 指针。 如果此字段不是 null 指针，该驱动程序取消引用指针，并将取消引用的值添加到每个延迟描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中具有非 null 值的字段在提取时间并使用新的指针值时绑定。  
  
 绑定偏移量是始终直接添加到 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段中的值。 如果偏移量更改为不同的值，新值仍会添加直接向每个描述符字段中的值。 新的偏移量不会添加到的字段值加上任何早期的偏移量。  
  
 此字段是*延迟的字段*： 在时它设置使用的却是在更高版本时由驱动程序需要确定的数据缓冲区的地址时不使用它。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**具有 SQL_ATTR_ROW_BIND_OFFSET_PTR 属性。 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**具有 SQL_ATTR_PARAM_BIND_OFFSET_PTR 属性。  
  
 有关详细信息，请参阅中的按行绑定的说明[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)和[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 **SQL_DESC_BIND_TYPE [应用程序描述符]**  
 此 SQLUINTEGER 标头字段绑定将方向设置为用于绑定列或参数。  
  
 在 ARDs，此字段指定的绑定方向时**SQLFetchScroll**或**SQLFetch**调用相关联的语句句柄。  
  
 若要选择的列的列绑定，此字段设置为 SQL_BIND_BY_COLUMN （默认值）。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**与 SQL_ATTR_ROW_BIND_TYPE*属性*。  
  
 在 APDs，此字段指定要用于动态参数的绑定方向。  
  
 若要选择列绑定参数，此字段设置为 SQL_BIND_BY_COLUMN （默认值）。  
  
 此外可以通过调用设置此字段中 APD **SQLSetStmtAttr**与 SQL_ATTR_PARAM_BIND_TYPE*属性*。  
  
 **SQL_DESC_COUNT [全部]**  
 此 SQLSMALLINT 标头字段指定包含数据的最高编号记录的基于 1 的索引。 当驱动程序将设置描述符的数据结构时，它也必须设置 SQL_DESC_COUNT 字段，以显示多少条记录是有意义。 当应用程序分配此数据结构的一个实例时，它没有指定多少条记录保留的空间。 按应用程序上指定的记录的内容，该驱动程序将任何所需的操作，以确保的描述符句柄是指足够大小的数据结构。  
  
 SQL_DESC_COUNT 不是计数 （如果该字段正在 ARD） 绑定的所有数据列或所有参数 （如果该字段正在 APD） 绑定，但最高编号记录数。 如果未绑定的最高编号列或参数，然后会将 SQL_DESC_COUNT 改为下一编号最高的列或参数的数目。 如果某一列或具有大量的参数小于的编号最高的列数是未绑定 (通过调用**SQLBindCol**与*TargetValuePtr*参数设置为 null 指针或**SQLBindParameter**与*ParameterValuePtr*参数设置为 null 指针)，SQL_DESC_COUNT 不会更改。 如果通过数字大于包含数据的最高编号记录来绑定其他列或参数，该驱动程序会自动增加 SQL_DESC_COUNT 字段中的值。 如果所有列都未都绑定通过调用**SQLFreeStmt**使用 SQL_UNBIND 选项中的 ARD 和 IRD 的 SQL_DESC_COUNT 字段设置为 0。 如果**SQLFreeStmt**调用使用 SQL_RESET_PARAMS 选项中的 APD 和 IPD 的 SQL_DESC_COUNT 字段设置为 0。  
  
 SQL_DESC_COUNT 中的值可以设置显式应用程序通过调用**SQLSetDescField**。 如果显式减少 SQL_DESC_COUNT 中的值，有效地删除所有记录号大于 SQL_DESC_COUNT 中的新值。 如果该字段正在 ARD SQL_DESC_COUNT 中的值显式设置为 0，并且当发布绑定的书签列除外的所有数据缓冲区。  
  
 ARD 此字段中的记录计数不包括绑定的书签列。 取消绑定书签列的唯一方法是将 SQL_DESC_DATA_PTR 字段设置为 null 指针。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [实现描述符]**  
 在 IRD，此 SQLULEN\*包含提取后调用的行数的缓冲区的标头字段指向**SQLFetch**或**SQLFetchScroll**，或在大容量操作中受影响的行数通过调用执行**SQLBulkOperations**或**SQLSetPos**，包括错误的行。  
  
 在 IPD，此 SQLUINTEGER * 标头字段指向包含集的已处理，包括错误集的参数数量的缓冲区。 如果这是 null 指针，则将返回没有数。  
  
 SQL_DESC_ROWS_PROCESSED_PTR 无效，只有在调用后返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 后**SQLFetch**或**SQLFetchScroll** （对于 IRD 字段中） 或**SQLExecute**， **SQLExecDirect**，或**SQLParamData** （对于 IPD 字段中）。 如果填充缓冲区中的调用通过指向此字段不返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容未定义的除非它将返回的 SQL_NO_DATA，在其中用例缓冲区中的值设置为 0。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**具有 SQL_ATTR_ROWS_FETCHED_PTR 属性。 此外可以通过调用设置此字段中 APD **SQLSetStmtAttr**具有 SQL_ATTR_PARAMS_PROCESSED_PTR 属性。  
  
 按此字段指向的缓冲区分配了应用程序。 它是由驱动程序设置的延迟的输出缓冲区。 它是默认设置为 null 指针。  
  
## <a name="record-fields"></a>记录字段  
 每个描述符包含包含列数据或动态参数，具体取决于描述符的类型定义的字段的一个或多个记录。 每个记录是单个列或参数的完整定义。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 此只读 SQLINTEGER 记录字段包含 SQL_TRUE 列是否是自动递增列中或 SQL_FALSE 如果列不是自动递增列。 此字段是只读的但基础的自动递增列不一定是只读的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段中包含的基列名称的结果集列。 如果基列名称不存在 （如下所示的是表达式的列的情况下），则此变量包含一个空字符串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基本的表名称的结果集列。 如果基表名称不能定义或不适用，则此变量包含一个空字符串。  
  
 **SQL_DESC_CASE_SENSITIVE [实现描述符]**  
 此只读 SQLINTEGER 记录字段包含 SQL_TRUE，如果列或参数被处理的排序规则和比较或 SQL_FALSE 的区分大小写，如果列均不被视为排序规则和比较的区分大小写，或如果它为非字符列。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段中包含的目录包含的列的基表。 如果列是一个表达式，或者如果列是视图的一部分，则返回值与驱动程序相关。 如果数据源不支持目录或目录不能确定，此变量包含一个空字符串。  
  
 **SQL_DESC_CONCISE_TYPE [全部]**  
 此 SQLSMALLINT 标头字段指定所有数据类型，其中包括日期时间和间隔数据类型的简洁数据类型。  
  
 SQL_DESC_CONCISE_TYPE、 SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段中的值会互相影响。 每个时间的字段之一设置、 其他还必须设置。 可以通过调用设置 SQL_DESC_CONCISE_TYPE **SQLBindCol**或**SQLBindParameter**，或**SQLSetDescField**。 可以通过调用设置 SQL_DESC_TYPE **SQLSetDescField**或**SQLSetDescRec**。  
  
 如果 SQL_DESC_CONCISE_TYPE 设置为简洁数据类型不是间隔或日期时间数据类型，SQL_DESC_TYPE 字段设置为相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为 0。  
  
 如果 SQL_DESC_CONCISE_TYPE 设置为的简洁的日期时间或间隔数据类型，SQL_DESC_TYPE 字段设置为相应的详细类型 （SQL_DATETIME 或 SQL_INTERVAL） 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为适当的子代码。  
  
 **SQL_DESC_DATA_PTR [应用程序描述符和 IPDs]**  
 此 SQLPOINTER 记录字段将指向的变量将包含的参数值 （APDs) 或 （对于 ARDs) 的列值。 此字段是*延迟的字段*。 在设置，但用于在更高版本时由驱动程序检索数据时不使用它。  
  
 如果指定 ARD SQL_DESC_DATA_PTR 字段的列是未绑定*TargetValuePtr*对的调用中的自变量**SQLBindCol**是 null 指针，或如果 SQL_DESC_DATA_PTR 字段中 ARD 设置的调用**SQLSetDescField**或**SQLSetDescRec**到 null 指针。 如果 SQL_DESC_DATA_PTR 字段设置为 null 指针，不会影响其他字段。  
  
 如果调用**SQLFetch**或**SQLFetchScroll** ，填充此字段的指向缓冲区中未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。  
  
 每当设置 APD、 ARD，或 IPD SQL_DESC_DATA_PTR 字段时，驱动程序将检查 SQL_DESC_TYPE 字段中的值包含一个有效的 ODBC C 数据类型或特定于驱动程序的数据类型，并影响的数据类型的其他所有字段都都一致。 提示一致性检查是 IPD SQL_DESC_DATA_PTR 字段的唯一用途。 具体而言，如果应用程序设置为 IPD 和更高版本调用 SQL_DESC_DATA_PTR 字段**SQLGetDescField**上此字段中，则不一定返回它已设置的值。 有关详细信息，请参阅"一致性检查" [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [全部]**  
 SQL_DATETIME 或 SQL_INTERVAL SQL_DESC_TYPE 字段时，此 SQLSMALLINT 记录字段将包含特定的日期时间或间隔数据类型的子代码。 这适用于 SQL 和 C 数据类型。 代码使用"代码"（对于 datetime 类型），替换为"TYPE"或"C_TYPE"或"代码"替换为"间隔"或"C_INTERVAL"（对于间隔类型） 包含的数据类型名称。  
  
 如果 SQL_DESC_TYPE 和应用程序描述符中的 SQL_DESC_CONCISE_TYPE 设置为 SQL_C_DEFAULT 和描述符不是与语句句柄关联，SQL_DESC_DATETIME_INTERVAL_CODE 的内容将不确定。  
  
 此字段可以为下表中列出的 datetime 数据类型设置。  
  
|日期时间类型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP / SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 此字段可以为下表中列出的间隔数据类型设置。  
  
|间隔类型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE / SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
QL_INTERVAL_HOUR_TO_MINUTE / SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE / SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
QL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 有关数据间隔，则此字段的详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [全部]**  
 此 SQLINTEGER 记录字段包含前导精度，如果 SQL_DESC_TYPE 字段为 SQL_INTERVAL 的间隔。 当 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为间隔的数据类型时，此字段设置为前导精度的默认时间间隔。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 此只读 SQLINTEGER 记录字段包含的最大显示列的数据所需的字符数。  
  
 **SQL_DESC_FIXED_PREC_SCALE [实现描述符]**  
 此只读 SQLSMALLINT 记录字段设置为 SQL_TRUE 如果列是精确数值列，并且具有固定的精度和非零的小数位数，或到 SQL_FALSE 如果该列不是具有固定的精度和小数位数的精确数值列。  
  
 **SQL_DESC_INDICATOR_PTR [应用程序描述符]**  
 在 ARDs，此 SQLLEN * 记录字段指向指示器变量。 如果列值为 NULL，则此变量包含 SQL_NULL_DATA。 为 APDs，指示器变量设置为 SQL_NULL_DATA 指定 NULL 动态自变量。 否则，变量进行零 （除非 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 中的值是相同的指针）。  
  
 如果在 ARD SQL_DESC_INDICATOR_PTR 字段为 null 指针，已阻止驱动程序返回有关该列是否是 NULL 的信息。 如果该列为 NULL 且 SQL_DESC_INDICATOR_PTR 为 null 指针，SQLSTATE 22002 （指示器变量需要但未提供） 则返回时的驱动程序尝试在调用后填充缓冲区**SQLFetch**或**SQLFetchScroll**。 如果调用**SQLFetch**或**SQLFetchScroll**未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。  
  
 SQL_DESC_INDICATOR_PTR 字段确定是否设置了指向 SQL_DESC_OCTET_LENGTH_PTR 的字段。 如果列的数据值为 NULL，则该驱动程序会将指示器变量设置为 SQL_NULL_DATA。 指向 SQL_DESC_OCTET_LENGTH_PTR 字段然后未设置。 如果在提取过程未遇到 NULL 值，通过 SQL_DESC_INDICATOR_PTR 指向的缓冲区设置为零，并且通过 SQL_DESC_OCTET_LENGTH_PTR 指向的缓冲区设置为数据的长度。  
  
 如果在 APD SQL_DESC_INDICATOR_PTR 字段为 null 指针，该应用程序无法使用此描述符记录指定 NULL 参数。  
  
 此字段是*延迟的字段*： 在它设置使用的却是在更高版本时由驱动程序 （为 ARDs) 指明可为 null，或者想要确定可为 null （对于 APDs) 时不使用它。  
  
 **SQL_DESC_LABEL [IRDs]**  
 此只读 SQLCHAR * 记录字段中包含的列标签或标题。 如果列不具有标签，则此变量包含列名称。 如果列是未命名参数和未标记，则此变量包含一个空字符串。  
  
 **SQL_DESC_LENGTH [全部]**  
 此 SQLULEN 记录字段为以字符为单位的字符字符串的最大值或实际长度，或者以字节为单位的 binary 数据类型。 它是固定长度的数据类型的最大长度或可变长度数据类型的实际长度。 其值始终不包括结尾的字符串的 null 终止字符。 对于其类型是 SQL_TYPE_DATE、 SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP，或 SQL interval 数据类型之一的值，此字段以字符为字符字符串表示形式的日期时间或间隔值单位的长度。  
  
 此字段中的值可能不同于"length"作为 ODBC 2 中定义的值*.x*。 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 此只读 SQLCHAR * 记录字段中包含的字符或驱动程序识别为此数据类型的文本的前缀的字符。 此变量包含的文本的前缀不适用的数据类型的空字符串。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 此只读 SQLCHAR * 记录字段中包含的字符或字符，则驱动程序识别为此数据类型的文本的后缀。 此变量包含的文本的后缀不是适用的数据类型的空字符串。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR * 记录字段包含的数据类型可能不同于数据类型的正则名称的任何本地化 （本机语言） 名称。 如果没有任何本地化的名称，则返回空字符串。 此字段为仅用于显示目的。  
  
 **SQL_DESC_NAME [实现描述符]**  
 此 SQLCHAR * 行描述符中的记录字段包含的列别名，如果该属性适用。 如果列别名不适用，则返回的列名称。 在任一情况下，该驱动程序将 SQL_DESC_UNNAMED 字段设置为 SQL_NAMED 时它设置为 SQL_DESC_NAME 字段。 如果没有任何列名称或列别名，该驱动程序将在 SQL_DESC_NAME 字段返回一个空字符串，并将 SQL_DESC_UNNAMED 字段设置为 SQL_UNNAMED。  
  
 应用程序可以将 IPD SQL_DESC_NAME 字段设置为参数名称或别名，以便按名称指定存储的过程参数。 (有关详细信息，请参阅[按名称 （名为参数） 的绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。)IRD SQL_DESC_NAME 字段是只读的字段;SQLSTATE HY091 将返回 （描述符字段标识符无效），如果应用程序尝试将其设置。  
  
 在 IPDs，此字段是未定义，如果驱动程序不支持命名的参数。 如果驱动程序支持命名的参数，并且能够描述参数，则此字段中返回参数名称。  
  
 **SQL_DESC_NULLABLE [实现描述符]**  
 IRDs，在此只读 SQLSMALLINT 记录字段是 SQL_NULLABLE，如果列可以具有 NULL 值，SQL_NO_NULLS 如果列不具有 NULL 值或 SQL_NULLABLE_UNKNOWN，如果它不已知的列是否接受 NULL 值。 此字段适用于结果集列，不基列。  
  
 在 IPDs，此字段始终设置为 SQL_NULLABLE 因为动态参数都始终可以为 null，并且不能通过应用程序设置。  
  
 **SQL_DESC_NUM_PREC_RADIX [全部]**  
 此 SQLINTEGER 字段包含值为 2 如果 SQL_DESC_TYPE 字段中的数据类型是近似数值数据类型，因为 SQL_DESC_PRECISION 字段包含的位数。 此字段包含值为 10 如果 SQL_DESC_TYPE 字段中的数据类型是精确数值数据类型，因为 SQL_DESC_PRECISION 字段包含的十进制位数。 此字段设置为 0 表示所有非数字数据类型。  
  
 **SQL_DESC_OCTET_LENGTH [全部]**  
 此 SQLLEN 记录字段包含的长度，以字节为单位，字符字符串或二进制数据类型。 对于固定长度字符或二进制类型，这是以字节为单位的实际长度。 对于长度可变的字符或二进制类型，这是以字节为单位的最大长度。 此值始终排除实现描述符的 null 终止字符的空间，并始终包括在应用程序描述符的 null 终止字符的空间。 对于应用程序数据，此字段包含缓冲区的大小。 对于 APDs，此字段定义仅为输出或输入/输出参数。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [应用程序描述符]**  
 此 SQLLEN * 记录字段指向将包含以字节为单位的动态参数 （参数描述符） 或 （对于行描述符） 绑定的列的值的总长度的变量。  
  
 对于 APD，此值将忽略除字符串和二进制; 以外的所有自变量如果此字段将指向 sql_nts 以，动态自变量必须是以 null 结尾。 若要指示绑定的参数将为数据在执行参数，应用程序此字段中设置相应的记录的 APD 为变量的请在执行时，将包含值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果. 如果有多个此类字段，为唯一标识的参数的值设置 SQL_DESC_DATA_PTR，可以以帮助确定哪些参数所请求的应用程序。  
  
 如果 ARD OCTET_LENGTH_PTR 字段为 null 指针，该驱动程序不返回列的长度信息。 如果 APD SQL_DESC_OCTET_LENGTH_PTR 字段为 null 指针，该驱动程序假定字符串和二进制值是以 null 结尾。 （二进制值不应为以 null 结尾但应为长度以避免被截断。）  
  
 如果调用**SQLFetch**或**SQLFetchScroll** ，填充此字段的指向缓冲区中未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。 此字段是*延迟的字段*。 在它设置使用的却是在更高版本时由驱动程序可确定或指示的数据的八位字节长度的时间不使用它。  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 此 SQLSMALLINT 记录字段设置为 SQL_PARAM_INPUT 输入参数，为一个输入/输出参数，为输出参数，SQL_PARAM_INPUT_OUTPUT_STREAM 输入/输出流参数或 SQL_ SQL_PARAM_OUTPUT SQL_PARAM_INPUT_OUTPUT有关流式处理的输出参数的 PARAM_OUTPUT_STREAM。 它是默认设置为 SQL_PARAM_INPUT。  
  
 为 IPD 字段设置为 SQL_PARAM_INPUT 默认情况下如果 IPD 不会自动填充 （SQL_ATTR_ENABLE_AUTO_IPD 语句属性是 SQL_FALSE） 驱动程序。 应用程序应在不是输入的参数的参数 IPD 设置此字段。  
  
 **SQL_DESC_PRECISION [全部]**  
 此 SQLSMALLINT 记录字段中包含的精确数值类型，尾数近似的数字类型，（二进制精度） 中的比特数或 SQL_TYPE_TIME，SQL_TYPE 秒的小数部分组件中的数字的数字的位数_TIMESTAMP 或 SQL_INTERVAL_SECOND 数据类型。 此字段为对于所有其他数据类型未定义。  
  
 此字段中的值可能不同于"精度"作为 ODBC 2 中定义的值*.x*。 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [实现描述符]**  
 此 SQLSMALLINTrecord 字段指示是否一列自动修改由 DBMS 行进行更新 （例如，类型为"timestamp"SQL Server 中的列） 时。 此记录字段的值是否则设置到 SQL_TRUE 如果列是行版本控制列，和 SQL_FALSE。 此列属性是类似于调用**SQLSpecialColumns**与 IdentifierType 的 SQL_ROWVER，以确定是否自动更新的列。  
  
 **SQL_DESC_SCALE [全部]**  
 此 SQLSMALLINT 记录字段包含 decimal 和 numeric 数据类型的定义小数位数。 该字段为对于所有其他数据类型未定义。  
  
 此字段中的值可能不同于"规模"ODBC 2 中定义的值*.x*。 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基本包含的列的表的架构名称。 如果列是一个表达式，或者如果列是视图的一部分，则返回值与驱动程序相关。 如果数据源不支持架构或架构名称不能确定，此变量包含一个空字符串。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   如果列不能在 SQL_PRED_NONE**其中**子句。 (这是与 ODBC 2 中的 SQL_UNSEARCHABLE 值相同*.x*。)  
  
-   SQL_PRED_CHAR 如果列可在**其中**但仅具有子句**如**谓词。 (这是与 ODBC 2 中的 SQL_LIKE_ONLY 值相同*.x*。)  
  
-   如果列可在 SQL_PRED_BASIC**其中**子句与除之外的所有比较运算符**如**。 (这是与 ODBC 2 中的 SQL_EXCEPT_LIKE 值相同*.x*。)  
  
-   如果列可在 SQL_PRED_SEARCHABLE**其中**子句的任何比较运算符。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基表包含此列的名称。 如果列是一个表达式，或者如果列是视图的一部分，则返回值与驱动程序相关。  
  
 **SQL_DESC_TYPE [全部]**  
 此 SQLSMALLINT 记录字段指定除日期时间和间隔数据类型之外的所有数据类型的简洁 SQL 或 C 数据类型。 对于日期时间和间隔数据类型，此字段指定详细的数据类型，即 SQL_DATETIME 或 SQL_INTERVAL。  
  
 此字段包含 SQL_DATETIME 或 SQL_INTERVAL，每当 SQL_DESC_DATETIME_INTERVAL_CODE 字段必须包含简洁的类型的相应子代码。 对于 datetime 数据类型，SQL_DESC_TYPE 包含 SQL_DATETIME，和 SQL_DESC_DATETIME_INTERVAL_CODE 字段包含特定的 datetime 数据类型的子代码。 对于间隔数据类型，SQL_DESC_TYPE 包含 SQL_INTERVAL 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段包含特定的时间间隔的数据类型的子代码。  
  
 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 字段中的值会互相影响。 每个时间的字段之一设置、 其他还必须设置。 可以通过调用设置 SQL_DESC_TYPE **SQLSetDescField**或**SQLSetDescRec**。 可以通过调用设置 SQL_DESC_CONCISE_TYPE **SQLBindCol**或**SQLBindParameter**，或**SQLSetDescField**。  
  
 如果 SQL_DESC_TYPE 设置为简洁数据类型不是间隔或日期时间数据类型，SQL_DESC_CONCISE_TYPE 字段设置为相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为 0。  
  
 如果 SQL_DESC_TYPE 设置为详细的日期时间或间隔数据类型 （SQL_DATETIME 或 SQL_INTERVAL） 并且 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为适当的子代码，SQL_DESC_CONCISE 类型字段设置为相应的简洁类型。 尝试将 SQL_DESC_TYPE 设置为一种简洁的日期时间或间隔类型将返回 SQLSTATE HY021 （不一致的描述符信息）。  
  
 当通过调用设置 SQL_DESC_TYPE 字段**SQLBindCol**， **SQLBindParameter**，或**SQLSetDescField**，以下字段设置为下面的默认值，下表中所示。 同一条记录的其余字段的值是不确定的。  
  
|SQL_DESC_TYPE 的值|其他字段隐式设置|  
|------------------------------|---------------------------------|  
|SQL_CHAR、 SQL_VARCHAR SQL_C_CHAR SQL_C_VARCHAR|SQL_DESC_LENGTH 设置为 1。 SQL_DESC_PRECISION 设置为 0。|  
|SQL_DATETIME|当 SQL_DESC_DATETIME_INTERVAL_CODE 设置为 SQL_CODE_DATE 或 SQL_CODE_TIME 时，SQL_DESC_PRECISION 设置为 0。 当它设置为 SQL_DESC_TIMESTAMP 时，SQL_DESC_PRECISION 设置为 6。|  
|SQL_DECIMAL，SQL_NUMERIC，SQL_C_NUMERIC|SQL_DESC_SCALE 设置为 0。 SQL_DESC_PRECISION 设置为各自的数据类型的实现定义精度。<br /><br /> 请参阅[到 c： 数值 SQL](../../../odbc/reference/appendixes/sql-to-c-numeric.md)有关如何手动将绑定 SQL_C_NUMERIC 值的信息。|  
|SQL_FLOAT SQL_C_FLOAT|SQL_FLOAT SQL_DESC_PRECISION 设置为实现定义的默认精度。|  
|SQL_INTERVAL|当 SQL_DESC_DATETIME_INTERVAL_CODE 设置为间隔数据类型时，SQL_DESC_DATETIME_INTERVAL_PRECISION 设置为 2 （默认间隔前导精度）。 当间隔的秒数部分时，SQL_DESC_PRECISION 设置为 6 （默认间隔秒精度）。|  
  
 在应用程序调用**SQLSetDescField**以设置域描述符，而不是调用**SQLSetDescRec**，应用程序必须首先声明的数据类型。 时，将隐式设置上表所示的其他字段。 如果任何值隐式集是不可接受，然后，应用程序可以调用**SQLSetDescField**或**SQLSetDescRec**显式设置不可接受的值。  
  
 **SQL_DESC_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR * 记录字段中包含的数据源而定类型名称 （例如，"CHAR"、"VARCHAR"等）。 如果未知的数据类型名称，此变量包含一个空字符串。  
  
 **SQL_DESC_UNNAMED [实现描述符]**  
 它集 SQL_DESC_NAME 字段时，将由驱动程序添加到 SQL_NAMED 或 SQL_UNNAMED 设置行描述符中的此 SQLSMALLINT 记录字段。 如果 SQL_DESC_NAME 字段包含的列别名或列别名不适用，驱动程序将 SQL_NAMED 设置 SQL_DESC_UNNAMED 字段。 如果应用程序将 IPD SQL_DESC_NAME 字段设置为参数名称或别名，该驱动程序将设置到 SQL_NAMED IPD SQL_DESC_UNNAMED 字段。 如果没有任何列名称或列别名，该驱动程序会将 SQL_DESC_UNNAMED 字段设置为 SQL_UNNAMED。  
  
 应用程序可以设置为 SQL_UNNAMED IPD SQL_DESC_UNNAMED 字段。 驱动程序返回 SQLSTATE HY091 （描述符字段标识符无效） 如果应用程序尝试将 IPD SQL_DESC_UNNAMED 字段设置为 SQL_NAMED。 IRD SQL_DESC_UNNAMED 字段是只读的;SQLSTATE HY091 将返回 （描述符字段标识符无效），如果应用程序尝试将其设置。  
  
 **SQL_DESC_UNSIGNED [实现描述符]**  
 此只读 SQLSMALLINT 记录字段设置为 SQL_TRUE 如果列类型是无符号或非数字或 SQL_FALSE 中，如果列类型进行签名。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   如果结果集列的 SQL_ATTR_READ_ONLY 是只读的。  
  
-   如果结果集列的 SQL_ATTR_WRITE 为读写。  
  
-   SQL_ATTR_READWRITE_UNKNOWN 如果它不已知的结果是否将列设置可更新。  
  
 SQL_DESC_UPDATABLE 介绍结果集中的列，不基表中的列的可更新性。 此结果集列所基于的基表中的列 updatability 可能不同于此字段中的值。 某列是否可更新可以基于数据类型、 用户权限和结果集本身的定义。 如果不清楚是否可更新列，则将返回 SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性检查  
 一致性检查时，将执行由驱动程序会自动为 ARD、 APD，或 IPD SQL_DESC_DATA_PTR 字段值将传递的应用程序。 如果其中任何一个字段是不一致，其他字段， **SQLSetDescField**将返回 SQLSTATE HY021 （不一致的描述符信息）。 有关详细信息，请参阅"一致性检查" [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|将参数绑定|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)

