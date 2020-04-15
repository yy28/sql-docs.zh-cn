---
title: SQLSetDescfield 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299547"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函数

**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
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
 [输入]指示包含应用程序要设置的字段的描述符记录。 描述符记录从 0 编号，记录编号 0 是书签记录。 对于标头字段，将忽略*RecNumber*参数。  
  
 *FieldIdentifier*  
 [输入]指示要设置其值的描述符的字段。 有关详细信息，请参阅"注释"部分中的"*字段标识符*参数"。  
  
 *ValuePtr*  
 [输入]指向包含描述符信息的缓冲区或整数值的指针。 数据类型取决于*字段标识符*的值。 如果*ValuePtr*是整数值，则根据*字段标识符*参数的值，它可以被视为 8 个字节 （SQLLEN）、4 个字节 （SQLINTEGER） 或 2 个字节 （SQLSMALLINT）。  
  
 *缓冲区长度*  
 [输入]如果*Field标识符*是 ODBC 定义的字段 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为 **ValuePtr*的长度。 对于字符串数据，此参数应包含字符串中的字节数。  
  
 如果*字段标识符*是 ODBC 定义的字段 *，ValuePtr*是整数，则忽略*缓冲区长度*。  
  
 如果*Field标识符*是驱动程序定义的字段，则应用程序通过设置*BufferLength*参数向驱动程序管理器指示该字段的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*ValuePtr*是指向字符串的指针，则*缓冲区长度*是字符串的长度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*BufferLength*应具有该值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定长度值，则*缓冲区长度*为SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT（视适用）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetDescField**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_DESC的*句柄类型*和*描述符句柄*。 下表列出了**SQLSetDescField**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持*\*ValuePtr*中指定的值（如果*ValuePtr*是指针）或*ValuePtr*中的值（如果*ValuePtr*是整数值），或者*\*ValuePtr*由于实现工作条件而无效，因此驱动程序替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07009|无效描述符索引|*字段标识符*参数是记录字段 *，RecNumber*参数为 0，*描述符句柄*参数引用 IPD 句柄。<br /><br /> *RecNumber*参数小于 0，*描述符处理*参数引用 ARD 或 APD。<br /><br /> *RecNumber*参数大于数据源可以支持的最大列或参数数，*描述符处理*参数引用 APD 或 ARD。<br /><br /> （DM）*字段标识符*参数*\*SQL_DESC_COUNT，ValuePtr*参数小于 0。<br /><br /> *RecNumber*参数等于 0，*描述符句柄*参数引用隐式分配的 APD。 （显式分配的应用程序描述符不会发生此错误，因为在执行时间之前，不知道显式分配的应用程序描述符是 APD 还是 ARD。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22001|字符串数据，右截断|*字段标识符*参数SQL_DESC_NAME，*缓冲区长度*参数的值大于SQL_MAX_IDENTIFIER_LEN。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM）*描述符处理*与*语句句柄*相关联，在调用此函数时，调用了异步执行函数（不是此函数），并且仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*，其中*描述符句柄*SQL_NEED_DATA关联并返回。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 对于与*描述符句柄*关联的连接句柄，调用了异步执行函数。 调用**SQLSetDescField**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用为与*描述符句柄*关联的语句句柄之一，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecute** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY016|无法修改实现行描述符|*描述符句柄*参数与 IRD 相关联，*并且字段标识符*参数未SQL_DESC_ARRAY_STATUS_PTR或SQL_DESC_ROWS_PROCESSED_PTR。|  
|HY021|描述符信息不一致|SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE字段不形成有效的 ODBC SQL 类型或有效的特定于驱动程序的 SQL 类型（对于 IPD）或有效的 ODBC C 类型（对于 AD 或 AD）。<br /><br /> 在一致性检查期间检查的描述符信息不一致。 （请参阅**SQLSetDescRec**中的"一致性检查"|  
|HY090|无效的字符串或缓冲区长度|（DM） * \*ValuePtr*是一个字符串，*缓冲区长度*小于零，但不等于SQL_NTS。<br /><br /> （DM） 驱动程序是 ODBC 2 *.x*驱动程序，描述符是 ARD，*列号*参数设置为 0，为参数*BufferLength*指定的值不等于 4。|  
|HY091|无效描述符字段标识符|为*FieldIdentifier 参数*指定的值不是 ODBC 定义的字段，不是实现定义的值。<br /><br /> 对于*描述符处理*参数，*字段标识符*参数无效。<br /><br /> *字段标识符*参数是一个只读的 ODBC 定义的字段。|  
|HY092|无效属性/选项标识符|* \*ValuePtr*中的值对*字段标识符*参数无效。<br /><br /> *字段标识符*参数SQL_DESC_UNNAMED，ValuePtr *ValuePtr* SQL_NAMED。|  
|HY105|无效参数类型|（DM） 为SQL_DESC_PARAMETER_TYPE字段指定的值无效。 （有关详细信息，请参阅**SQLBind 参数**中的"*输入输出类型*参数"部分。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*描述符处理*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetDescField**来一次设置一个描述符字段。 对**SQLSetDescField 的**一次调用在单个描述符中设置单个字段。 可以调用此函数来设置任何描述符类型中的任何字段，前提是可以设置该字段。 （请参阅本节后面的表。  
  
> [!NOTE]  
>  如果对**SQLSetDescField**的调用失败，则*RecNumber*参数标识的描述符记录的内容将未定义。  
  
 可以调用其他函数来设置具有函数单个调用的多个描述符字段。 **SQLSetDescRec**函数设置各种字段，这些字段会影响绑定到列或参数的数据类型和缓冲区（SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR字段）。 **SQLBindCol**或**SQLBind参数**可用于为列或参数的绑定制定完整的规范。 这些函数设置具有一个函数调用的特定描述符字段组。  
  
 可以调用**SQLSetDescField**来通过向绑定指针（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR或SQL_DESC_OCTET_LENGTH_PTR）添加偏移量来更改绑定缓冲区。 这将更改绑定缓冲区而不调用**SQLBindCol**或**SQLBindparameter**，这允许应用程序更改SQL_DESC_DATA_PTR而不更改其他字段，如SQL_DESC_DATA_TYPE。  
  
 如果应用程序调用**SQLSetDescField**来设置SQL_DESC_COUNT以外的任何字段，或者SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR或SQL_DESC_INDICATOR_PTR的延迟字段，则记录将变为未绑定。  
  
 描述符标头字段是通过使用相应的*字段标识符*调用**SQLSetDescField**来设置的。 许多标头字段也是语句属性，因此也可以通过调用**SQLSetStmtAttr**来设置它们。 这允许应用程序在不首先获取描述符句柄的情况下设置描述符字段。 当调用**SQLSetDescField**来设置标头字段时，将忽略*RecNumber*参数。  
  
 *RecNumber* 0 用于设置书签字段。  
  
