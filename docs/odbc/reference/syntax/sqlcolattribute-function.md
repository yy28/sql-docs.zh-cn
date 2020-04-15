---
title: SQLCol属性函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94de3dfc7036277f8be56c401326cdab07a9606
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301287"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLColAttribute**返回结果集中列的描述符信息。 描述符信息将作为字符串、描述符相关值或整数值返回。  
  
> [!NOTE]  
>  有关驱动程序管理器将此功能映射到 ODBC 3 时的详细信息。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射应用程序向后兼容性的替代函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 ColumnNumber   
 [输入]要从中检索字段值的 IRD 中的记录数。 此参数对应于结果数据的列数，按增加列顺序顺序排序，从 1 开始。 列可以按任意顺序描述。  
  
 列 0 可以在此参数中指定，但除SQL_DESC_TYPE和SQL_DESC_OCTET_LENGTH之外的所有值都将返回未定义的值。  
  
 *FieldIdentifier*  
 [输入]描述符句柄。 此句柄定义应查询 IRD 中的哪个字段（例如，SQL_COLUMN_TABLE_NAME）。  
  
 *CharacterAttributePtr*  
 [输出]指针指向要返回 IRD*的"列编号*"行*的字段标识符*字段中的值的缓冲区，如果该字段是字符串。 否则，该字段将未使用。  
  
 如果*字符属性Ptr*为 NULL，*则 StringLengthPtr*仍将返回字符*属性Ptr*指向的缓冲区中可用于返回的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*Field标识符*是 ODBC 定义的字段，而*字符属性Ptr*指向字符串或二进制缓冲区，则此参数应为\**字符属性Ptr*的长度。 如果*字段标识符*是 ODBC 定义的字段，\*而*字符属性*Ptr 是整数，则忽略此字段。 如果*\*字符属性Ptr*是 Unicode 字符串（在调用**SQLColAttributeW**时），*缓冲区长度*参数必须是偶数。 如果*Field标识符*是驱动程序定义的字段，则应用程序通过设置*BufferLength*参数向驱动程序管理器指示该字段的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*字符属性Ptr*是指向指针的指针，*则缓冲区长度*应具有SQL_IS_POINTER值。  
  
-   如果*字符属性Ptr*是指向字符串的指针，则*缓冲区长度*是缓冲区的长度。  
  
-   如果*字符属性Ptr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*字符属性Ptr*是指向固定长度数据类型的指针，*则缓冲区长度*必须是以下类型之一：SQL_IS_INTEGER、SQL_IS_UNINTEGER、SQL_SMALLINT 或 SQLUSMALLINT。  
  
 *字符串长度 Ptr*  
 [输出]指向一个缓冲区的指针，其中返回可用于在 #*字符属性Ptr*中返回的字节总数（不包括字符数据的空终止字节）。  
  
 对于字符数据，如果可供返回的字节数大于或等于*BufferLength，*\**则字符属性Ptr*中的描述符信息将被截断为*BufferLength*减去空终止字符的长度，并且由驱动程序终止。  
  
 对于所有其他类型的数据，将忽略*BufferLength*的值，驱动程序假定 #*字符属性Ptr*的大小为 32 位。  
  
 *数字属性Ptr*  
 [输出]指针指向整数缓冲区，用于在其中返回 IRD*的"列编号*"行的*字段标识符*字段中的值，如果该字段是数字描述符类型（如SQL_DESC_COLUMN_LENGTH）。 否则，该字段将未使用。 请注意，某些驱动程序可能只写入缓冲区的下 32 位或 16 位，并且保持高阶位不变。 因此，应用程序在调用此函数之前应初始化该值为 0。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColAttribute**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT*Handle*的*句柄类型*和*语句句柄*。 下表列出了**SQLColAttribute**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\**字符属性Ptr*不够大，无法返回整个字符串值，因此字符串值被截断。 未压缩字符串值的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07005|已准备好的语句不是*游标规范*|与*语句句柄*关联的语句未返回结果集，*并且字段标识符*未SQL_DESC_COUNT。 没有要描述的列。|  
