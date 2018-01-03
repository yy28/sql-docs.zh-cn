---
title: "SQLColAttribute 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLColAttribute
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLColAttribute
helpviewer_keywords: SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7470412149bf336be8d07495eab4aa9bdf449a86
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLColAttribute**返回结果集中的列的描述符信息。 为字符字符串、 一个依赖于描述符的值或一个整数值返回描述符信息。  
  
> [!NOTE]  
>  有关详细信息有关哪些驱动程序管理器时，将映射此函数可对 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射用于向后兼容性的应用程序的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ColumnNumber*  
 [输入]IRD 是要检索的字段值中的记录数。 此参数对应于结果数据，按不断增加的列顺序，从 1 开始按顺序排序的列号。 可以按任意顺序描述列。  
  
 第 0 列可以指定此参数，但除 SQL_DESC_TYPE 和 SQL_DESC_OCTET_LENGTH 以外的所有值都将都返回未定义的值。  
  
 *FieldIdentifier*  
 [输入]描述符句柄。 此句柄定义 IRD 中的哪个字段应查询 （例如 SQL_COLUMN_TABLE_NAME）。  
  
 *CharacterAttributePtr*  
 [输出]指向在其返回中的值的缓冲区的指针*FieldIdentifier*字段*ColumnNumber* IRD，如果字段为字符串的行。 否则，该字段为未使用。  
  
 如果*CharacterAttributePtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回在缓冲区中指向*CharacterAttributePtr*。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*CharacterAttributePtr*指向的字符串或二进制缓冲区时，此参数应为的长度\* *CharacterAttributePtr*。 如果*FieldIdentifier*是一个 ODBC 定义的字段和\* *CharacterAttribute*Ptr 是一个整数，则会忽略此字段。 如果 *\*CharacterAttributePtr*为 Unicode 字符串 (在调用时**SQLColAttributeW**)，则*BufferLength*参数必须为偶数。 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指明字段到驱动程序管理器的性质*BufferLength*自变量。 *BufferLength*可以具有下列值：  
  
-   如果*CharacterAttributePtr*是一个指针，指向*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*CharacterAttributePtr*是指向字符串， *BufferLength*是缓冲区的长度。  
  
-   如果*CharacterAttributePtr* SQL_LEN_BINARY_ATTR 的结果是指向二进制缓冲区中，应用程序位置的指针 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*CharacterAttributePtr*是为固定长度的数据类型，指针*BufferLength*必须是以下之一： SQL_IS_INTEGER、 SQL_IS_UNINTEGER、 SQL_SMALLINT 或 SQLUSMALLINT。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括字符数据的 null 终止字节） 的字节总数在其中缓冲区的指针可用于返回在 **CharacterAttributePtr*。  
  
 对于字符数据，可用于返回的字节数是否大于或等于*BufferLength*中的描述符信息\* *CharacterAttributePtr*截断为*BufferLength* null 终止字符的长度减和是由驱动程序以 null 结尾。  
  
 对于所有其他类型的数据的值*BufferLength*将被忽略，并且该驱动程序假定的大小 **CharacterAttributePtr*为 32 位。  
  
 *NumericAttributePtr*  
 [输出]到整数缓冲区中要返回中的值的指针*FieldIdentifier*字段*ColumnNumber* IRD，如果字段是一个数值描述符类型，例如 SQL_DESC_COLUMN_LENGTH 行。 否则，该字段为未使用。 请注意，某些驱动程序可能仅编写较低的 32 位或 16 位的缓冲区，并保留较高顺序位保持不变。 因此，应用程序应调用此函数之前初始化为 0 的值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColAttribute**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可能会通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLColAttribute**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *CharacterAttributePtr*不是否足够大以返回整个字符串值中，因此该字符串值被截断。 在中返回未截断的字符串值的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07005|不准备语句*光标规范*|与相关的语句*StatementHandle*未返回结果集和*FieldIdentifier*未 SQL_DESC_COUNT。 未描述的列。|  