> [!NOTE]  
>  在调用**SQLSetDescField**来设置书签字段之前，应始终设置语句属性SQL_ATTR_USE_BOOKMARKS。 虽然这不是强制性的，但强烈建议这样做。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>设置描述符字段的顺序  
 通过调用**SQLSetDescField**设置描述符字段时，应用程序必须遵循特定顺序：  
  
1.  应用程序必须首先设置SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE或SQL_DESC_DATETIME_INTERVAL_CODE字段。  
  
2.  设置这些字段之一后，应用程序可以设置数据类型的属性，并且驱动程序将数据类型属性字段设置为数据类型的相应默认值。 类型属性字段的自动默认可确保描述符始终准备好在应用程序指定数据类型后使用。 如果应用程序显式设置数据类型属性，则它将重写默认属性。  
  
3.  在步骤 1 中列出的一个字段被设置并设置了数据类型属性后，应用程序可以SQL_DESC_DATA_PTR设置。 这提示对描述符字段进行一致性检查。 如果应用程序在设置SQL_DESC_DATA_PTR字段后更改数据类型或属性，则驱动程序将SQL_DESC_DATA_PTR设置为空指针，取消绑定记录。 这将强制应用程序在描述符记录可用之前按顺序完成正确的步骤。  
  
## <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化  
 分配描述符时，描述符中的字段可以初始化为默认值，在没有默认值的情况下初始化，或者未定义描述符的类型。 下表指示每种描述符类型每个字段的初始化，其中"D"指示该字段用默认值初始化，而"ND"表示该字段在没有默认值的情况下初始化。 如果显示数字，则字段的默认值为该数字。 这些表还指示字段是读/写 （R/W） 还是只读 （R）。  
  
 IRD 的字段仅在准备或执行语句并填充 IRD 之后才具有默认值，而不是在分配语句句柄或描述符后。 在填充 IRD 之前，任何尝试访问 IRD 字段的尝试都将返回错误。  
  
 某些描述符字段是为描述符类型的一个或多个（但不是全部）定义的（AD 和 IRD 以及 AD 和 IPD）。 当一个字段未为描述符类型定义时，使用该描述符的任何函数都不需要该字段。  
  
 **SQLGetDescField**可以访问的字段不一定由**SQLSetDescField**设置。 下表列出了**SQLSetDescField**可以设置的字段。  
  
 标题字段的初始化在下表中概述。  
  
|标题字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD： R APD： R IRD： R IPD： R|ARD：SQL_DESC_ALLOC_AUTO隐式或SQL_DESC_ALLOC_USER为显式<br /><br /> APD：SQL_DESC_ALLOC_AUTO隐式或SQL_DESC_ALLOC_USER为显式<br /><br /> 国际复兴开发银行：SQL_DESC_ALLOC_AUTO<br /><br /> IPD：SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD：[1] APD：[1] IRD：未使用的 IPD：未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD：R/W APD：R/W IRD：R/W IPD：R/W|ARD： 空点子 APD： 空点 ptr IRD： 空点 IPD： 空点子|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD： 空点子 APD： 空点子 IRD： 未使用的 IPD： 未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD： SQL_BIND_BY_COLUMN<br /><br /> APD：SQL_BIND_BY_COLUMN<br /><br /> IRD：未使用<br /><br /> IPD：未使用|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： 0 APD： 0 IRD： D IPD： 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD：未使用的 APD：未使用的 IRD：R/W IPD：R/W|ARD：未使用的 APD：未使用的 IRD：空点 IPD：空点子|  
  
 [1] 仅当驱动程序自动填充 IPD 时，才会定义这些字段。 如果没有，它们未定义。 如果应用程序尝试设置这些字段，将返回 SQLSTATE HY091（无效描述符字段标识符）。  
  
 记录字段的初始化如下表所示。  
  
|记录字段名称|类型|R/W|默认|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD：未使用的 APD：未使用的 IRD：D IPD：D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： SQL_C_ DEFAULT APD： SQL_C_ DEFAULT IRD： D IPD： ND|  
|SQL_DESC_DATA_PTR|SQLPointer|ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD： 空点子 APD： 空点子 IRD： 未使用的 IPD： 未使用 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD：未使用的 APD：未使用的 IRD：D IPD：D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN ||ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD： 空点子 APD： 空点子 IRD： 未使用的 IPD： 未使用|  
|SQL_DESC_LABEL|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_LENGTH|SQLULEN|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD：未使用的 APD：未使用的 IRD：D IPD：D[1]|  
|SQL_DESC_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN ||ARD：R/W APD：R/W IRD：未使用的 IPD：未使用|ARD： 空点子 APD： 空点子 IRD： 未使用的 IPD： 未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：未使用的 IPD：R/W|ARD：未使用的 APD：未使用的 IRD：未使用的 IPD：D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD：未使用<br /><br /> APD：未使用<br /><br /> IRD： R<br /><br /> IPD： R|ARD：未使用<br /><br /> APD：未使用<br /><br /> IRD： ND<br /><br /> IPD： ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD：R/W APD：R/W IRD：R IPD：R/W|ARD： SQL_C_DEFAULT APD： SQL_C_DEFAULT IRD： D IPD： ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR ||ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD：未使用的 APD：未使用的 IRD：D IPD：D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：R|ARD：未使用的 APD：未使用的 IRD：D IPD：D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：R IPD：未使用|ARD：未使用的 APD：未使用的 IRD：D IPD：未使用|  
  
 [1] 仅当驱动程序自动填充 IPD 时，才会定义这些字段。 如果没有，它们未定义。 如果应用程序尝试设置这些字段，将返回 SQLSTATE HY091（无效描述符字段标识符）。  
  
 [2] IPD 中的SQL_DESC_DATA_PTR字段可以设置为强制一致性检查。 在随后调用**SQLGetDescField**或**SQLGetDescRec 时**，不需要驱动程序返回SQL_DESC_DATA_PTR设置为的值。  
  
