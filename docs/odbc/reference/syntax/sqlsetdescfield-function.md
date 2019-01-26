---
title: SQLSetDescField 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce80e7b9c6e8cfcf15c0810986c1a34e8d881ade
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044354"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函数

**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLSetDescField**设置描述符记录的单个字段的值。  
  
## <a name="syntax"></a>语法  
  
```cpp  
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
 [输入]指示包含该应用程序查找要设置的字段的描述符记录。 描述符记录编号介于 0，使用 0 表示的书签记录的记录号。 *RecNumber*标头字段，将忽略参数。  
  
 *FieldIdentifier*  
 [输入]表示其值将设置的描述符字段。 有关详细信息，请参阅"*FieldIdentifier*参数"中的"注释"部分。  
  
 *ValuePtr*  
 [输入]指向包含描述符信息，或者一个整数值的缓冲区的指针。 数据类型取决于的值*FieldIdentifier*。 如果*ValuePtr*是一个整数值，可能会被视为 8 个字节 (SQLLEN)、 4 个字节 (SQLINTEGER) 或 2 个字节 (SQLSMALLINT)，具体取决于值*FieldIdentifier*参数。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度 **ValuePtr*。 对于字符串数据，此参数应包含在字符串中的字节数。  
  
 如果*FieldIdentifier*是一个 ODBC 定义的字段和*ValuePtr*是一个整数*BufferLength*将被忽略。  
  
 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指示字段到驱动程序管理器的性质*BufferLength*参数。 *BufferLength*可以具有以下值：  
  
-   如果*ValuePtr*是一个指向一个字符串，然后*BufferLength*是 sql_nts; 的字符串的长度。  
  
-   如果*ValuePtr*是一个指向二进制缓冲区，则 SQL_LEN_BINARY_ATTR 将结果放置于该应用程序 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*ValuePtr*指向的字符串或二进制字符串以外的值，即*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含一个固定长度值，则*BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetDescField**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DESC 和一个*处理*的*DescriptorHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetDescField** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持在指定的值 *\*ValuePtr* (如果*ValuePtr*是指针) 或中的值*ValuePtr* (如果*ValuePtr*是一个整数值)，或 *\*ValuePtr*无效由于实现运行情况，因此驱动程序替换一个相近的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|描述符索引无效|*FieldIdentifier*自变量是一个记录字段中， *RecNumber*参数为 0，并且*DescriptorHandle*参数引用的 IPD 的句柄。<br /><br /> *RecNumber*参数为小于 0，并且*DescriptorHandle* ARD 或 APD 引用参数。<br /><br /> *RecNumber*参数为大于最大号的列或参数的数据源可以支持，并*DescriptorHandle* APD 或 ARD 引用参数。<br /><br /> （数据挖掘） *FieldIdentifier*参数为 SQL_DESC_COUNT，并 *\*ValuePtr*参数为小于 0。<br /><br /> *RecNumber*参数为等于 0，并且*DescriptorHandle*隐式分配 APD 引用参数。 （是显式分配应用程序描述符，不会发生此错误因为不知道是显式分配应用程序描述符是 APD 或直到 ARD 执行时间。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22001|字符串数据，右截断|*FieldIdentifier*参数为 SQL_DESC_NAME，并*BufferLength*参数为大于 SQL_MAX_IDENTIFIER_LEN 的值。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） *DescriptorHandle*与关联*StatementHandle*其中 （而不此是） 的异步执行函数调用和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*与其*DescriptorHandle*已关联，并返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此异步函数仍在执行时**SQLSetDescField**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*DescriptorHandle* ，并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY016|无法修改实现行描述符|*DescriptorHandle*参数为与 IRD 相关联并*FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR 参数不是。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段未形成有效的 ODBC SQL 类型或有效的特定于驱动程序的 SQL 类型 （适用于 Ipd) 或有效的 ODBC C 类型 （适用于 Apd 或 ARDs）。<br /><br /> 一致性检查期间检查的描述符信息不是一致的。 (请参阅"一致性检查"中的**SQLSetDescRec**。)|  
|HY090|字符串或缓冲区长度无效|（数据挖掘）  *\*ValuePtr*是一个字符串，并*BufferLength*是小于零，但不是等于 SQL_NTS。<br /><br /> (DM) 驱动程序是 ODBC 2 *.x*驱动程序，该描述符是 ARD *ColumnNumber*参数设置为 0，并为该参数指定的值*BufferLength*是不等于 4。|  
|HY091|描述符字段标识符无效|为指定的值*FieldIdentifier*参数不是 ODBC 定义的字段，不是实现定义的值。<br /><br /> *FieldIdentifier*参数的无效*DescriptorHandle*参数。<br /><br /> *FieldIdentifier*自变量是只读的、 ODBC 定义的字段。|  
|HY092|属性/选项标识符无效|中的值 *\*ValuePtr*对无效*FieldIdentifier*参数。<br /><br /> *FieldIdentifier*参数为 SQL_DESC_UNNAMED，并*ValuePtr*已 SQL_NAMED。|  
|HY105|无效的参数类型|(DM) 指定为 SQL_DESC_PARAMETER_TYPE 字段的值无效。 (有关详细信息，请参阅"*InputOutputType*自变量"部分中**SQLBindParameter**。)|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetDescField**设置一次一个的任何描述符字段。 调用一次**SQLSetDescField**单一描述符中设置的单个字段。 此函数可以调用以在任何描述符类型中设置的任何字段，提供可设置该字段。 （请参阅本节后面的表。）  
  
> [!NOTE]  
>  如果调用**SQLSetDescField**失败，标识的描述符记录的内容*RecNumber*自变量是不确定。  
  
 可以调用其他函数来设置多个描述符字段，该函数一次调用。 **SQLSetDescRec**函数设置了不同的字段的数据类型和缓冲区绑定到列或参数 （SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_PRECISION、 SQL_ 的影响DESC_SCALE、 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 字段）。 **SQLBindCol**或**SQLBindParameter**可用于使绑定的列或参数的完整规范。 这些函数将设置一组特定的描述符字段使用一个函数调用。  
  
 **SQLSetDescField**可以调用以通过将某一偏移量添加到绑定指针 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 或 SQL_DESC_OCTET_LENGTH_PTR） 来更改绑定缓冲区。 这会更改而无需调用绑定缓冲区**SQLBindCol**或**SQLBindParameter**，让应用程序，而无需更改其他字段，例如 SQL_DESC_DATA_ 更改 SQL_DESC_DATA_PTR类型。  
  
 如果应用程序调用**SQLSetDescField**若要设置除 SQL_DESC_COUNT 以外的任何字段或延迟的字段 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 或 SQL_DESC_INDICATOR_PTR，记录解除绑定。  
  
 描述符标头字段将通过调用**SQLSetDescField**具有相应*FieldIdentifier*。 许多标头字段也是语句属性，因此还可以通过调用设置它们**SQLSetStmtAttr**。 这允许应用程序无需首先获取描述符句柄设置描述符字段。 当**SQLSetDescField**调用来设置的标头字段， *RecNumber*忽略参数。  
  
 一个*RecNumber*的 0 用于设置书签字段。  
  
> [!NOTE]  
>  语句属性 SQL_ATTR_USE_BOOKMARKS 应始终设置，然后再调**SQLSetDescField**设置书签字段。 尽管这不是必需的强烈建议。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>设置描述符字段的序列  
 当通过调用设置描述符字段**SQLSetDescField**，应用程序必须遵循特定的顺序：  
  
1.  应用程序必须先设置的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 或 SQL_DESC_DATETIME_INTERVAL_CODE 字段。  
  
2.  已设置了一个这些字段后，应用程序可以设置数据类型的属性和驱动程序的数据类型的适当的默认值设置数据类型属性字段。 自动将使用默认值的类型特性字段可确保该描述符是始终可供使用后一种数据类型指定应用程序。 如果应用程序显式设置数据类型的属性，它重写默认属性。  
  
3.  已设置了一个在步骤 1 中所列的字段，并且数据类型属性已设置后，应用程序可以设置 SQL_DESC_DATA_PTR。 这会提示描述符字段一致性的检查。 如果应用程序设置 SQL_DESC_DATA_PTR 字段后更改的数据类型或属性，该驱动程序设置 SQL_DESC_DATA_PTR 到 null 指针时，取消绑定该记录。 这会强制应用程序可用的描述符记录之前在序列中，完成适当的步骤。  
  
## <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化  
 当分配的描述符时，描述符中的字段可以初始化为默认值、 没有默认值，初始化或是未定义的类型的描述符。 以下各表指示每种类型的描述符，使用"D"，该值指示该字段默认值，初始化和"ND"，该值指示该字段没有默认值初始化每个字段的初始化。 如果显示一个数字，该字段的默认值是该数字。 这些表还指示字段是否为读/写 (R/W) 或只读的 (R)。  
  
 IRD 字段只在已准备或执行该语句并已填充了 IRD，已分配语句句柄或描述符时不具有默认值。 直到已填充 IRD，任何尝试访问的 IRD 字段将返回错误。  
  
 某些描述符字段定义为一个或多个，但不是全部的描述符类型 （ARDs 和 IRDs，和 Apd 和 Ipd）。 未定义类型的描述符字段时，不需要任何使用该描述符的函数。  
  
 可以通过访问的字段**SQLGetDescField**一定不能通过设置**SQLSetDescField**。 可以通过设置的字段**SQLSetDescField**下表中列出。  
  
 下表概述了标头字段的初始化。  
  
|标头字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD:R APD:R IRD:R IPD:R|ARD:有关 SQL_DESC_ALLOC_AUTO 隐式或 SQL_DESC_ALLOC_USER 为显式<br /><br /> APD:有关 SQL_DESC_ALLOC_AUTO 隐式或 SQL_DESC_ALLOC_USER 为显式<br /><br /> IRD:SQL_DESC_ALLOC_AUTO<br /><br /> IPD:SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN 生成|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: [1] APD: [1] IRD:未使用的 IPD:未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|ARD:R/W APD:R/W IRD:R/W IPD:R/W|ARD:Ptr APD，则为 null:Ptr IRD，则为 null:Ptr IPD，则为 null:Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:Ptr APD，则为 null:Ptr IRD，则为 null:未使用的 IPD:未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:SQL_BIND_BY_COLUMN<br /><br /> APD:SQL_BIND_BY_COLUMN<br /><br /> IRD:未使用<br /><br /> IPD:未使用|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:0 APD:0 IRD:D IPD:0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|ARD:未使用的 APD:未使用的 IRD:R/W IPD:R/W|ARD:未使用的 APD:未使用的 IRD:Ptr IPD，则为 null:Null ptr|  
  
 [1] 字段只有在驱动程序会自动填充 IPD 时定义。 如果不是，不进行定义。 如果应用程序尝试设置这些字段，SQLSTATE HY091 将返回 （无效的描述符字段标识符）。  
  
 记录的字段初始化为下表中所示。  
  
|记录字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:SQL_C_ 默认 APD:SQL_C_ 默认 IRD:D IPD:ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:Ptr APD，则为 null:Ptr IRD，则为 null:未使用的 IPD:未使用 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_DISPLAY_SIZE|为 SQLLEN|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_INDICATOR_PTR|为 SQLLEN *|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:Ptr APD，则为 null:Ptr IRD，则为 null:未使用的 IPD:未使用|  
|SQL_DESC_LABEL|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LENGTH|SQLULEN 生成|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_OCTET_LENGTH|为 SQLLEN|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_OCTET_LENGTH_PTR|为 SQLLEN *|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:Ptr APD，则为 null:Ptr IRD，则为 null:未使用的 IPD:未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:未使用的 IPD:R/W|ARD:未使用的 APD:未使用的 IRD:未使用的 IPD:D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD:R<br /><br /> IPD:R|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD:ND<br /><br /> IPD:ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD:SQL_C_DEFAULT APD:SQL_C_DEFAULT IRD:D IPD:ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R/W|ARD:ND APD:ND IRD:D IPD:ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
  
 [1] 字段只有在驱动程序会自动填充 IPD 时定义。 如果不是，不进行定义。 如果应用程序尝试设置这些字段，SQLSTATE HY091 将返回 （无效的描述符字段标识符）。  
  
 [可以设置 2] 上，在 IPD 中的 SQL_DESC_DATA_PTR 字段以便强制执行一致性检查。 中的后续调用**SQLGetDescField**或**SQLGetDescRec**，驱动程序不需要返回 SQL_DESC_DATA_PTR 已设置为的值。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 参数  
 *FieldIdentifier*参数指示要设置的描述符字段。 描述符包含*描述符标头*下一步部分中，"标头字段，"和零个或多中所述的标头字段组成*描述符记录*包含的记录字段"标头字段"部分的一节中所述。  
  
## <a name="header-fields"></a>标头字段  
 每个描述符具有标头包含以下字段：  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 此只读 SQLSMALLINT 标头字段指定驱动程序或显式由应用程序是否会自动分配的描述符。 应用程序可以获取，但不是修改此字段。 如果驱动程序自动分配的描述符，字段由驱动程序设置为 SQL_DESC_ALLOC_AUTO 中。 如果描述符已显式分配应用程序，它是由驱动程序设置 SQL_DESC_ALLOC_USER。  
  
 **SQL_DESC_ARRAY_SIZE [Application descriptors]**  
 ARDs，在此 sqlulen 生成标头字段指定行集中的行的数。 这是通过调用返回的行数**SQLFetch**或**SQLFetchScroll**或通过调用要操作**SQLBulkOperations**或**SQLSetPos**.  
  
 Apd，在此 sqlulen 生成标头字段指定的每个参数的值的数目。  
  
 此字段的默认值为 1。 如果 SQL_DESC_ARRAY_SIZE 大于 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 或 ARD 指向数组。 每个数组的基数是此字段的值相等。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**使用 SQL_ATTR_ROW_ARRAY_SIZE 属性。 APD 中的此字段还可以设置通过调用**SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 属性。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 对于每个描述符类型，此 SQLUSMALLINT * 标头字段指向数组的 SQLUSMALLINT 值。 这些列阵，如下所示命名： 行状态数组 (IRD) 中，参数状态数组 (IPD)、 行操作数组 (ARD) 和参数操作数组 (APD)。  
  
 在 IRD 中为此标头字段将指向调用后包含状态的值的行状态数组**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或者**SQLSetPos**。 数组不包含任意多个元素的行集中的行一样。 应用程序必须分配 SQLUSMALLINTs 一个数组，并将此字段以指向该数组。 默认情况下，该字段设置为 null 指针。 该驱动程序将填充数组-除非 SQL_DESC_ARRAY_STATUS_PTR 字段设置为 null 指针，在这种情况下生成无状态的值并不填充该数组。  
  
> [!CAUTION]  
>  如果应用程序将设置指向 IRD SQL_DESC_ARRAY_STATUS_PTR 字段的行状态数组的元素，驱动程序行为不确定。  
  
 通过调用最初填充数组**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或者**SQLSetPos**。 如果调用未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，对指向此字段的数组的内容未定义。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_SUCCESS:已成功提取行，并且自上次提取以来未发生更改。  
  
-   SQL_ROW_SUCCESS_WITH_INFO:已成功提取行，并且自上次提取以来未发生更改。 但是，有关行返回一条警告。  
  
-   SQL_ROW_ERROR:提取行时出错。  
  
-   SQL_ROW_UPDATED:行已成功提取和上次提取后进行了更新。 如果再次提取行时，其状态为 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED:已删除行，因为它上次提取。  
  
-   SQL_ROW_ADDED:通过插入行**SQLBulkOperations**。 如果再次提取行时，其状态为 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW:行集重叠的结果集的末尾并不返回任何行时，对应于此元素的行状态数组。  
  
 在 IRD 中的此字段还可以设置通过调用**SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR 属性。  
  
 只有在已返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 后 IRD SQL_DESC_ARRAY_STATUS_PTR 字段有效。 如果返回代码不是其中之一，通过 SQL_DESC_ROWS_PROCESSED_PTR 指向的位置未定义。  
  
 在 IPD，此标头字段将指向包含的每组参数值对的调用后的状态信息的参数状态数组**SQLExecute**或**SQLExecDirect**。 如果在调用**SQLExecute**或**SQLExecDirect**未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，对指向此字段的数组的内容是不确定。 应用程序必须分配 SQLUSMALLINTs 一个数组，并将此字段以指向该数组。 该驱动程序将填充数组-除非 SQL_DESC_ARRAY_STATUS_PTR 字段设置为 null 指针，在这种情况下生成无状态的值并不填充该数组。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_SUCCESS:此参数集的成功执行 SQL 语句。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO:参数; 这一组已成功执行 SQL 语句但是，诊断数据结构中提供了警告信息。  
  
-   SQL_PARAM_ERROR:在处理此套参数出错。 诊断数据结构中提供了其他错误的信息。  
  
-   SQL_PARAM_UNUSED:此参数集处于未使用，可能是因为，一些以前的参数集导致中止将来进行处理，出现错误，或因为 SQL_PARAM_IGNORE 设置该集的 SQL_DESC_ARRAY_STATUS_PTR 字段指定数组中的参数APD 中。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE:诊断信息不可用。 此示例是信息的驱动程序会参数的数组将作为一个整体化单元，因此不会生成此级别的错误。  
  
 此外可以通过调用设置此字段在 IPD **SQLSetStmtAttr**使用 SQL_ATTR_PARAM_STATUS_PTR 属性。  
  
 ARD，在此标头字段将指向应用程序以指示此行是否忽略可以设置的值的行操作数组**SQLSetPos**操作。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_PROCEED:使用在大容量操作中包括的行**SQLSetPos**。 （此设置不保证该操作会在行上发生。 如果行有状态 SQL_ROW_ERROR IRD 行状态数组中的，该驱动程序可能不能在行中执行该操作。）  
  
-   SQL_ROW_IGNORE:行不会进行大容量操作使用**SQLSetPos**。  
  
 如果不设置了数组的任何元素，在大容量操作中包含的所有行。 如果 ARD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为 null 指针，所有的行包括在大容量操作;解释与相同时指针指向有效的数组和数组的所有元素都已 SQL_ROW_PROCEED。 如果数组中的元素设置为 SQL_ROW_IGNORE，已忽略行的行状态数组中的值不会更改。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr** SQL_ATTR_ROW_OPERATION_PTR 属性。  
  
 APD 中此标头字段将指向参数操作数组的值可以设置的应用程序，以指示参数的此集是否为何时忽略**SQLExecute**或**SQLExecDirect**调用。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_PROCEED:中包含的参数集**SQLExecute**或**SQLExecDirect**调用。  
  
-   SQL_PARAM_IGNORE:参数集不会进行**SQLExecute**或**SQLExecDirect**调用。  
  
 如果不设置了数组的任何元素，则在使用的参数数组中的所有集**SQLExecute**或**SQLExecDirect**调用。 APD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为 null 指针，如果使用不同的参数的所有集;解释与相同时指针指向有效的数组和数组的所有元素都已 SQL_PARAM_PROCEED。  
  
 APD 中的此字段还可以设置通过调用**SQLSetStmtAttr** SQL_ATTR_PARAM_OPERATION_PTR 属性。  
  
 **SQL_DESC_BIND_OFFSET_PTR [Application descriptors]**  
 此为 SQLLEN * 标头字段指向绑定偏移量。 默认情况下，它是设置为 null 指针。 如果此字段不是 null 指针，该驱动程序取消引用指针，并将取消引用的值添加到每个延迟的描述符记录 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 中有一个非 null 值的字段在提取时间，并使用新指针值绑定时。  
  
 绑定偏移量会始终直接添加到中的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段的值。 如果偏移量更改为不同的值，新值是仍直接添加到每个描述符字段中的值。 新的偏移量不添加到字段值再加上任何早期的偏移量。  
  
 此字段才*延迟的字段*:不在时设置，但在更高版本时使用驱动程序需要确定的数据缓冲区的地址时使用。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr** SQL_ATTR_ROW_BIND_OFFSET_PTR 属性。 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr** SQL_ATTR_PARAM_BIND_OFFSET_PTR 属性。  
  
 有关详细信息，请参阅中的按行绑定的描述[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)并[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 **SQL_DESC_BIND_TYPE [Application descriptors]**  
 此 SQLUINTEGER 标头字段将设置要使用绑定列或参数的绑定方向。  
  
 在 ARDs，此字段指定绑定方向时**SQLFetchScroll**或**SQLFetch**相关联的语句句柄上调用。  
  
 若要选择按列绑定的列，此字段设置为 SQL_BIND_BY_COLUMN （默认值）。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr**与 SQL_ATTR_ROW_BIND_TYPE*属性*。  
  
 Apd，在此字段指定要用于动态参数的绑定方向。  
  
 若要选择按列绑定为参数，此字段设置为 SQL_BIND_BY_COLUMN （默认值）。  
  
 APD 中的此字段还可以设置通过调用**SQLSetStmtAttr**与 SQL_ATTR_PARAM_BIND_TYPE*属性*。  
  
 **SQL_DESC_COUNT [All]**  
 此 SQLSMALLINT 标头字段指定的编号最高的记录的包含数据的基于 1 的索引。 当驱动程序设置描述符的数据结构时，它还必须设置 SQL_DESC_COUNT 字段，用于显示多少条记录是有意义。 当应用程序分配此数据结构的实例时，它无需指定多少条记录要保留的空间。 应用程序指定的记录的内容，如驱动程序将任何所需的操作，以确保描述符句柄引用到足够大小的数据结构。  
  
 SQL_DESC_COUNT 不是计数 （如果该字段正在 ARD） 绑定的所有数据列或所有参数都绑定 （如果该字段是 APD 中），但编号最高的记录数。 如果编号最高的列或参数未绑定，然后 SQL_DESC_COUNT 更改为下一编号最高的列或参数的数目。 如果某一列或具有大量的参数，小于编号最高的列数是未绑定 (通过调用**SQLBindCol**与*TargetValuePtr*参数设置为 null 指针或**SQLBindParameter**与*ParameterValuePtr*参数设置为 null 指针)，SQL_DESC_COUNT 不会更改。 如果数字大于包含数据的编号最高的记录与绑定其他列或参数，该驱动程序将自动增加 SQL_DESC_COUNT 字段中的值。 如果所有列都未都绑定通过调用**SQLFreeStmt**使用 SQL_UNBIND 选项中的 ARD 和 IRD 的 SQL_DESC_COUNT 字段设置为 0。 如果**SQLFreeStmt**称为 SQL_RESET_PARAMS 选项后，APD 和 IPD 中的 SQL_DESC_COUNT 字段设置为 0。  
  
 SQL_DESC_COUNT 中的值可以显式设置的应用程序通过调用**SQLSetDescField**。 如果显式减小 SQL_DESC_COUNT 中的值有效地删除编号大于 SQL_DESC_COUNT 中的新值的所有记录。 如果该字段正在 ARD SQL_DESC_COUNT 中的值显式设置为 0，释放所有数据缓冲区绑定的书签列除外。  
  
 ARD 此字段中的记录数不包括绑定的书签列。 取消绑定书签列的唯一方法是设置 SQL_DESC_DATA_PTR 字段为 null 指针。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [实现描述符]**  
 在 IRD 中为此 SQLULEN\*标头字段指向包含在调用后提取的行数的缓冲区**SQLFetch**或**SQLFetchScroll**，或在大容量操作中受影响的行数通过调用执行**SQLBulkOperations**或**SQLSetPos**，其中包括错误的行。  
  
 在 IPD 此 SQLUINTEGER * 标头字段指向包含已处理，包括错误集的参数集的数量的缓冲区。 如果这是 null 指针，则将返回无编号。  
  
 只有在调用后返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 后 SQL_DESC_ROWS_PROCESSED_PTR 是有效**SQLFetch**或**SQLFetchScroll** （适用于一个 IRD 字段） 或**SQLExecute**， **SQLExecDirect**，或**SQLParamData** （适用于 IPD 字段）。 如果指向缓冲区中填充的调用此字段不会返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定，除非其返回 sql_no_data 为止，在其中用例在缓冲区中的值设置为 0。  
  
 此外可以通过调用设置此字段中 ARD **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR 属性。 APD 中的此字段还可以设置通过调用**SQLSetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR 属性使用。  
  
 应用程序分配了此字段通过指向的缓冲区。 它是由驱动程序设置的延迟的输出缓冲区。 默认情况下，它是设置为 null 指针。  
  
## <a name="record-fields"></a>记录字段  
 每个描述符包含包含定义列数据或动态参数，具体取决于描述符的类型的字段的一个或多个记录。 每个记录是单个列或参数的完整定义。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 如果列是自动递增列或 SQL_FALSE 则列不是自动递增列，此只读 SQLINTEGER 记录字段包含 SQL_TRUE。 此字段是只读的但基础的自动递增列不一定是只读的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基列名称，为结果集列。 如果基列名称不存在 （如中所示的列的表达式的情况下），此变量包含空字符串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基本表的名称，为结果集列。 如果基表名称不能定义或不适用，则此变量包含空字符串。  
  
 **SQL_DESC_CASE_SENSITIVE [实现描述符]**  
 此只读 SQLINTEGER 记录字段包含 SQL_TRUE，如果列或参数视为以排序规则和比较或 SQL_FALSE 的区分大小写，如果列不将排序规则和比较的区分大小写，或如果它为非列。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基础表包含的列的目录。 返回值与驱动程序相关，如果列是表达式或列是视图的一部分。 如果数据源不支持目录或目录不能确定，此变量包含空字符串。  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 此 SQLSMALLINT 标头字段指定所有数据类型，包括日期时间和间隔数据类型的简洁数据类型。  
  
 SQL_DESC_CONCISE_TYPE、 的 SQL_DESC_TYPE、 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段中的值相互依赖。 每个时间域中的一个设置，其他还必须设置。 可以通过调用设置 SQL_DESC_CONCISE_TYPE **SQLBindCol**或**SQLBindParameter**，或**SQLSetDescField**。 可以通过调用设置的 SQL_DESC_TYPE **SQLSetDescField**或**SQLSetDescRec**。  
  
 如果 SQL_DESC_CONCISE_TYPE 设置为一个时间间隔或日期时间数据类型以外的简洁数据类型，SQL_DESC_TYPE 字段设置为相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为 0。  
  
 如果 SQL_DESC_CONCISE_TYPE 设置为简明的 datetime 或间隔数据类型，SQL_DESC_TYPE 字段设置为相应的详细类型 （SQL_DATETIME 或 SQL_INTERVAL） 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为相应的子代码。  
  
 **SQL_DESC_DATA_PTR [应用程序描述符和 Ipd]**  
 此 SQLPOINTER 记录字段将指向将包含的参数值 （Apd) 或 （对于 ARDs) 列值的变量。 此字段才*延迟的字段*。 在设置，但用于在更高版本时驱动程序检索数据时不使用它。  
  
 ARD 的 SQL_DESC_DATA_PTR 字段指定列是未绑定，则*TargetValuePtr*调用中的参数**SQLBindCol**是 null 指针或 ARD 如果 SQL_DESC_DATA_PTR 字段中设置的调用到**SQLSetDescField**或**SQLSetDescRec**到 null 指针。 如果 SQL_DESC_DATA_PTR 字段设置为 null 指针，不会影响其他字段。  
  
 如果在调用**SQLFetch**或**SQLFetchScroll** ，填写此字段通过指向的缓冲区未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。  
  
 每当设置 APD、 ARD 或 IPD 的 SQL_DESC_DATA_PTR 字段时，驱动程序将检查中的 SQL_DESC_TYPE 字段的值包含一个有效的 ODBC C 数据类型或特定于驱动程序的数据类型，并影响的数据类型的所有其他字段都是一致。 提示一致性检查是 IPD 的 SQL_DESC_DATA_PTR 字段的唯一用途。 具体而言，如果应用程序在设置 SQL_DESC_DATA_PTR 字段 IPD 和更高版本调用**SQLGetDescField**上此字段中，它不一定返回已设置的值。 详细信息，请参阅"一致性检查"中[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 此 SQLSMALLINT 记录字段包含特定的日期时间间隔数据类型的子代码的 SQL_DESC_TYPE 字段为 SQL_DATETIME 或 SQL_INTERVAL 时。 这适用于 SQL 和 C 数据类型。 代码使用"代码"（适用于 datetime 类型） 替换为"类型"或"C_TYPE"或"代码"（对于间隔类型） 替换为"间隔"或"C_INTERVAL"包含的数据类型名称。  
  
 如果描述符不是与语句句柄相关联的 SQL_DESC_TYPE 和在应用程序描述符 SQL_DESC_CONCISE_TYPE 设置为 SQL_C_DEFAULT，SQL_DESC_DATETIME_INTERVAL_CODE 内容未定义。  
  
 此字段可以设置为下表中列出的日期时间数据类型。  
  
|日期时间类型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 此字段可以设置为下表中列出的时间间隔数据类型。  
  
|间隔类型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/ SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/ SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/ SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/ SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/ SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/ SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 有关数据的时间间隔，则此字段的详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 此 SQLINTEGER 记录字段包含间隔起始精度，如果 SQL_DESC_TYPE 字段为 SQL_INTERVAL。 当 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为时间间隔数据类型时，此字段设置为默认间隔起始精度。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 此只读 SQLINTEGER 记录字段包含的最大为显示列中的数据所需字符数。  
  
 **SQL_DESC_FIXED_PREC_SCALE [实现描述符]**  
 如果列不是具有固定的精度和小数位数的精确数值列，此只读 SQLSMALLINT 记录字段是设置为 SQL_TRUE，如果为确切的数值列的列，并具有固定的精度和非零值的小数位数，或 SQL_FALSE。  
  
 **SQL_DESC_INDICATOR_PTR [Application descriptors]**  
 在 ARDs，此为 SQLLEN * 记录字段指向指示器变量。 如果列的值为 NULL，则此变量包含 SQL_NULL_DATA。 为 Apd，指示器变量设置为 SQL_NULL_DATA 指定空的动态参数。 否则，该变量为零 （除非 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 中的值是相同的指针）。  
  
 如果在 ARD SQL_DESC_INDICATOR_PTR 字段为 null 指针，会阻止驱动程序返回有关列是否为 NULL 的信息。 如果该列为 NULL 和 SQL_DESC_INDICATOR_PTR null 指针，SQLSTATE 22002 （指示器变量，但未提供） 时返回的驱动程序尝试在调用后填充缓冲区**SQLFetch**或**SQLFetchScroll**。 如果在调用**SQLFetch**或**SQLFetchScroll**未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。  
  
 SQL_DESC_INDICATOR_PTR 字段确定是否设置指向 SQL_DESC_OCTET_LENGTH_PTR 的字段。 如果列的数据值为 NULL，驱动程序将设置为 SQL_NULL_DATA 指示符变量。 然后未设置指向 SQL_DESC_OCTET_LENGTH_PTR 的字段。 如果在提取期间未遇到 NULL 值，通过 SQL_DESC_INDICATOR_PTR 指向的缓冲区设置为零和 SQL_DESC_OCTET_LENGTH_PTR 通过指向的缓冲区设置为数据的长度。  
  
 APD 中的 SQL_DESC_INDICATOR_PTR 字段是否为 null 指针，该应用程序不能使用此描述符记录指定空的参数。  
  
 此字段才*延迟的字段*:它不使用时设置，但在更高版本时使用驱动程序以指示可为 null 性 （适用于 ARDs) 或 （适用于 Apd) 确定为 null 性。  
  
 **SQL_DESC_LABEL [IRDs]**  
 此只读 SQLCHAR * 记录字段包含的列标签或标题。 如果列不具有一个标签，此变量将包含列名称。 如果为未命名的列并将其未标记，此变量包含空字符串。  
  
 **SQL_DESC_LENGTH [All]**  
 此 sqlulen 生成记录字段是字符串的字符的最大值或实际长度或二进制数据类型，以字节为单位。 这是固定长度的数据类型的最大长度或可变长度数据类型的实际长度。 其值始终不包括 null 终止字符的结束字符字符串。 对于值类型为 SQL_TYPE_DATE、 SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP，或 SQL interval 数据类型之一，此字段以字符为单位的 datetime 或间隔值的字符字符串表示形式的长度。  
  
 此字段中的值可能不同于"length"作为 ODBC 2 中定义的值 *.x*。 有关详细信息，请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 此只读 SQLCHAR * 记录字段包含的字符或驱动程序会识别为此数据类型的文字的前缀的字符。 此变量包含空字符串数据类型为其文字前缀不适用。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 此只读 SQLCHAR * 记录字段包含的字符或驱动程序会识别为此数据类型的文字的后缀的字符。 此变量包含空字符串数据类型为其文本后缀不适用。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR * 记录字段包含的数据类型可能不同于常规的数据类型名称的任何本地化 （本机语言） 名称。 如果没有本地化的名称，则返回空字符串。 此字段是仅出于显示目的。  
  
 **SQL_DESC_NAME [实现描述符]**  
 此 SQLCHAR * 行描述符记录字段包含的列别名，如果要将其应用。 如果列别名不适用，则返回的列名称。 在任一情况下，驱动程序将 SQL_DESC_UNNAMED 字段设置为 SQL_NAMED 时设置 SQL_DESC_NAME 字段。 如果没有任何列名称或列别名，该驱动程序 SQL_DESC_NAME 字段中返回一个空字符串，并将 SQL_DESC_UNNAMED 字段设置为 SQL_UNNAMED。  
  
 应用程序可以将 IPD SQL_DESC_NAME 字段设置为参数名称或别名，以按名称指定存储的过程参数。 (有关详细信息，请参阅[按名称 （命名参数） 绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。)IRD SQL_DESC_NAME 字段是只读的字段;SQLSTATE HY091 将返回 （无效的描述符字段标识符），如果应用程序尝试将其设置。  
  
 在 Ipd，此字段是未定义，如果该驱动程序不支持命名的参数。 如果驱动程序支持命名的参数，并能够描述参数，参数名称是在此字段中返回。  
  
 **SQL_DESC_NULLABLE [Implementation descriptors]**  
 IRDs，在此只读 SQLSMALLINT 记录字段是 SQL_NULLABLE，如果列可以具有 NULL 值，如果列不具有 NULL 值，SQL_NO_NULLS 或 SQL_NULLABLE_UNKNOWN，如果不知道列是否接受 NULL 值。 此字段与结果集列不基列。  
  
 在 Ipd，此字段始终设置为 SQL_NULLABLE 因为动态参数始终是可以为 null，不能通过应用程序设置。  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 此 SQLINTEGER 字段包含值为 2 如果中的 SQL_DESC_TYPE 字段的数据类型为近似数字数据类型，因为 SQL_DESC_PRECISION 字段包含的位数。 此字段包含值为 10 如果中的 SQL_DESC_TYPE 字段的数据类型为精确数字数据类型，因为 SQL_DESC_PRECISION 字段包含的小数位数。 此字段设置为 0 表示所有非数字数据类型。  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 此为 SQLLEN 记录字段包含的长度，以字节为单位的字符串或二进制数据类型。 对于固定长度的字符或二进制类型，这是以字节为单位的实际长度。 对于可变长度字符或二进制类型，这是以字节为单位的最大长度。 此值始终不包括实现描述符的 null 终止字符的空间，并始终包括在应用程序描述符的 null 终止字符的空间。 对于应用程序数据，此字段包含缓冲区的大小。 对于 Apd，此字段仅对输出或输入/输出参数的定义。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [Application descriptors]**  
 此为 SQLLEN * 记录字段指向的变量将包含以字节为单位 （适用于参数描述符） 的动态自变量或绑定的列的值 （适用于行描述符） 的总长度。  
  
 对于 APD 中，此值将忽略除字符的字符串和二进制; 之外的所有参数如果此字段将指向 SQL_NTS，动态自变量必须是以 null 结尾。 若要指示绑定的参数将为执行时数据参数，应用程序设置此字段相应的记录的 APD 中为变量的请在执行时，将包含值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果. 如果有多个此类字段，为唯一标识的参数的值设置 SQL_DESC_DATA_PTR，可以帮助确定哪些参数所请求的应用程序。  
  
 如果 ARD OCTET_LENGTH_PTR 字段为 null 指针，该驱动程序不返回列的长度信息。 APD SQL_DESC_OCTET_LENGTH_PTR 字段是否为 null 指针，该驱动程序假定字符串和二进制值都是以 null 结尾。 （二进制值不应为以 null 结尾但应为提供的长度，以避免被截断。）  
  
 如果在调用**SQLFetch**或**SQLFetchScroll** ，填写此字段通过指向的缓冲区未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，缓冲区的内容是不确定。 此字段才*延迟的字段*。 在设置，但用于在更高版本时驱动程序确定或指示八位字节长度的数据时不使用它。  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 此 SQLSMALLINT 记录字段设置为 SQL_PARAM_INPUT 为输入参数，用于输入/输出参数，对于输出参数，对于经过流处理输入/输出参数，SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_ SQL_PARAM_OUTPUT SQL_PARAM_INPUT_OUTPUTPARAM_OUTPUT_STREAM 流式传输的输出参数。 默认情况下，它是设置为 SQL_PARAM_INPUT。  
  
 IPD 的字段设置为 SQL_PARAM_INPUT 默认情况下如果 （SQL_ATTR_ENABLE_AUTO_IPD 语句属性是 SQL_FALSE） 的驱动程序不会自动填充 IPD。 应用程序应将此字段设置为不是输入的参数的参数 IPD 中。  
  
 **SQL_DESC_PRECISION [All]**  
 此 SQLSMALLINT 记录字段包含确切的数值类型，（二进制精度） 的近似数值类型的尾数的位数或数字 SQL_TYPE_TIME SQL_TYPE 秒的小数部分组件中的数字的位数_TIMESTAMP 或 SQL_INTERVAL_SECOND 数据类型。 此字段对于所有其他数据类型未定义。  
  
 此字段中的值可能不同于"精度"作为 ODBC 2 中定义的值 *.x*。 有关详细信息，请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [实现描述符]**  
 此 SQLSMALLINTrecord 字段指示是否一列自动修改 DBMS （例如 SQL Server 中的"timestamp"的类型的列） 更新行时。 此记录字段的值是否则设置为行版本控制列，列是否 SQL_TRUE 和 SQL_FALSE。 此列属性是类似于调用**SQLSpecialColumns**与 IdentifierType 的 SQL_ROWVER，以确定是否自动更新列。  
  
 **SQL_DESC_SCALE [All]**  
 此 SQLSMALLINT 记录字段包含定义的小数位数的 decimal 和 numeric 数据类型。 对于所有其他数据类型未定义字段。  
  
 此字段中的值可能不同于 ODBC 2 中定义的"规模"的值 *.x*。 有关详细信息，请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基础表包含的列的架构名称。 返回值与驱动程序相关，如果列是表达式或列是视图的一部分。 如果数据源不支持架构或架构名称不能确定，此变量包含空字符串。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   如果列不能用于 SQL_PRED_NONE**其中**子句。 (这是 ODBC 2 中的 SQL_UNSEARCHABLE 值相同 *.x*。)  
  
-   SQL_PRED_CHAR 如果中可以使用该列**其中**子句，但只带有**如**谓词。 (这是 ODBC 2 中的 SQL_LIKE_ONLY 值相同 *.x*。)  
  
-   SQL_PRED_BASIC 如果中可以使用该列**其中**使用除所有比较运算符的子句**如**。 (这是 ODBC 2 中的 SQL_EXCEPT_LIKE 值相同 *.x*。)  
  
-   如果列可在 SQL_PRED_SEARCHABLE**其中**子句包含任何比较运算符。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 此只读 SQLCHAR * 记录字段包含基础表包含此列的名称。 返回值与驱动程序相关，如果列是表达式或列是视图的一部分。  
  
 **SQL_DESC_TYPE [All]**  
 此 SQLSMALLINT 记录字段指定除日期时间和间隔数据类型之外的所有数据类型的简洁 SQL 或 C 数据类型。 对于日期时间和间隔数据类型，此字段指定为 SQL_DATETIME 或 SQL_INTERVAL 的详细数据类型。  
  
 每当此字段包含 SQL_DATETIME 或 SQL_INTERVAL，SQL_DESC_DATETIME_INTERVAL_CODE 字段必须包含简单的类型的相应子代码。 对于 datetime 数据类型的 SQL_DESC_TYPE 包含 SQL_DATETIME，和 SQL_DESC_DATETIME_INTERVAL_CODE 字段包含特定日期/时间数据类型的子代码。 间隔数据类型的 SQL_DESC_TYPE 包含 SQL_INTERVAL，SQL_DESC_DATETIME_INTERVAL_CODE 字段包含特定的时间间隔数据类型的子代码。  
  
 中的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 字段的值是相互依赖。 每个时间域中的一个设置，其他还必须设置。 可以通过调用设置的 SQL_DESC_TYPE **SQLSetDescField**或**SQLSetDescRec**。 可以通过调用设置 SQL_DESC_CONCISE_TYPE **SQLBindCol**或**SQLBindParameter**，或**SQLSetDescField**。  
  
 如果 SQL_DESC_TYPE 设置为一个时间间隔或日期时间数据类型以外的简洁数据类型，SQL_DESC_CONCISE_TYPE 字段设置为相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为 0。  
  
 如果将 SQL_DESC_TYPE 设置为详细 datetime 或间隔数据类型 （SQL_DATETIME 或 SQL_INTERVAL） 并且 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为相应的子代码，SQL_DESC_CONCISE 类型字段设置为相应的简洁类型。 尝试将 SQL_DESC_TYPE 设置为一种简洁的 datetime 或间隔类型将返回 SQLSTATE HY021 （描述符信息不一致）。  
  
 当通过调用设置的 SQL_DESC_TYPE 字段**SQLBindCol**， **SQLBindParameter**，或**SQLSetDescField**，为以下的默认值，设置以下字段下表中所示。 同一条记录的其余字段的值不确定。  
  
|SQL_DESC_TYPE 值|其他字段隐式设置|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH 设置为 1。 SQL_DESC_PRECISION 设置为 0。|  
|SQL_DATETIME|当 SQL_DESC_DATETIME_INTERVAL_CODE 设置为 SQL_CODE_DATE 或 SQL_CODE_TIME 时，SQL_DESC_PRECISION 设置为 0。 当它设置为 SQL_DESC_TIMESTAMP 时，SQL_DESC_PRECISION 设置为 6。|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE 设置为 0。 SQL_DESC_PRECISION 设置为各自的数据类型的实现定义的精度。<br /><br /> 请参阅[从 SQL 到 c:数值](../../../odbc/reference/appendixes/sql-to-c-numeric.md)有关如何手动将绑定 SQL_C_NUMERIC 值的信息。|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION SQL_FLOAT 设置为实现定义的默认精度。|  
|SQL_INTERVAL|当 SQL_DESC_DATETIME_INTERVAL_CODE 设置为时间间隔数据类型时，SQL_DESC_DATETIME_INTERVAL_PRECISION 设置为 2 （默认间隔前导精度）。 如果间隔的秒组成部分，SQL_DESC_PRECISION 设置为 6 （默认间隔秒精度）。|  
  
 当应用程序调用**SQLSetDescField**设置字段的描述符，而不是调用**SQLSetDescRec**，首先必须声明数据类型，该应用程序。 当它执行隐式设置上表中所指示的其他字段。 如果任何值隐式集是不可接受，然后，应用程序可以调用**SQLSetDescField**或**SQLSetDescRec**显式设置不可接受的值。  
  
 **SQL_DESC_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR * 记录字段包含的数据依赖于源的类型名称 （例如，"CHAR"、"VARCHAR"等）。 如果数据类型名称未知，则此变量包含空字符串。  
  
 **SQL_DESC_UNNAMED [实现描述符]**  
 行描述符此 SQLSMALLINT 记录字段设置为 SQL_NAMED 或 SQL_UNNAMED 驱动程序时它设置 SQL_DESC_NAME 字段。 如果 SQL_DESC_NAME 字段包含的列别名或列别名不适用，则该驱动程序会将 SQL_DESC_UNNAMED 字段设置为 SQL_NAMED。 如果应用程序将 IPD SQL_DESC_NAME 字段设置为参数名或别名，则驱动程序会将 IPD 的 SQL_DESC_UNNAMED 字段设置为 SQL_NAMED。 如果没有任何列名称或列别名，该驱动程序将 SQL_DESC_UNNAMED 字段设置为 SQL_UNNAMED。  
  
 应用程序可以设置为 SQL_UNNAMED IPD SQL_DESC_UNNAMED 字段。 驱动程序将返回 SQLSTATE HY091 （无效的描述符字段标识符） 如果应用程序尝试 IPD 的 SQL_DESC_UNNAMED 字段设置为 SQL_NAMED。 IRD SQL_DESC_UNNAMED 字段是只读的;SQLSTATE HY091 将返回 （无效的描述符字段标识符），如果应用程序尝试将其设置。  
  
 **SQL_DESC_UNSIGNED [实现描述符]**  
 如果有符号的列类型，此只读 SQLSMALLINT 记录字段是设置为 SQL_TRUE 如果列类型为无符号的或非数字或 SQL_FALSE。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   SQL_ATTR_READ_ONLY 如果结果集列是只读的。  
  
-   如果结果集列 SQL_ATTR_WRITE 为读写。  
  
-   SQL_ATTR_READWRITE_UNKNOWN 如果不知道结果是否将列设置可更新。  
  
 SQL_DESC_UPDATABLE 介绍结果集中的列、 不在基表中的列的可更新性。 此结果集列所基于的基表中的列的可更新性可能会不同于此字段中的值。 某列是否可更新可以基于数据类型、 用户权限和结果集自身的定义。 如果不清楚是否可更新列，则应返回 SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性检查  
 一致性检查时，将执行由驱动程序会自动应用程序为 ARD、 APD 或 IPD 的 SQL_DESC_DATA_PTR 字段将传递的值。 如果任何字段是与其他字段不一致**SQLSetDescField**将返回 SQLSTATE HY021 （描述符信息不一致）。 详细信息，请参阅"一致性检查"中[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|列绑定|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|一个参数绑定|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)