|07009|无效描述符索引|（DM） 为*列编号*指定的值等于 0，并且SQL_ATTR_USE_BOOKMARKS语句属性SQL_UB_OFF。<br /><br /> 为参数*ColumnNumber*指定的值大于结果集中的列数。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagField**从诊断数据结构返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQLColAttribute 时，此 aynchronous 函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 在调用**SQLPrepare、SQLExecDirect**或*语句句柄*的目录函数之前调用函数。 **SQLPrepare**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM）*\*字符属性Ptr*是一个字符字符串，*缓冲区长度*小于 0 但不等于SQL_NTS。|  
|HY091|无效描述符字段标识符|为参数*FieldIdentifier*指定的值不是定义的值之一，不是实现定义的值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|驱动程序无法|驱动程序不支持为参数*字段标识符*指定的值。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
 在**SQLPrepare**之后和**SQLExecute**之前调用时 **，SQLColAttribute**可以返回**SQLPrepare**或**SQLExecute**可以返回的任何 SQLSTATE，具体取决于数据源何时计算与*语句句柄*关联的 SQL 语句。  
  
 出于性能原因，应用程序在执行语句之前不应调用**SQLColAttribute。**  
  
## <a name="comments"></a>注释  
 有关应用程序如何使用**SQLColAttribute**返回的信息的信息，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**返回\**数字属性Ptr*或\**字符属性Ptr*中的信息。 整数信息在\**数字属性Ptr*中作为 SQLLEN 值返回;所有其他格式的信息都返回在\**字符属性Ptr*中。 在\**数字属性Ptr*中返回信息时，驱动程序将忽略*字符属性Ptr、**缓冲区长度*和*字符串长度Ptr*。 当在\**字符属性Ptr*中返回信息时，驱动程序将忽略*数字属性Ptr*。  
  
 **SQLColAttribute**从 IRD 的描述符字段返回值。 函数使用语句句柄而不是描述符句柄调用。 **SQLColAttribute**为本节后面列出的*字段标识符*值返回的值也可以通过使用适当的 IRD 句柄调用**SQLGetDescField**来检索。  
  
 当前定义的描述符字段、引入它们的 ODBC 版本以及为其返回信息的参数在本节的后面部分显示;驱动程序可以定义更多的描述符类型，以利用不同的数据源。  
  
 ODBC 3.*x*驱动程序必须为每个描述符字段返回一个值。 如果描述符字段不适用于驱动程序或数据源，除非另有说明，否则驱动程序在\**StringLengthPtr*中返回 0 或在 #*字符属性Ptr*中返回一个空字符串。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3.*x*函数**SQLColAttribute**替换已弃用的 ODBC 2。*x*函数**SQLColattributes**。 将**SQLColattributes**映射到**SQLColattribute**时（当 ODBC 2 时）。*x*应用程序使用 ODBC 3。*x*驱动程序），或将**SQLColattribute**映射到**SQLColattributes（** 当 ODBC 3 时）。*x*应用程序使用 ODBC 2。*x*驱动程序），驱动程序管理器传递*字段标识符*的值，将其映射到新值，或返回错误，如下所示：  
  
> [!NOTE]  
>  ODBC 3 中*字段标识符*值中使用的前缀。*x*已从 ODBC 2 中使用的更改。*x*. . 新前缀为"SQL_DESC";新前缀为"SQL_DESC";如果 "SQL_DESC"，则为"SQL_DESC"旧前缀为"SQL_COLUMN"。  
  
-   如果 **#define** ODBC 2 的值。*x* *字段标识符*与 ODBC 3**的#define**值相同。*x* *字段标识符*，函数调用中的值刚刚传递。  
  
-   ODBC 2**的值#define。***x* *字段标识符*SQL_COLUMN_LENGTH、SQL_COLUMN_PRECISION和SQL_COLUMN_SCALE与 ODBC 3**的#define**值不同。*x* *字段标识符*SQL_DESC_PRECISION、SQL_DESC_SCALE 和SQL_DESC_LENGTH。 ODBC 2.*x*驱动程序仅支持 ODBC 2。*x*值。 ODBC 3.*x*驱动程序必须同时支持这三个*字段标识符*的"SQL_COLUMN"和"SQL_DESC"值。 这些值不同，因为在 ODBC 3 中定义精度、比例和长度的方式不同。*x*比在ODBC 2中。*x*. . 有关详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果 **#define** ODBC 2 的值。*x* *字段标识符*不同于 ODBC 3**的#define**值。*x* *字段标识符*，与 COUNT、NAME 和 NULLABLE 值一样，函数调用中的值映射到相应的值。 例如，SQL_COLUMN_COUNT映射到SQL_DESC_COUNT，并且SQL_DESC_COUNT映射到SQL_COLUMN_COUNT，具体取决于映射的方向。  
  