## <a name="fieldidentifier-argument"></a>字段标识符参数  
 *字段标识符*参数指示要设置的描述符字段。 描述符包含*描述符标头，* 由下一节中描述的标题字段"标题字段"和零个或多个*描述符记录组成，* 由"标题字段"部分后部分中描述的记录字段组成。  
  
## <a name="header-fields"></a>标题字段  
 每个描述符都有一个标头，其中包含以下字段：  
  
 **SQL_DESC_ALLOC_TYPE [全部]**  
 此只读 SQLSMALLINT 标头字段指定描述符是由驱动程序自动分配还是由应用程序显式分配。 应用程序可以获取而不是修改此字段。 如果描述符由驱动程序自动分配，则该字段设置为由驱动程序SQL_DESC_ALLOC_AUTO。 如果描述符由应用程序显式分配，则驱动程序将其设置为SQL_DESC_ALLOC_USER。  
  
 **SQL_DESC_ARRAY_SIZE [应用程序描述符]**  
 在 ARD 中，此 SQLULEN 标头字段指定行集中的行数。 这是调用**SQLFetch**或**SQLFetchScroll**或通过调用**SQLBulk 操作**或**SQLSetPos**返回的行数。  
  
 在 AD 中，此 SQLULEN 标头字段指定每个参数的值数。  
  
 此字段的默认值为 1。 如果SQL_DESC_ARRAY_SIZE大于 APD 或 ARD 指向数组的 1、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR。 每个数组的基数等于此字段的值。  
  
 ARD 中的此字段也可以通过使用SQL_ATTR_ROW_ARRAY_SIZE属性调用**SQLSetStmtAttr**来设置。 APD 中的此字段也可以通过使用SQL_ATTR_PARAMSET_SIZE属性调用**SQLSetStmtAttr**来设置。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [全部]**  
 对于每种描述符类型，此 SQLUSMALLINT = 标头字段指向 SQLUSMALLINT 值数组。 这些数组的命名方式如下：行状态数组 （IRD）、参数状态数组 （IPD）、行操作数组 （ARD） 和参数操作数组 （APD）。  
  
 在 IRD 中，此标头字段指向在调用**SQLBulk 操作**、SQLFetch、SQLFetchScroll**SQLFetch**或**SQLFetchScroll****SQLSetPos**后包含状态值的行状态数组。 数组具有与行集中的行一样多的元素。 应用程序必须分配 SQLUSMALLINT 数组，并将此字段设置为指向数组。 默认情况下，该字段设置为空指针。 驱动程序将填充数组 - 除非SQL_DESC_ARRAY_STATUS_PTR字段设置为空指针，在这种情况下不会生成状态值，并且数组未填充。  
  
> [!CAUTION]  
>  如果应用程序设置 IRD SQL_DESC_ARRAY_STATUS_PTR 字段指向的行状态数组的元素，则驱动程序行为未定义。  
  
 数组最初由对**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos**的调用填充。 **SQLFetchScroll** 如果调用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则此字段指向的数组的内容将未定义。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_SUCCESS：该行已成功提取，自上次提取以来未更改。  
  
-   SQL_ROW_SUCCESS_WITH_INFO：该行已成功提取，自上次提取以来未更改。 但是，返回了有关该行的警告。  
  
-   SQL_ROW_ERROR：获取行时出错。  
  
-   SQL_ROW_UPDATED：该行已成功提取，自上次提取以来已更新。 如果再次提取该行，则其状态为SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED：自上次提取行以来，该行已被删除。  
  
-   SQL_ROW_ADDED：该行由**SQLBulk 操作**插入。 如果再次提取该行，则其状态为SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW：行集与结果集的末尾重叠，并且不会返回对应于行状态数组的此元素的行。  
  
 IRD 中的此字段也可以通过使用SQL_ATTR_ROW_STATUS_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 IRD 的SQL_DESC_ARRAY_STATUS_PTR字段仅在返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO后才有效。 如果返回代码不是其中之一，则SQL_DESC_ROWS_PROCESSED_PTR指向的位置未定义。  
  
 在 IPD 中，此标头字段指向一个参数状态数组，其中包含对 SQLExecute 或**SQLExecDirect**调用**SQLExecDirect**后每组参数值的状态信息。 如果对 SQLExecute 或**SQLExecDirect**的调用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则此字段指向的数组的内容未定义。 **SQLExecDirect** 应用程序必须分配 SQLUSMALLINT 数组，并将此字段设置为指向数组。 驱动程序将填充数组 - 除非SQL_DESC_ARRAY_STATUS_PTR字段设置为空指针，在这种情况下不会生成状态值，并且数组未填充。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_SUCCESS：已成功为这组参数执行 SQL 语句。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO：已成功为这组参数执行 SQL 语句;但是，诊断数据结构中提供了警告信息。  
  
-   SQL_PARAM_ERROR：在处理这组参数时出错。 诊断数据结构中提供了其他错误信息。  
  
-   SQL_PARAM_UNUSED：此参数集未使用，可能是因为以前的一些参数集导致错误中止进一步处理，或者因为 aPD 的SQL_DESC_ARRAY_STATUS_PTR字段指定的数组中为该参数集设置了SQL_PARAM_IGNORE。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE：诊断信息不可用。 例如，当驱动程序将参数数组视为单片单元，因此不会生成此级别的错误信息。  
  
 IPD 中的此字段也可以通过使用SQL_ATTR_PARAM_STATUS_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 在 ARD 中，此标头字段指向一个行操作数组，该数组的值可以由应用程序设置，以指示是否为**SQLSetPos**操作忽略此行。 数组中的元素可以包含以下值：  
  