|07009|无效的描述符索引|(DM) 为指定的值*ColumnNumber*等于 0，且 SQL_ATTR_USE_BOOKMARKS 语句属性为 SQL_UB_OFF。<br /><br /> 为参数指定的值*ColumnNumber*大于结果集中的列数。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagField**从诊断的数据结构描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 调用 SQLColAttribute 时仍在执行此 aynchronous 函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 在调用之前调用该函数**SQLPrepare**， **SQLExecDirect**，或为目录函数*StatementHandle*。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM)  *\*CharacterAttributePtr*是一个字符串，和*BufferLength*小于 0，但与 sql_nts 以不相等。|  
|HY091|描述符字段标识符无效|为参数指定的值*FieldIdentifier*未定义的值之一，且未实现定义的值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|驱动程序不可用|为参数指定的值*FieldIdentifier*驱动程序不支持。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
 当之后调用**SQLPrepare**和之前**SQLExecute**， **SQLColAttribute**可以返回可以由任何 SQLSTATE **SQLPrepare**或**SQLExecute**，取决于当数据源的计算结果与相关的 SQL 语句*StatementHandle*。  
  
 出于性能原因，应用程序不应调用**SQLColAttribute**之前执行语句。  
  
## <a name="comments"></a>注释  
 有关如何应用程序使用返回的信息信息**SQLColAttribute**，请参阅[结果设置元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**或者返回的信息在\* *NumericAttributePtr*或\* *CharacterAttributePtr*。 在中返回整数信息\* *NumericAttributePtr*作为 SQLLEN 值; 所有其他格式的信息中返回\* *CharacterAttributePtr*。 当在返回信息\* *NumericAttributePtr*，驱动程序将忽略*CharacterAttributePtr*， *BufferLength*，和*StringLengthPtr*。 当在返回信息\* *CharacterAttributePtr*，驱动程序将忽略*NumericAttributePtr*。  
  
 **SQLColAttribute**从 IRD 描述符字段返回值。 使用语句句柄，而不是的描述符句柄调用该函数。 返回的值**SQLColAttribute**为*FieldIdentifier*稍后在本部分中列出的值也可通过调用检索**SQLGetDescField**与适当 IRD 句柄。  
  
 当前定义的描述符字段，在其中引入了它们，并在本部分中; 更高版本显示在其中为其返回信息的自变量的 ODBC 版本可以由驱动程序以利用不同数据源中定义更多的描述符类型。  
  
 一个 ODBC 3。*x*驱动程序必须为每个描述符字段返回一个值。 如果描述符字段不适用于驱动程序或数据源和驱动程序除非另行说明，否则返回 0，在\* *StringLengthPtr*或空字符串中的 **CharacterAttributePtr*。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3。*x*函数**SQLColAttribute**替换不推荐使用的 ODBC 2。*x*函数**SQLColAttributes**。 映射时**SQLColAttributes**到**SQLColAttribute** (时 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序)，或映射**SQLColAttribute**到**SQLColAttributes** (时 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序)，或者驱动程序管理器的值传递*FieldIdentifier*通过，请将其映射到一个新值，或返回一个错误，，如下所示：  
  
> [!NOTE]  
>  中使用的前缀*FieldIdentifier* ODBC 3 中的值。*x*已从该中使用 ODBC 2。*x*。 新的前缀为"SQL_DESC";旧的前缀为"SQL_COLUMN"。  
  
-   如果**#define** ODBC 2 的值。*x* *FieldIdentifier*相同**#define** ODBC 3 的值。*x* *FieldIdentifier*，只需传递函数调用中的值。  
  
-   **#Define** ODBC 2 的值。*x* *FieldIdentifiers* SQL_COLUMN_LENGTH、 SQL_COLUMN_PRECISION 和 SQL_COLUMN_SCALE 是不同于**#define** ODBC 3 的值。*x* *FieldIdentifiers* SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_LENGTH。 一个 ODBC 2。*x*驱动程序需要仅支持 ODBC 2。*x*值。 一个 ODBC 3。*x*驱动程序必须支持这三个"SQL_COLUMN"和"SQL_DESC"值*FieldIdentifiers*。 因为精度、 小数位数和长度的定义有所不同 ODBC 3 中，这些值会不同。*x* ODBC 2 中相比。*x*。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果**#define** ODBC 2 的值。*x* *FieldIdentifier*不同于**#define** ODBC 3 的值。*x* *FieldIdentifier*、 一样会出现的计数，名称，并且可以为 NULL 值，函数调用中的值映射到相应的值。 例如，SQL_COLUMN_COUNT 映射到 SQL_DESC_COUNT，和 SQL_DESC_COUNT 映射到 SQL_COLUMN_COUNT，具体取决于映射的方向。  
  
-   如果*FieldIdentifier*是 ODBC 3 中的新值。*x*，为其时 ODBC 2 没有相应的值。*x*，它将不映射时 ODBC 3。*x*对的调用中的应用程序使用它**SQLColAttribute** ODBC 2 中。*x*驱动程序，并调用将返回 SQLSTATE HY091 （描述符字段标识符无效）。  
  
 下表列出了通过返回的描述符类型**SQLColAttribute**。 类型*NumericAttributePtr*值是**SQLLEN \*** 。  
  
|*FieldIdentifier*|信息<br /><br /> 在中返回|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|如果列是自动增量列，SQL_TRUE。<br /><br /> 如果列不是自动增量列或不是数值，SQL_FALSE。<br /><br /> 此字段为数值数据类型列的有效。 应用程序可以将值插入的行中包含自动递增的列，但通常不能更新列中的值。<br /><br /> 当插入将变成 autoincrement 列时，唯一的值将在插入时，插入到列。 增量未定义，但数据源 – 特定。 应用程序不应假定启动在任何特定点或增量的 autoincrement 列按任何特定值。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|列集结果的基列名称。 如果基列名称不存在 （如下所示的是表达式的列的情况下），此变量包含一个空字符串。<br /><br /> 从 IRD，这是只读字段的 SQL_DESC_BASE_COLUMN_NAME 记录字段返回此信息。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|包含的列的基表的名称。 如果基表名称不能定义，或不适用，则此变量包含一个空字符串。<br /><br /> 从 IRD，这是只读字段的 SQL_DESC_BASE_TABLE_NAME 记录字段返回此信息。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|如果列被处理为有关排序规则和比较区分大小写的 SQL_TRUE。<br /><br /> 如果列均不被视为排序规则和比较的区分大小写，或为非字符，SQL_FALSE。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含列的表的目录。 如果列是一个表达式，或者如果列是视图的一部分，则返回的值是实现定义。 如果数据源不支持目录或无法确定目录名称，则返回空字符串。 此 VARCHAR 记录字段不超过 128 个字符。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|简洁数据类型。<br /><br /> 对于日期时间和间隔数据类型，此字段会返回简洁数据类型;例如，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR。 (有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附录 d： 数据类型中。)<br /><br /> 从 IRD SQL_DESC_CONCISE_TYPE 记录字段返回此信息。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|在结果集中可用的列数。 如果结果集中没有列，这将返回 0。 中的值*ColumnNumber*忽略自变量。<br /><br /> 从 IRD SQL_DESC_COUNT 标头字段返回此信息。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|显示列中的数据所需的字符的最大数量。 有关显示大小的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|如果列是数据源 – 特定固定的精度和非零的小数位数，SQL_TRUE。<br /><br /> 如果列不具有数据源 – 特定固定的精度和非零的小数位数，SQL_FALSE。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|列标签或标题。 例如，一个名为 EmpName 列可能被标记为员工姓名或可能标有别名。<br /><br /> 如果列不具有标签，则返回的列名称。 如果列是未标记，未命名的则返回空字符串。|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|是一个数字值的最大值或实际的字符长度的字符字符串或二进制数据类型。 它是固定长度的数据类型的最大字符长度或可变长度数据类型的实际字符长度。 其值始终不包括结尾的字符串的 null 终止字节。<br /><br /> 从 IRD SQL_DESC_LENGTH 记录字段返回此信息。<br /><br /> 有关长度的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含的字符或驱动程序识别为此数据类型的文本的前缀的字符。 此字段包含的文本的前缀不适用的数据类型的空字符串。 有关详细信息，请参阅[文字前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含的字符或字符，则驱动程序识别为此数据类型的文本的后缀。 此字段包含的文本的后缀不是适用的数据类型的空字符串。 有关详细信息，请参阅[文字前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含可能与数据类型的正则名称不同的数据类型的任何本地化 （本机语言） 名称。 如果没有任何本地化的名称，则返回空字符串。 此字段为仅用于显示目的。 字符串的字符集与区域设置相关并通常是服务器的默认字符集。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|如果要将它应用作为列别名。 如果列别名不适用，则返回的列名称。 在任一情况下，SQL_DESC_UNNAMED 设为 SQL_NAMED。 如果没有任何列名称或列别名，则返回空字符串，并且 SQL_DESC_UNNAMED 设置为 SQL_UNNAMED。<br /><br /> 从 IRD SQL_DESC_NAME 记录字段返回此信息。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ 可以为 NULL 的列可以具有 NULL 值; 如果如果列不具有 NULL 值;，SQL_NO_NULLS或 SQL_NULLABLE_UNKNOWN 如果它不已知的列是否接受 NULL 值。<br /><br /> 从 IRD SQL_DESC_NULLABLE 记录字段返回此信息。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|如果 SQL_DESC_TYPE 字段中的数据类型是近似数值数据类型，此 SQLINTEGER 字段将包含值为 2，因为 SQL_DESC_PRECISION 字段包含的位数。 如果 SQL_DESC_TYPE 字段中的数据类型是精确数值数据类型，此字段将包含值为 10，因为 SQL_DESC_PRECISION 字段包含的十进制位数。 此字段设置为 0 表示所有非数字数据类型。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|字符字符串或二进制数据类型的长度，以字节为单位。 对于固定长度字符或二进制类型，这是以字节为单位的实际长度。 对于长度可变的字符或二进制类型，这是以字节为单位的最大长度。 此值不包括 null 终止符。<br /><br /> 从 IRD SQL_DESC_OCTET_LENGTH 记录字段返回此信息。<br /><br /> 有关长度的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|一个数值，对于数值数据类型表示适用的精度。 数据类型 SQL_TYPE_TIME，SQL_TYPE_TIMESTAMP，它表示一个时间间隔，其值的所有 interval 数据类型的小数秒元素适用的精度。<br /><br /> 从 IRD SQL_DESC_PRECISION 记录字段返回此信息。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|是一种数值数据类型的适用小数位数的数字值。 对于小数和数值数据类型，这是定义的比例。 它是不确定对于所有其他数据类型。<br /><br /> 从 IRD 缩放记录字段返回此信息。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含列的表的架构。 如果列是一个表达式，或者如果列是视图的一部分，则返回的值是实现定义。 如果数据源不支持架构或架构名称不能确定，则返回空字符串。 此 VARCHAR 记录字段不超过 128 个字符。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|如果列不能在 WHERE 子句，SQL_PRED_NONE。 （这是与 ODBC 2 中的 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果在 WHERE 子句，但仅与 LIKE 谓词，则可以使用列，SQL_PRED_CHAR。 （这是与 ODBC 2 中的 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> 如果可以使用类似除外的所有比较运算符的 WHERE 子句中使用列，SQL_PRED_BASIC。 （这是与 ODBC 2 中的 SQL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果可以使用任何比较运算符的 WHERE 子句中使用列，SQL_PRED_SEARCHABLE。<br /><br /> 列键入 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 通常返回 SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含该列的表的名称。 如果列是一个表达式，或者如果列是视图的一部分，则返回的值是实现定义。<br /><br /> 如果无法确定表名，则返回空字符串。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|一个数字值，指定的 SQL 数据类型。<br /><br /> 当*ColumnNumber*等于为 0，SQL_BINARY 返回可变长度书签的和 SQL_INTEGER 返回固定长度书签的。<br /><br /> 对于日期时间和间隔数据类型，此字段会返回详细的数据类型： SQL_DATETIME 或 SQL_INTERVAL。 (有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附录 d： 数据类型中。<br /><br /> 从 IRD SQL_DESC_TYPE 记录字段返回此信息。 **注意：**为了与 ODBC 2 配合工作。*x*驱动程序，请改用 SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|数据源 – 依赖于数据类型名称;例如，"CHAR"、"VARCHAR"、"货币"、"长 VARBINARY"或者"CHAR （） FOR BIT DATA"。<br /><br /> 如果类型为未知，则返回空字符串。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 或 SQL_UNNAMED。 如果 IRD SQL_DESC_NAME 字段包含的列别名或列名，则返回 SQL_NAMED。 如果没有列名称或列别名，则返回 SQL_UNNAMED。<br /><br /> 从 IRD SQL_DESC_UNNAMED 记录字段返回此信息。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 如果列是无符号 （或不是数字）。<br /><br /> 如果签名列，SQL_FALSE。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|列将被描述为定义的常数的值：<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 介绍结果集中的列，不基表中的列的可更新性。 结果集列所基于的基列 updatability 可能不同于此字段中的值。 某列是否可更新可以基于数据类型、 用户权限和结果集本身的定义。 如果不清楚是否可更新列，则将返回 SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**是可扩展的替代方法**SQLDescribeCol**。 **SQLDescribeCol**返回一组固定的基于 ANSI 89 SQL 描述符信息。 **SQLColAttribute**允许对更广泛的 ANSI sql-92 和 DBMS 供应商扩展中可用的描述符信息集的访问。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取数据的多个的行|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>示例  
 下面的示例代码不会释放句柄和连接。 请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)，[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)，和[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)有关代码示例，以释放句柄和语句。  
  
```  
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
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   retCode = SQLNumResultCols(hstmt, &numColumn);  
  
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
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