-   如果*字段标识符*是 ODBC 3 中的新值。*x*，ODBC 2 中没有相应的值。*x*，当 ODBC 3 时不会映射它。*x*应用程序在 ODBC 2 中调用**SQLColAttribute**时使用它。*x*驱动程序，并且调用将返回 SQLSTATE HY091（无效描述符字段标识符）。  
  
 下表列出了**SQLColAttribute**返回的描述符类型。 *数字属性Ptr*值的类型是**SQLLEN \* **。  
  
|*FieldIdentifier*|信息<br /><br /> 返回|描述|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE （ODBC 1.0）|*数字属性Ptr*|如果列是自动递增列，则SQL_TRUE。<br /><br /> 如果列不是自动增量列或不是数字，则SQL_FALSE。<br /><br /> 此字段仅适用于数字数据类型列。 应用程序可以将值插入到包含自动增量列的行中，但通常无法更新列中的值。<br /><br /> 当将插入到自动增量列中时，在插入时将一个唯一值插入到列中。 增量未定义，但特定于数据源。 应用程序不应假定自动增量列从任何特定点开始，或由任何特定值增量。|  
|SQL_DESC_BASE_COLUMN_NAME （ODBC 3.0）|*CharacterAttributePtr*|结果集列的基本列名称。 如果基本列名称不存在（如表达式的列），则此变量包含一个空字符串。<br /><br /> 此信息从 IRD 的SQL_DESC_BASE_COLUMN_NAME记录字段返回，该记录字段是只读字段。|  
|SQL_DESC_BASE_TABLE_NAME （ODBC 3.0）|*CharacterAttributePtr*|包含列的基表的名称。 如果无法定义基表名称或不适用，则此变量包含一个空字符串。<br /><br /> 此信息从 IRD 的SQL_DESC_BASE_TABLE_NAME记录字段返回，该记录字段是只读字段。|  
|SQL_DESC_CASE_SENSITIVE （ODBC 1.0）|*数字属性Ptr*|SQL_TRUE该列是否被视为区分大小写（用于排序和比较）。<br /><br /> SQL_FALSE如果列不被视为区分大小写（用于排序规则和比较）或非字符。|  
|SQL_DESC_CATALOG_NAME （ODBC 2.0）|*CharacterAttributePtr*|包含列的表的目录。 如果列是表达式或列是视图的一部分，则返回的值是实现定义的。 如果数据源不支持目录或无法确定目录名称，则返回一个空字符串。 此 VARCHAR 记录字段不限于 128 个字符。|  
|SQL_DESC_CONCISE_TYPE （ODBC 1.0）|*数字属性Ptr*|简洁的数据类型。<br /><br /> 对于日期时间和间隔数据类型，此字段返回简洁的数据类型;例如，SQL_TYPE_TIME或SQL_INTERVAL_YEAR。 （有关详细信息，请参阅附录 D 中的[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)：数据类型。<br /><br /> 此信息从 IRD 的SQL_DESC_CONCISE_TYPE记录字段返回。|  
|SQL_DESC_COUNT （ODBC 1.0）|*数字属性Ptr*|结果集中可用的列数。 如果结果集中没有列，则返回 0。 将忽略*列编号*参数中的值。<br /><br /> 此信息从 IRD 的SQL_DESC_COUNT标头字段返回。|  
|SQL_DESC_DISPLAY_SIZE （ODBC 1.0）|*数字属性Ptr*|显示列中数据所需的最大字符数。 有关显示大小的详细信息，请参阅附录 D：数据类型中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|SQL_DESC_FIXED_PREC_SCALE （ODBC 1.0）|*数字属性Ptr*|如果列具有特定于数据源的固定精度和非零比例，SQL_TRUE。<br /><br /> 如果列没有特定于数据源的固定精度和非零比例，则SQL_FALSE。|  
|SQL_DESC_LABEL （ODBC 2.0）|*CharacterAttributePtr*|列标签或标题。 例如，名为 EmpName 的列可能标记为"员工姓名"，或者可能标有别名。<br /><br /> 如果列没有标签，则返回列名称。 如果列未标记且未命名，则返回一个空字符串。|  
|SQL_DESC_LENGTH （ODBC 3.0）|*数字属性Ptr*|一个数值，它是字符串或二进制数据类型的最大或实际字符长度。 它是固定长度数据类型的最大字符长度，或可变长度数据类型的实际字符长度。 其值始终排除结束字符串的空终止字节。<br /><br /> 此信息从 IRD 的SQL_DESC_LENGTH记录字段返回。<br /><br /> 有关长度的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|SQL_DESC_LITERAL_PREFIX （ODBC 3.0）|*CharacterAttributePtr*|此 VARCHAR（128） 记录字段包含驱动程序识别为此数据类型文本的前缀的字符。 此字段包含不适用于文本前缀的数据类型的空字符串。 有关详细信息，请参阅[文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX （ODBC 3.0）|*CharacterAttributePtr*|此 VARCHAR（128） 记录字段包含驱动程序识别为此数据类型文本的后缀的字符或字符。 此字段包含不适用于文本后缀的数据类型的空字符串。 有关详细信息，请参阅[文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME （ODBC 3.0）|*CharacterAttributePtr*|此 VARCHAR（128） 记录字段包含数据类型可能与数据类型的常规名称不同的任何本地化（母语）名称。 如果没有本地化名称，则返回一个空字符串。 此字段仅用于显示目的。 字符串的字符集与区域设置相关，通常是服务器的默认字符集。|  
|SQL_DESC_NAME （ODBC 3.0）|*CharacterAttributePtr*|列别名（如果适用）。 如果列别名不适用，则返回列名称。 在这两种情况下，SQL_DESC_UNNAMED设置为SQL_NAMED。 如果没有列名或列别名，则返回一个空字符串，并将SQL_DESC_UNNAMED设置为SQL_UNNAMED。<br /><br /> 此信息从 IRD SQL_DESC_NAME记录字段返回。|  
|SQL_DESC_NULLABLE （ODBC 3.0）|*数字属性Ptr*|如果列可以具有 NULL 值，则SQL_ NULLABLE;如果列没有 NULL 值，则SQL_NO_NULLS;如果列没有 NULL 值，则为或SQL_NULLABLE_UNKNOWN如果不知道列是否接受 NULL 值。<br /><br /> 此信息从 IRD 的SQL_DESC_NULLABLE记录字段返回。|  
|SQL_DESC_NUM_PREC_RADIX （ODBC 3.0）|*数字属性Ptr*|如果SQL_DESC_TYPE字段中的数据类型是近似数值数据类型，则此 SQLINTEGER 字段包含值 2，因为SQL_DESC_PRECISION字段包含位数。 如果SQL_DESC_TYPE字段中的数据类型是精确的数字数据类型，则此字段包含值 10，因为SQL_DESC_PRECISION字段包含小数位数。 此字段设置为 0，用于所有非数字数据类型。|  
|SQL_DESC_OCTET_LENGTH （ODBC 3.0）|*数字属性Ptr*|字符串或二进制数据类型的长度（以字节为单位）。 对于固定长度字符或二进制类型，这是以字节为单位的实际长度。 对于可变长度字符或二进制类型，这是以字节为单位的最大长度。 此值不包括空终止符。<br /><br /> 此信息从 IRD 的SQL_DESC_OCTET_LENGTH记录字段返回。<br /><br /> 有关长度的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|SQL_DESC_PRECISION （ODBC 3.0）|*数字属性Ptr*|数字数据类型表示适用精度的数值。 对于SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP和所有表示时间间隔的间隔数据类型，其值是小数秒组件的适用精度。<br /><br /> 此信息从 IRD SQL_DESC_PRECISION记录字段返回。|  
|SQL_DESC_SCALE （ODBC 3.0）|*数字属性Ptr*|数值，是数值数据类型的适用比例。 对于 DECIMAL 和数字数据类型，这是定义的比例。 它是未定义的所有其他数据类型。<br /><br /> 此信息从 IRD 的 SCALE 记录字段返回。|  
|SQL_DESC_SCHEMA_NAME （ODBC 2.0）|*CharacterAttributePtr*|包含列的表的架构。 如果列是表达式或列是视图的一部分，则返回的值是实现定义的。 如果数据源不支持架构或无法确定架构名称，则返回一个空字符串。 此 VARCHAR 记录字段不限于 128 个字符。|  
|SQL_DESC_SEARCHABLE （ODBC 1.0）|*数字属性Ptr*|如果列不能在 WHERE 子句中使用，则SQL_PRED_NONE。 （这与 ODBC 2 中的SQL_UNSEARCHABLE值相同。*x*.）<br /><br /> SQL_PRED_CHAR该列是否可以在 WHERE 子句中使用，但只能与 LIKE 谓词一起使用。 （这与 ODBC 2 中的SQL_LIKE_ONLY值相同。*x*.）<br /><br /> SQL_PRED_BASIC该列是否可以在 WHERE 子句中使用，所有比较运算符（LIKE 除外）。 （这与 ODBC 2 中的SQL_EXCEPT_LIKE值相同。*x*.）<br /><br /> SQL_PRED_SEARCHABLE该列是否可以在任何比较运算符的 WHERE 子句中使用。<br /><br /> 类型SQL_LONGVARCHAR和SQL_LONGVARBINARY的列通常返回SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME （ODBC 2.0）|*CharacterAttributePtr*|包含该列的表的名称。 如果列是表达式或列是视图的一部分，则返回的值是实现定义的。<br /><br /> 如果无法确定表名称，则返回一个空字符串。|  
|SQL_DESC_TYPE （ODBC 3.0）|*数字属性Ptr*|指定 SQL 数据类型的数值。<br /><br /> 当*列号*等于 0 时，将返回可变长度书签SQL_BINARY，并为固定长度书签返回SQL_INTEGER。<br /><br /> 对于日期时间和间隔数据类型，此字段返回详细数据类型：SQL_DATETIME或SQL_INTERVAL。 （有关详细信息，请参阅附录 D 中的[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)：数据类型。<br /><br /> 此信息从 IRD SQL_DESC_TYPE记录字段返回。 **注：** 对抗 ODBC 2。*x*驱动程序，而是使用SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME （ODBC 1.0）|*CharacterAttributePtr*|与数据源相关的数据类型名称;例如，"CHAR"，"VARCHAR"，"金钱"，"长VARBINARY"，或"CHAR （ ） BIT 数据"。<br /><br /> 如果类型未知，则返回一个空字符串。|  
|SQL_DESC_UNNAMED （ODBC 3.0）|*数字属性Ptr*|SQL_NAMED或SQL_UNNAMED。 如果 IRD 的SQL_DESC_NAME字段包含列别名或列名称，则返回SQL_NAMED。 如果没有列名称或列别名，则返回SQL_UNNAMED。<br /><br /> 此信息从 IRD 的SQL_DESC_UNNAMED记录字段返回。|  
|SQL_DESC_UNSIGNED （ODBC 1.0）|*数字属性Ptr*|如果列是无符号的（或不是数字），SQL_TRUE。<br /><br /> 如果对列进行签名，则SQL_FALSE。|  
|SQL_DESC_UPDATABLE （ODBC 1.0）|*数字属性Ptr*|列由定义的常量的值描述：<br /><br /> SQL_ATTR_READONLYSQL_ATTR_WRITESQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE描述结果集中列的升数据度，而不是基表中的列。 结果集列所基于的基础列的升数据度可能与此字段中的值不同。 列是否可更新可以基于数据类型、用户权限和结果集本身的定义。 如果不清楚列是否可更新，则应返回SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**是**SQLDescribeCol**的可扩展替代方法。 **SQLDescribeCol**返回一组基于 ANSI-89 SQL 的固定描述符信息。 **SQLColAttribute**允许访问 ANSI SQL-92 和 DBMS 供应商扩展中提供的更广泛的描述符信息集。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>示例  
 以下示例代码不释放句柄和连接。 有关代码示例以释放句柄和语句，请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)、[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)和[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