-   SQL_ROW_PROCEED：该行包含在使用**SQLSetPos**的批量操作中。 （此设置不保证该操作将在行上发生。 如果该行的状态SQL_ROW_ERROR IRD 行状态数组中，则驱动程序可能无法在行中执行操作。  
  
-   SQL_ROW_IGNORE： 使用**SQLSetPos**将该行从批量操作中排除。  
  
 如果未设置数组的元素，则所有行都包含在批量操作中。 如果 ARD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为空指针，则所有行都包含在批量操作中;如果 ARD 字段中的值为空指针，则所有行都包含在批量操作中。"解释与指针指向有效数组和数组的所有元素都SQL_ROW_PROCEED相同。 如果数组中的元素设置为SQL_ROW_IGNORE，则忽略行的行状态数组中的值不会更改。  
  
 ARD 中的此字段也可以通过使用SQL_ATTR_ROW_OPERATION_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 在 APD 中，此标头字段指向应用程序可以设置的值的参数操作数组，以指示在调用 SQLExecute 或**SQLExecDirect**时是否忽略这组**SQLExecDirect**参数。 数组中的元素可以包含以下值：  
  
-   SQL_PARAM_PROCEED：SQLExecute 或**SQLExecDirect**调用中包含**SQLExecDirect**一组参数。  
  
-   SQL_PARAM_IGNORE：从 SQLExecute 或**SQLExecDirect**调用**SQLExecDirect**中排除参数集。  
  
 如果未设置数组的元素，则 SQLExecute 或**SQLExecDirect**调用中将使用数组中的所有参数集。 **SQLExecDirect** 如果 APD SQL_DESC_ARRAY_STATUS_PTR 字段中的值为空指针，则使用所有参数集;如果使用 aPD 字段中的值，则使用所有参数集。解释与指针指向有效数组和数组的所有元素SQL_PARAM_PROCEED相同。  
  
 APD 中的此字段也可以通过使用SQL_ATTR_PARAM_OPERATION_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 **SQL_DESC_BIND_OFFSET_PTR [应用程序描述符]**  
 此 SQLLEN = 标头字段指向绑定偏移量。 默认情况下，它设置为空指针。 如果此字段不是空指针，则驱动程序将引用指针，并将已引用的值添加到在提取时描述符记录中具有非空值（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR）的每个延迟字段，并在绑定时使用新的指针值。  
  
 绑定偏移量始终直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR字段中的值。 如果偏移更改为其他值，则新值仍直接添加到每个描述符字段中的值。 新偏移量不会添加到字段值加上任何较早的偏移量中。  
  
 此字段是*延迟字段*：在设置时不使用它，但在需要确定数据缓冲区的地址时，驱动程序稍后会使用它。  
  
 ARD 中的此字段也可以通过使用SQL_ATTR_ROW_BIND_OFFSET_PTR属性调用**SQLSetStmtAttr**来设置。 ARD 中的此字段也可以通过使用SQL_ATTR_PARAM_BIND_OFFSET_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 有关详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)和[SQLBind参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)中行绑定的说明。  
  
 **SQL_DESC_BIND_TYPE [应用程序描述符]**  
 此 SQLUINTEGER 标头字段设置绑定方向，用于绑定列或参数。  
  
 在 AD 中，此字段指定在关联语句句柄上调用**SQLFetchScroll**或**SQLFetch**时绑定方向。  
  
 要为列选择按列方向的绑定，此字段设置为SQL_BIND_BY_COLUMN（默认值）。  
  
 ARD 中的此字段也可以通过使用 SQL_ATTR_ROW_BIND_TYPE*属性*调用**SQLSetStmtAttr**来设置。  
  
 在 AD 中，此字段指定用于动态参数的绑定方向。  
  
 要为参数选择按列绑定，此字段设置为SQL_BIND_BY_COLUMN（默认值）。  
  
 APD 中的此字段也可以通过使用 SQL_ATTR_PARAM_BIND_TYPE*属性*调用**SQLSetStmtAttr**来设置。  
  
 **SQL_DESC_COUNT [全部]**  
 此 SQLSMALLINT 标头字段指定包含数据的最高编号记录的基于 1 的索引。 当驱动程序为描述符设置数据结构时，它还必须设置SQL_DESC_COUNT字段以显示有多少记录很重要。 当应用程序分配此数据结构的实例时，它不必指定要为其保留多少记录。 当应用程序指定记录的内容时，驱动程序会执行任何必需的操作，以确保描述符句柄引用大小适当的数据结构。  
  
 SQL_DESC_COUNT不是绑定的所有数据列（如果字段位于 ARD 中）或绑定的所有参数（如果字段位于 APD 中）的计数，而是编号最高的记录数。 如果最高编号的列或参数未绑定，则SQL_DESC_COUNT更改为下一个编号最高的列或参数的编号。 如果数字小于最高编号列数的列或参数未绑定（通过调用**SQLBindCol，** 将*TargetValuePtr*参数设置为空指针，或将*参数ValuePtr*参数设置为空指针的**SQLBindparameter），** 则不会更改SQL_DESC_COUNT。 如果附加列或参数的编号大于包含数据的最高编号记录，则驱动程序会自动增加SQL_DESC_COUNT字段中的值。 如果使用"SQL_UNBIND"选项调用**SQLFreeStmt**取消绑定所有列，则 ARD 和 IRD 中的SQL_DESC_COUNT字段设置为 0。 如果使用SQL_RESET_PARAMS选项调用**SQLFreeStmt，** 则 APD 和 IPD 中的SQL_DESC_COUNT字段设置为 0。  
  
 SQL_DESC_COUNT中的值可以通过调用**SQLSetDescField**由应用程序显式设置。 如果显式减小SQL_DESC_COUNT中的值，则有效删除SQL_DESC_COUNT中数字大于新值的所有记录。 如果SQL_DESC_COUNT中的值显式设置为 0，并且该字段位于 ARD 中，则释放除绑定书签列之外的所有数据缓冲区。  
  
 ARD 此字段中的记录计数不包括绑定书签列。 取消绑定书签列的唯一方法是将SQL_DESC_DATA_PTR字段设置为空指针。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [实现描述符]**  
 在 IRD 中，此\*SQLULEN 标头字段指向一个缓冲区，其中包含调用**SQLFetch**或**SQLFetchScroll**后获取的行数，或调用**SQLBulk 操作**或**SQLSetPos（** 包括错误行）在批量操作中受影响的行数。  
  
 在 IPD 中，此 SQLUINTEGER = 标头字段指向一个缓冲区，其中包含已处理的参数集数，包括错误集。 如果这是空指针，则不会返回任何数字。  
  
 SQL_DESC_ROWS_PROCESSED_PTR仅在调用**SQLFetch**或**SQLFetchScroll（** 对于 IRD 字段）或 SQLExecute、SQLExecDirect**SQLExecute**或**SQLParamData（** 对于 IPD 字段）后返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO后才有效。 **SQLExecDirect** 如果填充此字段指向的缓冲区的调用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容将未定义，除非返回SQL_NO_DATA，在这种情况下缓冲区中的值设置为 0。  
  
 ARD 中的此字段也可以通过使用SQL_ATTR_ROWS_FETCHED_PTR属性调用**SQLSetStmtAttr**来设置。 APD 中的此字段也可以通过使用SQL_ATTR_PARAMS_PROCESSED_PTR属性调用**SQLSetStmtAttr**来设置。  
  
 此字段指向的缓冲区由应用程序分配。 它是驱动程序设置的延迟输出缓冲区。 默认情况下，它设置为空指针。  
  
