---
title: SQLColAttribute 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca10614062a495de2c8f0ee80d7bbd5c0e675ad4
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449746"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLColAttribute**结果集中返回列的描述符信息。 描述符信息返回为字符串、 一个依赖于描述符的值或一个整数值。  
  
> [!NOTE]  
>  有关哪些驱动程序管理器的详细信息将时 ODBC 3 映射到此函数。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[向后兼容性的应用程序映射替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 [输入]在 IRD 是要检索的字段值中的记录数。 此参数对应于结果数据，在不断增加的列顺序，从 1 开始按顺序排序的列号。 可以按任意顺序描述列。  
  
 可以在该参数中指定列 0 但除 SQL_DESC_TYPE 和 SQL_DESC_OCTET_LENGTH 之外的所有值都将都返回未定义的值。  
  
 *FieldIdentifier*  
 [输入]描述符句柄。 此句柄定义 IRD 中的哪个字段应查询 （例如 SQL_COLUMN_TABLE_NAME）。  
  
 *CharacterAttributePtr*  
 [输出]指向用于返回中的值的缓冲区*FieldIdentifier*字段*ColumnNumber* IRD，如果此字段为字符字符串的行。 否则，该字段是未使用。  
  
 如果*CharacterAttributePtr*为 NULL， *StringLengthPtr*仍将返回的总字节数 （不包括字符数据的 null 终止字符） 可用于在缓冲区中返回指向*CharacterAttributePtr*。  
  
 *BufferLength*  
 [输入]如果*FieldIdentifier*是一个 ODBC 定义的字段和*CharacterAttributePtr*指向字符的字符串或二进制缓冲区中，此参数应为的长度\* *CharacterAttributePtr*。 如果*FieldIdentifier*是一个 ODBC 定义的字段和\* *CharacterAttribute*Ptr 是一个整数，则忽略此字段。 如果 *\*CharacterAttributePtr*是 Unicode 字符串 (在调用时**SQLColAttributeW**)，则*BufferLength*参数必须为偶数。 如果*FieldIdentifier*是驱动程序定义的字段，该应用程序通过设置来指示字段到驱动程序管理器的性质*BufferLength*参数。 *BufferLength*可以具有以下值：  
  
-   如果*CharacterAttributePtr*是一个指针，指向*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*CharacterAttributePtr*是一个字符串，指向*BufferLength*是缓冲区的长度。  
  
-   如果*CharacterAttributePtr* SQL_LEN_BINARY_ATTR 的结果是指向二进制缓冲区中，在应用程序的位置的指针 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*CharacterAttributePtr*是为固定长度的数据类型，指针*BufferLength*必须是以下值之一：SQL_IS_INTEGER、 SQL_IS_UNINTEGER、 SQL_SMALLINT 或 SQLUSMALLINT。  
  
 *StringLengthPtr*  
 [输出]指向用于返回的总字节数 （不包括字符数据的 null 终止字节） 的缓冲区可用于在返回 **CharacterAttributePtr*。  
  
 对于字符数据，可用来返回的字节数是否大于或等于*BufferLength*中的描述符信息\* *CharacterAttributePtr*截断为*BufferLength*减去 null 终止字符的长度是由驱动程序以 null 结尾。  
  
 对于所有其他类型的数据的值*BufferLength*将被忽略，并且该驱动程序假定的大小 **CharacterAttributePtr*为 32 位。  
  
 *NumericAttributePtr*  
 [输出]指向用于返回中的值的整数缓冲区*FieldIdentifier*字段*ColumnNumber* IRD，如果字段是一个数字描述符类型，例如 SQL_DESC_COLUMN_LENGTH 行。 否则，该字段是未使用。 请注意，某些驱动程序可能只能写入低 32 位或 16 位的缓冲区，并保留较高顺序位保持不变。 因此，应用程序应调用此函数之前初始化为 0 的值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColAttribute**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLColAttribute** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *CharacterAttributePtr*是否不足够大以返回整个字符串值中，因此字符串值被截断。 在返回未截断的字符串值的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07005|预定义语句不*游标规范*|与相关的语句*StatementHandle*未返回结果集并*FieldIdentifier*未 SQL_DESC_COUNT。 没有任何列来描述。|  
|07009|描述符索引无效|(DM) 为指定的值*ColumnNumber*等于 0，而 SQL_ATTR_USE_BOOKMARKS 语句属性是 SQL_UB_OFF。<br /><br /> 为参数指定的值*ColumnNumber*大于结果集中的列数。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagField**从诊断数据结构描述的错误，其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 调用 SQLColAttribute 时仍在执行此 aynchronous 函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 在调用之前已调用函数**SQLPrepare**， **SQLExecDirect**，或为目录函数*StatementHandle*。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|（数据挖掘）  *\*CharacterAttributePtr*是一个字符串，并*BufferLength*小于 0，但不是等于 SQL_NTS。|  
|HY091|描述符字段标识符无效|为参数指定的值*FieldIdentifier*未定义的值之一，而且不是实现定义的值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|驱动程序不可用|为参数指定的值*FieldIdentifier*不受驱动程序。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
 当调用后**SQLPrepare**之前**SQLExecute**， **SQLColAttribute**可以返回任何可由返回的 SQLSTATE **SQLPrepare**或**SQLExecute**，取决于当数据源的计算结果与关联的 SQL 语句*StatementHandle*。  
  
 出于性能原因，应用程序不应调用**SQLColAttribute**语句之前执行。  
  
## <a name="comments"></a>注释  
 有关应用程序如何使用返回的信息**SQLColAttribute**，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**返回的信息，或者在\* *NumericAttributePtr*中或在\* *CharacterAttributePtr*。 在中返回整数信息\* *NumericAttributePtr*为 SQLLEN 值; 所有其他格式的信息中返回\* *CharacterAttributePtr*。 当在返回的信息时\* *NumericAttributePtr*，该驱动程序将忽略*CharacterAttributePtr*， *BufferLength*，和*StringLengthPtr*。 当在返回的信息时\* *CharacterAttributePtr*，该驱动程序将忽略*NumericAttributePtr*。  
  
 **SQLColAttribute**从 IRD 的描述符字段返回值。 语句句柄，而不是个描述符句柄调用的函数。 返回的值**SQLColAttribute**有关*FieldIdentifier*稍后在本部分中列出的值也可以检索通过调用**SQLGetDescField**与合适的 IRD 句柄。  
  
 当前定义的描述符字段，在其中引入了它们，并在其中为其返回信息的自变量稍后在本部分中; ODBC 的版本更多的描述符类型可能会由驱动程序以利用不同的数据源定义。  
  
 ODBC 3。*x*驱动程序必须为每个描述符字段返回一个值。 如果描述符字段不适用于驱动程序或数据源，并且除非另行说明，否则驱动程序将返回 0 \* *StringLengthPtr*或空字符串中的 **CharacterAttributePtr*。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3。*x*函数**SQLColAttribute**替换不推荐使用的 ODBC 2。*x*函数**SQLColAttributes**。 映射时**SQLColAttributes**到**SQLColAttribute** (时 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序)，或映射**SQLColAttribute**到**SQLColAttributes** (时 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序)，或者驱动程序管理器的值传递*FieldIdentifier*通过，请将其映射到一个新值，或返回一个错误，按如下所示：  
  
> [!NOTE]  
>  在中使用的前缀*FieldIdentifier* ODBC 3 中的值。*x*已从该中使用的 ODBC 2。*x*。 新的前缀为"SQL_DESC";旧的前缀为"SQL_COLUMN"。  
  
-   如果 **#define** ODBC 2 的值。*x* *FieldIdentifier*等同于 **#define** ODBC 3 的值。*x* *FieldIdentifier*，只需通过传递函数调用中的值。  
  
-   **#Define** ODBC 2 的值。*x* *FieldIdentifiers* SQL_COLUMN_LENGTH、 SQL_COLUMN_PRECISION 和 SQL_COLUMN_SCALE 是不同于 **#define** ODBC 3 的值。*x* *FieldIdentifiers* SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_LENGTH。 ODBC 2。*x*驱动程序仅需支持 ODBC 2。*x*值。 ODBC 3。*x*驱动程序必须支持"SQL_COLUMN"和"SQL_DESC"值的这三种*FieldIdentifiers*。 这些值是不同的因为精度、 小数位数和长度定义以不同的方式在 ODBC 3。*x*比 ODBC 2 中。*x*。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果 **#define** ODBC 2 的值。*x* *FieldIdentifier*不同于 **#define** ODBC 3 的值。*x* *FieldIdentifier*，和为发生计数，名称，可以为 NULL 值，函数调用中的值映射到相应的值。 例如，SQL_COLUMN_COUNT 映射到 SQL_DESC_COUNT，并且 SQL_DESC_COUNT 映射到 SQL_COLUMN_COUNT，具体取决于映射的方向。  
  
-   如果*FieldIdentifier*是在 ODBC 3 的新值。*x*，为其时 ODBC 2 没有相应的值。*x*，它不会映射时 ODBC 3。*x*对的调用中的应用程序使用它**SQLColAttribute** ODBC 2 中。*x*驱动程序，并调用将返回 SQLSTATE HY091 （无效的描述符字段标识符）。  
  
 下表列出了返回的描述符类型**SQLColAttribute**。 类型*NumericAttributePtr*的值是**SQLLEN \*** 。  
  
|*FieldIdentifier*|信息<br /><br /> 在中返回|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 列是否自动递增列。<br /><br /> 如果列不是自动递增列，或不是数值，SQL_FALSE。<br /><br /> 此字段是有效的数值数据类型列。 应用程序可以将值插入到的行中包含自动递增的列，但通常不能更新列中的值。<br /><br /> 插入到 autoincrement 列时，唯一的值是在插入时，插入到列。 增量未定义，但源特定的数据。 应用程序不应假定 autoincrement 列按任何特定值开始在任何特定点或增量。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|基列名称的结果集列。 如果基列名称不存在 （如中所示的列的表达式的情况下），则此变量包含空字符串。<br /><br /> 将从 IRD 的只读字段的 SQL_DESC_BASE_COLUMN_NAME 记录字段返回此信息。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|包含的列的基表的名称。 如果基表名称不能定义或不适用，则此变量包含空字符串。<br /><br /> 将从 IRD 的只读字段的 SQL_DESC_BASE_TABLE_NAME 记录字段返回此信息。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|如果将列视为排序规则和比较的区分大小写为，SQL_TRUE。<br /><br /> 如果列均不被视为排序规则和比较的区分大小写，或为非字符类型，SQL_FALSE。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含的列的表的目录。 返回的值是实现定义如果列是表达式或列是视图的一部分。 如果数据源不支持目录或目录名称不能确定，则返回空字符串。 此 VARCHAR 记录字段不超过 128 个字符。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|简洁数据类型。<br /><br /> 对于日期时间和间隔数据类型，此字段返回的简洁数据类型;例如，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR。 (有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)中附录 d:数据类型。）<br /><br /> 将从 IRD 的 SQL_DESC_CONCISE_TYPE 记录字段返回此信息。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|在结果集中可用的列数。 如果结果集中没有任何列，这会返回 0。 中的值*ColumnNumber*忽略参数。<br /><br /> 从 IRD 的 SQL_DESC_COUNT 标头字段中返回此信息。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|若要显示列中的数据所需的字符的最大数目。 有关显示大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|如果列具有固定的精度和非零规模的数据源特定于，SQL_TRUE。<br /><br /> 如果列不具有固定的精度和非零规模的数据源特定于，SQL_FALSE。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|列标签或标题。 例如，一个名为 EmpName 列可能被标记为雇员姓名或可能会带有一个别名。<br /><br /> 如果列不具有标签，则返回的列名称。 如果列是未标记的和未命名，则返回空字符串。|  
|SQL_DESC_LENGTH  (ODBC 3.0)|*NumericAttributePtr*|可以是数字值的最大值或实际的字符长度的字符字符串或二进制数据类型。 这是固定长度的数据类型的最大字符长度或可变长度数据类型的实际字符长度。 其值始终不包括结束字符字符串的 null 终止字节。<br /><br /> 将从 IRD 的 SQL_DESC_LENGTH 记录字段返回此信息。<br /><br /> 长度有关的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含的字符或驱动程序会识别为此数据类型的文字的前缀的字符。 此字段包含空字符串数据类型为其文字前缀不适用。 有关详细信息，请参阅[文字前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含的字符或驱动程序会识别为此数据类型的文字的后缀的字符。 此字段包含空字符串数据类型为其文本后缀不适用。 有关详细信息，请参阅[文字前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 记录字段包含的数据类型可能不同于常规的数据类型名称的任何本地化 （本机语言） 名称。 如果没有本地化的名称，则返回空字符串。 此字段是仅出于显示目的。 字符串的字符集与区域设置相关并通常是服务器的默认字符集。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|如果要将它应用列别名。 如果列别名不适用，则返回的列名称。 在任一情况下，SQL_DESC_UNNAMED 设置为 SQL_NAMED。 如果没有任何列名称或列别名，则返回空字符串和 SQL_DESC_UNNAMED 设置为 SQL_UNNAMED。<br /><br /> 将从 IRD 的 SQL_DESC_NAME 记录字段返回此信息。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ 可以为 NULL 的列可以具有 NULL 值; 如果如果列不具有 NULL 值;，SQL_NO_NULLS或 SQL_NULLABLE_UNKNOWN 如果不知道列是否接受 NULL 值。<br /><br /> 将从 IRD 的 SQL_DESC_NULLABLE 记录字段返回此信息。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|近似数字数据类型中的 SQL_DESC_TYPE 字段的数据类型时，此 SQLINTEGER 字段将包含值为 2，因为 SQL_DESC_PRECISION 字段包含的位数。 如果中的 SQL_DESC_TYPE 字段的数据类型为精确数字数据类型，此字段将包含值为 10，因为 SQL_DESC_PRECISION 字段包含的小数位数。 此字段设置为 0 表示所有非数字数据类型。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|字符字符串或二进制数据类型长度 （字节）。 对于固定长度的字符或二进制类型，这是以字节为单位的实际长度。 对于可变长度字符或二进制类型，这是以字节为单位的最大长度。 此值不包括 null 终止符。<br /><br /> 将从 IRD 的 SQL_DESC_OCTET_LENGTH 记录字段返回此信息。<br /><br /> 长度有关的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|一个数字值，该值为数值数据类型表示适用的精度。 对于数据类型 SQL_TYPE_TIME SQL_TYPE_TIMESTAMP，并表示时间间隔，其值的所有间隔数据类型都是适用精度的秒的小数部分。<br /><br /> 将从 IRD 的 SQL_DESC_PRECISION 记录字段返回此信息。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|一个数字值，该值是数值数据类型的适用小数位数。 对于 DECIMAL 和 NUMERIC 数据类型，这是定义的小数位数。 对于所有其他数据类型未定义它。<br /><br /> 将从 IRD 的规模记录字段返回此信息。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含的列的表的架构。 返回的值是实现定义如果列是表达式或列是视图的一部分。 如果数据源不支持架构或架构名称不能确定，则返回空字符串。 此 VARCHAR 记录字段不超过 128 个字符。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|如果列不能在 WHERE 子句中使用，SQL_PRED_NONE。 （这是 ODBC 2 中的 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果在 WHERE 子句，但只能与 LIKE 谓词，则可以使用列，SQL_PRED_CHAR。 （这是 ODBC 2 中的 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> 如果可以使用类似于除外的所有比较运算符的 WHERE 子句中使用该列，SQL_PRED_BASIC。 （这是 ODBC 2 中的 SQL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果可以使用任何比较运算符的 WHERE 子句中使用该列，SQL_PRED_SEARCHABLE。<br /><br /> 列键入 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 通常返回 SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含该列的表的名称。 返回的值是实现定义如果列是表达式或列是视图的一部分。<br /><br /> 如果无法确定表名，则返回空字符串。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|一个数字值，该值指定 SQL 数据类型。<br /><br /> 当*ColumnNumber*相等长度可变的书签的为 0，返回 SQL_BINARY 和 SQL_INTEGER 返回定长书签的。<br /><br /> 对于日期时间和间隔数据类型，此字段返回详细数据类型：SQL_DATETIME 或 SQL_INTERVAL。 (有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)中附录 d:数据类型。<br /><br /> 将从 IRD 的 SQL_DESC_TYPE 记录字段返回此信息。 **注意：** 若要对 ODBC 2 起作用。*x*驱动程序，请改用 SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|数据源相关的数据类型名称;"例如，CHAR"、"VARCHAR"、"MONEY"、"长 VARBINARY"或者"CHAR FOR BIT DATA （）"。<br /><br /> 如果该类型是未知的则返回空字符串。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 或 SQL_UNNAMED。 如果 IRD SQL_DESC_NAME 字段包含的列别名或列名，则返回 SQL_NAMED。 如果没有列名称或列别名，则返回 SQL_UNNAMED。<br /><br /> 将从 IRD 的 SQL_DESC_UNNAMED 记录字段返回此信息。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 如果列是无符号 （或不是数字）。<br /><br /> 如果列已签名，SQL_FALSE。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|该列被描述为定义的常数的值：<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 介绍结果集中的列、 不在基表中的列的可更新性。 结果集列所基于的基列的可更新性可能不同于此字段中的值。 某列是否可更新可以基于数据类型、 用户权限和结果集自身的定义。 如果不清楚是否可更新列，则应返回 SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**可扩展替代**SQLDescribeCol**。 **SQLDescribeCol**返回一组固定的基于 ANSI 89 SQL 描述符信息。 **SQLColAttribute**允许对更广泛的 ANSI SQL-92 和 DBMS 供应商扩展中可用的描述符信息集的访问。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在提取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>示例  
 下面的示例代码不会释放句柄和连接。 请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)，[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)，并[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)有关代码示例以释放句柄和语句。  
  
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
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