## <a name="record-fields"></a>记录字段  
 每个描述符包含一个或多个记录，这些记录由定义列数据或动态参数的字段组成，具体取决于描述符的类型。 每个记录都是单个列或参数的完整定义。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [红外点]**  
 此只读 SQLINTEGER 记录字段包含SQL_TRUE如果列是自动递增列，则SQL_FALSE列不是自动递增列。 此字段是只读的，但基础自动递增列不一定是只读的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [红外点]**  
 此只读 SQLCHAR = 记录字段包含结果集列的基本列名称。 如果基本列名称不存在（如表达式的列），此变量包含一个空字符串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRD]**  
 此只读 SQLCHAR = 记录字段包含结果集列的基表名称。 如果无法定义基表名称或不适用，则此变量包含一个空字符串。  
  
 **SQL_DESC_CASE_SENSITIVE [实现描述符]**  
 此只读 SQLINTEGER 记录字段包含SQL_TRUE如果列或参数被视为区分大小写（用于排序规则和比较）;如果该列不被视为区分大小写（用于排序规则和比较）或该列是否被视为非字符列，则SQL_FALSE。  
  
 **SQL_DESC_CATALOG_NAME [红外指示]**  
 此只读 SQLCHAR = 记录字段包含包含列的基表的目录。 如果列是表达式或列是视图的一部分，则返回值与驱动程序相关。 如果数据源不支持目录或无法确定目录，则此变量包含一个空字符串。  
  
 **SQL_DESC_CONCISE_TYPE [全部]**  
 此 SQLSMALLINT 标头字段指定所有数据类型（包括日期时间和间隔数据类型）的简明数据类型。  
  
 SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE字段中的值是相互依赖的。 每次设置其中一个字段时，还必须设置另一个字段。 SQL_DESC_CONCISE_TYPE可以通过调用**SQLBindCol**或**SQLBind参数**（或**SQLSetDescField）** 来设置。 SQL_DESC_TYPE可以通过调用**SQLSetDescField**或**SQLSetDescRec**来设置。  
  
 如果SQL_DESC_CONCISE_TYPE设置为间隔或日期时间数据类型以外的简明数据类型，则SQL_DESC_TYPE字段设置为相同的值，SQL_DESC_DATETIME_INTERVAL_CODE字段设置为 0。  
  
 如果SQL_DESC_CONCISE_TYPE设置为简明日期时间或间隔数据类型，则SQL_DESC_TYPE字段设置为相应的详细类型（SQL_DATETIME或SQL_INTERVAL），并将SQL_DESC_DATETIME_INTERVAL_CODE字段设置为相应的子代码。  
  
 **SQL_DESC_DATA_PTR [应用程序描述符和 IPD]**  
 此 SQLPOINTER 记录字段指向将包含参数值（对于 AD）或列值（用于 AD）的变量。 此字段是*递延字段*。 它在设置时不使用，但驱动程序稍后使用它来检索数据。  
  
 如果调用**SQLBindCol**中的*TargetValuePtr*参数为空指针，或者 ARD 中的SQL_DESC_DATA_PTR字段由对**SQLSetDescField**或**SQLSetDescRec**的调用设置为空指针，则 ARD SQL_DESC_DATA_PTR字段指定的列将取消绑定。 如果SQL_DESC_DATA_PTR字段设置为空指针，则其他字段不受影响。  
  
 如果对**SQLFetch**或**SQLFetchScroll**的调用填充此字段指向的缓冲区未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容未定义。  
  
 每当设置 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR字段时，驱动程序都会检查SQL_DESC_TYPE字段中的值是否包含有效的 ODBC C 数据类型或特定于驱动程序的数据类型，并且影响数据类型的所有其他字段是否一致。 提示一致性检查是 IPD SQL_DESC_DATA_PTR字段的唯一用途。 具体而言，如果应用程序设置 IPD 的SQL_DESC_DATA_PTR字段，并在此字段上调用**SQLGetDescField，** 则不一定返回它设置的值。 有关详细信息，请参阅[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的"一致性检查"。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [全部]**  
 当SQL_DESC_TYPE字段SQL_DATETIME或SQL_INTERVAL时，此 SQLSMALLINT 记录字段包含特定日期时间或间隔数据类型的子代码。 SQL 和 C 数据类型都是如此。 代码由数据类型名称组成，其中"CODE"代替了"TYPE"或"C_TYPE"（用于日期时间类型），或"CODE"代替"INTERVAL"或"C_INTERVAL"（对于间隔类型）。  
  
 如果应用程序描述符中的SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE设置为SQL_C_DEFAULT，并且描述符不与语句句柄关联，则SQL_DESC_DATETIME_INTERVAL_CODE的内容未定义。  
  
 此字段可用于下表中列出的日期时间数据类型。  
  
|日期时间类型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 此字段可用于下表中列出的间隔数据类型。  
  
|间隔类型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/ SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 有关数据间隔和此字段的详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [全部]**  
 如果SQL_DESC_TYPE字段SQL_INTERVAL，则此 SQLINTEGER 记录字段包含间隔前导精度。 当SQL_DESC_DATETIME_INTERVAL_CODE字段设置为间隔数据类型时，此字段设置为默认间隔前导精度。  
  
 **SQL_DESC_DISPLAY_SIZE [IRD]**  
 此只读 SQLINTEGER 记录字段包含显示列中数据所需的最大字符数。  
  
 **SQL_DESC_FIXED_PREC_SCALE [实现描述符]**  
 如果列是精确数值列且具有固定精度和非零比例，则此只读 SQLSMALLINT 记录字段设置为SQL_TRUE，如果列不是具有固定精度和刻度的精确数字列，则SQL_FALSE。  
  
 **SQL_DESC_INDICATOR_PTR [应用程序描述符]**  
 在 ARD 中，此 SQLLEN = 记录字段指向指标变量。 如果列值为 NULL，则此变量包含SQL_NULL_DATA。 对于 AD，指标变量设置为SQL_NULL_DATA指定 NULL 动态参数。 否则，变量为零（除非SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR中的值是相同的指针）。  
  
 如果 ARD 中的SQL_DESC_INDICATOR_PTR字段为空指针，则阻止驱动程序返回有关列是否为 NULL 的信息。 如果列为 NULL 且SQL_DESC_INDICATOR_PTR为空指针，则当驱动程序尝试在调用**SQLFetch**或**SQLFetchScroll**后填充缓冲区时，将返回 SQLSTATE 22002（需要但未提供指标变量）。 如果对**SQLFetch**或**SQLFetchScroll**的调用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容未定义。  
  
 SQL_DESC_INDICATOR_PTR字段确定是否设置了SQL_DESC_OCTET_LENGTH_PTR指向的字段。 如果列的数据值为 NULL，则驱动程序将指示器变量设置为SQL_NULL_DATA。 然后不设置SQL_DESC_OCTET_LENGTH_PTR指向的字段。 如果在提取过程中未遇到 NULL 值，则SQL_DESC_INDICATOR_PTR指向的缓冲区设置为零，SQL_DESC_OCTET_LENGTH_PTR指向的缓冲区设置为数据的长度。  
  
 如果 APD 中的SQL_DESC_INDICATOR_PTR字段是空指针，则应用程序不能使用此描述符记录指定 NULL 参数。  
  
 此字段是*递延字段*：在设置时不使用它，但驱动程序稍后使用它来指示 null（对于 AD）或确定 null（对于 AD）。  
  
 **SQL_DESC_LABEL [红外指示]**  
 此只读 SQLCHAR = 记录字段包含列标签或标题。 如果列没有标签，则此变量包含列名称。 如果列未命名且未标记，则此变量包含一个空字符串。  
  
 **SQL_DESC_LENGTH [全部]**  
 此 SQLULEN 记录字段是字符字符串的最大长度或实际长度，或以字节为单位的二进制数据类型。 它是固定长度数据类型的最大长度，或可变长度数据类型的实际长度。 其值始终排除结束字符字符串的 null 终止字符。 对于类型为SQL_TYPE_DATE、SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP 或 SQL 间隔数据类型之一的值，此字段具有日期时间或间隔值的字符串表示的字符长度。  
  
 此字段中的值可能与 ODBC 2 *.x*中定义的"长度"值不同。 有关详细信息，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [红外点]**  
 此只读 SQLCHAR = 记录字段包含驱动程序识别为此数据类型文本的前缀的字符或字符。 此变量包含不适用于文本前缀的数据类型的空字符串。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRD]**  
 此只读 SQLCHAR = 记录字段包含驱动程序识别为此数据类型文本的后缀的字符或字符。 此变量包含不适用于文本后缀的数据类型的空字符串。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR = 记录字段包含数据类型可能与数据类型的常规名称不同的任何本地化（母语）名称。 如果没有本地化名称，则返回一个空字符串。 此字段仅用于显示目的。  
  
 **SQL_DESC_NAME [实现描述符]**  
 此 SQLCHAR = 行描述符中的记录字段包含列别名（如果适用）。 如果列别名不适用，则返回列名称。 在这两种情况下，驱动程序在设置SQL_DESC_NAME字段时将SQL_DESC_UNNAMED字段设置为SQL_NAMED。 如果没有列名或列别名，驱动程序将返回SQL_DESC_NAME字段中的空字符串，并将SQL_DESC_UNNAMED字段设置为SQL_UNNAMED。  
  
 应用程序可以将 IPD 的SQL_DESC_NAME字段设置为参数名称或别名，以便按名称指定存储的过程参数。 （有关详细信息，请参阅[按名称（命名参数）绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。IRD 的SQL_DESC_NAME字段是只读字段;如果应用程序尝试设置 SQLSTATE HY091（无效描述符字段标识符），将返回它。  
  
 在 ID 中，如果驱动程序不支持命名参数，则此字段未定义。 如果驱动程序支持命名参数并能够描述参数，则参数名称将在此字段中返回。  
  
 **SQL_DESC_NULLABLE [实现描述符]**  
 在 IRD 中，如果列可以具有 NULL 值，则此只读 SQLSMALLINT 记录字段SQL_NULLABLE，如果列没有 NULL 值，则SQL_NO_NULLS列是否具有 NULL 值，或者如果不知道列是否接受 NULL 值，则SQL_NULLABLE_UNKNOWN。 此字段与结果集列相关，而不是与基本列相关。  
  
 在 IID 中，此字段始终设置为SQL_NULLABLE，因为动态参数始终为空，并且不能由应用程序设置。  
  
 **SQL_DESC_NUM_PREC_RADIX [全部]**  
 如果SQL_DESC_TYPE字段中的数据类型是近似数值数据类型，则此 SQLINTEGER 字段包含值 2，因为SQL_DESC_PRECISION字段包含位数。 如果SQL_DESC_TYPE字段中的数据类型是精确数字数据类型，则此字段包含值 10，因为SQL_DESC_PRECISION字段包含小数位数。 此字段设置为 0，用于所有非数字数据类型。  
  
 **SQL_DESC_OCTET_LENGTH [全部]**  
 此 SQLLEN 记录字段包含字符串或二进制数据类型的长度（以字节为单位）。 对于固定长度字符或二进制类型，这是以字节为单位的实际长度。 对于可变长度字符或二进制类型，这是以字节为单位的最大长度。 此值始终排除实现描述符的 null 终止字符的空间，并且始终包含应用程序描述符的 null 终止字符的空间。 对于应用程序数据，此字段包含缓冲区的大小。 对于 AD，此字段仅为输出或输入/输出参数定义。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [应用程序描述符]**  
 此 SQLLEN = 记录字段指向一个变量，该变量将包含动态参数（对于参数描述符）或绑定列值（对于行描述符）的总长度。  
  
 对于 APD，除字符串和二进制之外的所有参数，此值都将被忽略;如果此字段指向SQL_NTS，则动态参数必须为 null 终止。 为了指示绑定参数将是执行时的数据参数，应用程序将 APD 的适当记录中的此字段设置为变量，在执行时，该变量将包含值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的结果。 如果有多个此类字段，则可以将SQL_DESC_DATA_PTR设置为唯一标识参数的值，以帮助应用程序确定请求的参数。  
  
 如果 ARD 的OCTET_LENGTH_PTR字段为空指针，则驱动程序不会返回列的长度信息。 如果 APD 的SQL_DESC_OCTET_LENGTH_PTR字段为空指针，则驱动程序假定字符串和二进制值为 null 终止。 （二进制值不应为 null 终止，而应为长度指定以避免截断。  
  
 如果对**SQLFetch**或**SQLFetchScroll**的调用填充此字段指向的缓冲区未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则缓冲区的内容未定义。 此字段是*递延字段*。 它在设置时不使用，但驱动程序稍后使用它来确定或指示数据的八进制长度。  
  
 **SQL_DESC_PARAMETER_TYPE [IPD]**  
 此 SQLSMALLINT 记录字段设置为输入参数SQL_PARAM_INPUT、输入/输出参数SQL_PARAM_INPUT_OUTPUT、输出参数SQL_PARAM_OUTPUT、输入/输出流参数SQL_PARAM_INPUT_OUTPUT_STREAM或输出流参数的SQL_PARAM_OUTPUT_STREAM。 默认情况下，它设置为SQL_PARAM_INPUT。  
  
 对于 IPD，如果驱动程序未自动填充 IPD（SQL_ATTR_ENABLE_AUTO_IPD语句属性SQL_FALSE），则默认情况下，该字段设置为SQL_PARAM_INPUT。 应用程序应在 IPD 中为不是输入参数的参数设置此字段。  
  
 **SQL_DESC_PRECISION [全部]**  
 此 SQLSMALLINT 记录字段包含精确数值类型的位数、近似数值类型的 mantissa 中的位数（二进制精度），或SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP 或SQL_INTERVAL_SECOND数据类型的小数秒分量中的位数。 此字段对于所有其他数据类型未定义。  
  
 此字段中的值可能与 ODBC 2 *.x*中定义的"精度"值不同。 有关详细信息，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [实现描述符]**  
 此 SQLSMALLINTrecord 字段指示在更新行时 DBMS 是否自动修改列（例如，SQL Server 中类型"时间戳"类型的列）。 如果列是行版本控制列，则此记录字段的值设置为SQL_TRUE，否则SQL_FALSE。 此列属性类似于使用SQL_ROWVER标识符类型调用**SQL 特别列**，以确定列是否自动更新。  
  
 **SQL_DESC_SCALE [全部]**  
 此 SQLSMALLINT 记录字段包含小数点和数字数据类型的已定义比例。 对于所有其他数据类型，该字段未定义。  
  
 此字段中的值可能与 ODBC 2 *.x*中定义的"缩放"值不同。 有关详细信息，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [红外指示]**  
 此只读 SQLCHAR = 记录字段包含包含列的基表的架构名称。 如果列是表达式或列是视图的一部分，则返回值与驱动程序相关。 如果数据源不支持架构或无法确定架构名称，则此变量包含一个空字符串。  
  
 **SQL_DESC_SEARCHABLE [红外点]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   如果列不能在**WHERE**子句中使用，则SQL_PRED_NONE。 （这与 ODBC 2 *.x 中的*SQL_UNSEARCHABLE值相同。  
  
-   SQL_PRED_CHAR该列是否可以在**WHERE**子句中使用，但只能与**LIKE**谓词一起使用。 （这与 ODBC 2 *.x 中的*SQL_LIKE_ONLY值相同。  
  
-   SQL_PRED_BASIC该列是否可以在**WHERE**子句中使用，与除**LIKE**之外的所有比较运算符。 （这与 ODBC 2 *.x 中的*SQL_EXCEPT_LIKE值相同。  
  
-   SQL_PRED_SEARCHABLE该列是否可以在任何比较运算符的**WHERE**子句中使用。  
  
 **SQL_DESC_TABLE_NAME [IRD]**  
 此只读 SQLCHAR = 记录字段包含包含此列的基表的名称。 如果列是表达式或列是视图的一部分，则返回值与驱动程序相关。  
  
 **SQL_DESC_TYPE [全部]**  
 此 SQLSMALLINT 记录字段指定除日期时间和间隔数据类型之外的所有数据类型的简明 SQL 或 C 数据类型。 对于日期时间和间隔数据类型，此字段指定SQL_DATETIME或SQL_INTERVAL的详细数据类型。  
  
 每当此字段包含SQL_DATETIME或SQL_INTERVAL时，SQL_DESC_DATETIME_INTERVAL_CODE字段必须包含简洁类型的相应子代码。 对于日期时间数据类型，SQL_DESC_TYPE包含SQL_DATETIME，并且SQL_DESC_DATETIME_INTERVAL_CODE字段包含特定日期时间数据类型的子代码。 对于间隔数据类型，SQL_DESC_TYPE包含SQL_INTERVAL，并且SQL_DESC_DATETIME_INTERVAL_CODE字段包含特定间隔数据类型的子代码。  
  
 SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE字段中的值是相互依赖的。 每次设置其中一个字段时，还必须设置另一个字段。 SQL_DESC_TYPE可以通过调用**SQLSetDescField**或**SQLSetDescRec**来设置。 SQL_DESC_CONCISE_TYPE可以通过调用**SQLBindCol**或**SQLBind参数**（或**SQLSetDescField）** 来设置。  
  
 如果SQL_DESC_TYPE设置为间隔或日期时间数据类型以外的简明数据类型，则SQL_DESC_CONCISE_TYPE字段设置为相同的值，SQL_DESC_DATETIME_INTERVAL_CODE字段设置为 0。  
  
 如果SQL_DESC_TYPE设置为详细日期时间或间隔数据类型（SQL_DATETIME 或SQL_INTERVAL），并且SQL_DESC_DATETIME_INTERVAL_CODE字段设置为相应的子代码，则SQL_DESC_CONCISE TYPE 字段设置为相应的简洁类型。 尝试将SQL_DESC_TYPE设置为其中一个简洁的日期时间或间隔类型将返回 SQLSTATE HY021（描述符信息不一致）。  
  
 当SQL_DESC_TYPE字段由对**SQLBindCol、SQLBind****参数**或**SQLSetDescField**的调用设置时，以下字段将设置为以下默认值，如下表所示。 未定义同一记录的剩余字段的值。  
  
|SQL_DESC_TYPE值|其他字段隐式设置|  
|------------------------------|---------------------------------|  
|SQL_CHAR、SQL_VARCHAR、SQL_C_CHAR、SQL_C_VARCHAR|SQL_DESC_LENGTH设置为 1。 SQL_DESC_PRECISION设置为 0。|  
|SQL_DATETIME|当SQL_DESC_DATETIME_INTERVAL_CODE设置为SQL_CODE_DATE或SQL_CODE_TIME时，SQL_DESC_PRECISION设置为 0。 当它设置为SQL_DESC_TIMESTAMP时，SQL_DESC_PRECISION设置为 6。|  
|SQL_DECIMAL，SQL_NUMERIC，SQL_C_NUMERIC|SQL_DESC_SCALE设置为 0。 SQL_DESC_PRECISION设置为相应数据类型的实现定义的精度。<br /><br /> 有关如何手动绑定SQL_C_NUMERIC值的信息，请参阅[SQL 到 C：数字](../../../odbc/reference/appendixes/sql-to-c-numeric.md)。|  
|SQL_FLOAT，SQL_C_FLOAT|SQL_DESC_PRECISION设置为SQL_FLOAT的实现定义的默认精度。|  
|SQL_INTERVAL|当SQL_DESC_DATETIME_INTERVAL_CODE设置为间隔数据类型时，SQL_DESC_DATETIME_INTERVAL_PRECISION设置为 2（默认间隔前导精度）。 当间隔具有秒分量时，SQL_DESC_PRECISION设置为 6（默认间隔秒精度）。|  
  
 当应用程序调用**SQLSetDescField**来设置描述符的字段，而不是调用**SQLSetDescRec**时，应用程序必须首先声明数据类型。 当它这样做时，上一个表中指示的其他字段将隐式设置。 如果隐式设置的任何值是不可接受的，则应用程序可以调用**SQLSetDescField**或**SQLSetDescRec**显式设置不可接受的值。  
  
 **SQL_DESC_TYPE_NAME [实现描述符]**  
 此只读 SQLCHAR = 记录字段包含与数据源相关的类型名称（例如，"CHAR"、"VARCHAR"等）。 如果数据类型名称未知，则此变量包含一个空字符串。  
  
 **SQL_DESC_UNNAMED [实现描述符]**  
 行描述符中的此 SQLSMALLINT 记录字段由驱动程序设置为SQL_NAMED或SQL_UNNAMED设置SQL_DESC_NAME字段时。 如果SQL_DESC_NAME字段包含列别名，或者列别名不适用，则驱动程序将SQL_DESC_UNNAMED字段设置为SQL_NAMED。 如果应用程序将 IPD 的SQL_DESC_NAME字段设置为参数名称或别名，则驱动程序将 IPD 的SQL_DESC_UNNAMED字段设置为SQL_NAMED。 如果没有列名称或列别名，驱动程序将SQL_DESC_UNNAMED字段设置为SQL_UNNAMED。  
  
 应用程序可以将 IPD 的SQL_DESC_UNNAMED字段设置为SQL_UNNAMED。 如果应用程序尝试将 IPD 的SQL_DESC_UNNAMED字段设置为SQL_NAMED，则驱动程序将返回 SQLSTATE HY091（无效描述符字段标识符）。 IRD 的SQL_DESC_UNNAMED字段是只读的;如果应用程序尝试设置 SQLSTATE HY091（无效描述符字段标识符），将返回它。  
  
 **SQL_DESC_UNSIGNED [实现描述符]**  
 如果列类型未签名或非数字，则此只读 SQLSMALLINT 记录字段设置为SQL_TRUE，如果列类型已签名，则SQL_FALSE。  
  
 **SQL_DESC_UPDATABLE [红外点]**  
 此只读 SQLSMALLINT 记录字段设置为以下值之一：  
  
-   如果结果集列是只读的，SQL_ATTR_READ_ONLY。  
  
-   如果结果集列是读写列，SQL_ATTR_WRITE。  
  
-   如果不知道结果集列是否可更新，SQL_ATTR_READWRITE_UNKNOWN。  
  
 SQL_DESC_UPDATABLE描述结果集中列的升数据度，而不是基表中的列。 此结果集列所基于的基表中列的升数据度可能与此字段中的值不同。 列是否可更新可以基于数据类型、用户权限和结果集本身的定义。 如果不清楚列是否可更新，则应返回SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性检查  
 每当应用程序通过 ARD、APD 或 IPD SQL_DESC_DATA_PTR字段的值时，驱动程序会自动执行一致性检查。 如果任何字段与其他字段不一致 **，SQLSetDescField**将返回 SQLSTATE HY021（描述符信息不一致）。 有关详细信息，请参阅[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的"一致性检查"。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|绑定参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)
