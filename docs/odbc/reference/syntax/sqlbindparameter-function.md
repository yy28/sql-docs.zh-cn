---
title: "SQLBindParameter 函数 |Microsoft 文档"
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
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1984e301d72e8f2f80cce8e5a5c9864dad0e956
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函数
**一致性**  
 版本引入了： ODBC 2.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBindParameter**将缓冲区绑定到的 SQL 语句中的参数标记。 **SQLBindParameter**支持到 Unicode C 数据类型的绑定，即使基础驱动程序不支持 Unicode 数据。  
  
> [!NOTE]  
>  此函数将替换 ODBC 1.0 函数**SQLSetParam**。 有关详细信息，请参阅"注释"。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ParameterNumber*  
 [输入]参数号排序按顺序在不断增加的参数顺序，从 1 开始。  
  
 *InputOutputType*  
 [输入]参数的类型。 有关详细信息，请参阅"*InputOutputType*自变量"中"注释"。  
  
 *ValueType*  
 [输入]参数的 C 数据类型。 有关详细信息，请参阅"*ValueType*自变量"中"注释"。  
  
 *ParameterType*  
 [输入]参数的 SQL 数据类型。 有关详细信息，请参阅"*ParameterType*自变量"中"注释"。  
  
 *Columnsize 类型*  
 [输入]列或表达式的相应参数标记的大小。 有关详细信息，请参阅"*columnsize 类型*自变量"中"注释"。  
  
 如果你的应用程序将在 64 位 Windows 操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *DecimalDigits*  
 [输入]十进制数字的列或表达式的相应参数标记。 有关列大小的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *ParameterValuePtr*  
 [延迟的输入]指向参数的数据的缓冲区的指针。 有关详细信息，请参阅"*ParameterValuePtr*自变量"中"注释"。  
  
 *BufferLength*  
 [输入/输出]长度*ParameterValuePtr*以字节为单位的缓冲区。 有关详细信息，请参阅"*BufferLength*自变量"中"注释"。  
  
 请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
 *StrLen_or_IndPtr*  
 [延迟的输入]指向参数的长度的缓冲区的指针。 有关详细信息，请参阅"*StrLen_or_IndPtr*自变量"中"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBindParameter**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLBindParameter**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|标识的数据类型*ValueType*不能将参数转换为标识的数据类型*ParameterType*自变量。 请注意，此错误可能由返回**SQLExecDirect**， **SQLExecute**，或**SQLPutData**在执行时，而不是按**SQLBindParameter**.|  
|07009|无效的描述符索引|(DM) 值的参数的指定*ParameterNumber*是小于 1。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 **MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY003|应用程序缓冲区类型无效|自变量所指定的值*ValueType*不是有效的 C 数据类型或 SQL_C_DEFAULT。|  
|HY004|SQL 数据类型无效|为参数指定的值*ParameterType*已既不是有效的 ODBC SQL 数据类型标识符，也不是特定于驱动程序的 SQL 数据类型标识符驱动程序支持。|  
|HY009|无效的参数值|(DM) 自变量*ParameterValuePtr*是空指针，该参数*StrLen_or_IndPtr*是 null 指针和的自变量*InputOutputType*未 SQL_PARAM_输出。<br /><br /> (DM) SQL_PARAM_OUTPUT，其中参数*ParameterValuePtr*是空指针，C 类型为 char 或二进制和 BufferLength (*cbValueMax*) 大于 0。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBindParameter**调用。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY021|描述符信息不一致|在一致性检查过程中检查的描述符信息不是一致的。 (请参阅中的"一致性检查"一节**SQLSetDescField**。)<br /><br /> 为参数指定的值*DecimalDigits*超出了支持由指定的 SQL 数据类型的列的数据源的值的范围*ParameterType*自变量。|  
|HY090|字符串或缓冲区长度无效|(DM) 中的值*BufferLength*小于 0。 (请参阅中的 SQL_DESC_DATA_PTR 字段的说明**SQLSetDescField**。)|  
|HY104|无效的精度或小数位数值|为参数指定的值*columnsize 类型*或*DecimalDigits*超出了支持由指定的 SQL 数据类型的列的数据源的值的范围*ParameterType*自变量。|  
|HY105|无效的参数类型|(DM) 值的参数的指定*InputOutputType*无效。 （请参阅"注释"。）|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的参数指定的值的组合的转换*ValueType*和驱动程序的特定于值为参数指定*ParameterType*.<br /><br /> 为参数指定的值*ParameterType*的 ODBC 版本所支持的驱动程序，但不支持的驱动程序或数据源是有效的 ODBC SQL 数据类型标识符。<br /><br /> 驱动程序还支持仅 ODBC 2。*x*和自变量*ValueType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 中列出所有间隔 C 数据类型和[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中。<br /><br /> 该驱动程序仅支持之前售价 3.50 和的自变量的 ODBC 版本*ValueType*已 SQL_C_GUID。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLBindParameter**绑定 SQL 语句中的每个参数标记。 绑定仍然有效之前的应用程序调用**SQLBindParameter**同样，调用**SQLFreeStmt** SQL_RESET_PARAMS 选项或调用与**SQLSetDescField**到APD SQL_DESC_COUNT 标头字段设置为 0。  
  
 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。 有关参数数据类型和参数标记的详细信息，请参阅[参数数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)和[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)附录 c: SQL 语法中。  
  
## <a name="parameternumber-argument"></a>ParameterNumber 自变量  
 如果*ParameterNumber*对的调用中**SQLBindParameter**大于 SQL_DESC_COUNT，值**SQLSetDescField**调用以增加 SQL_DESC_ 的值计数到*ParameterNumber*。  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 自变量  
 *InputOutputType*参数指定的参数的类型。 此参数设置为 IPD SQL_DESC_PARAMETER_TYPE 字段。 请勿调用过程，如的 SQL 语句中的所有参数**插入**语句，*输入**参数*。 在过程调用中的参数可作为输入、 输入/输出，或输出参数。 (应用程序调用**SQLProcedureColumns**来确定在过程调用; 参数的类型无法确定其类型参数都被认为是输入的参数。)  
  
 *InputOutputType*自变量是下列值之一：  
  
-   SQL_PARAM_INPUT。 参数将不调用过程中，如 SQL 语句中的参数标记**插入**语句，或它将在过程中的输入的参数的标记。 例如中的参数**插入到员工值 (？，？，？)**是输入的参数，而中的参数**{调用 AddEmp (？，？，？)}**可以但并不一定，输入的参数。  
  
     当执行语句时，该驱动程序将为参数的数据发送到数据源;\* *ParameterValuePtr*缓冲区必须包含有效的输入的值，或 **StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT 的结果_EXEC 宏。  
  
     如果应用程序无法确定在过程调用中参数的类型，它将设置*InputOutputType*到 SQL_PARAM_INPUT; 如果数据源返回一个值对于参数，驱动程序将丢弃它。  
  
-   SQL_PARAM_INPUT_OUTPUT。 参数将标记中的过程的输入/输出参数。 例如中的参数**{调用 GetEmpDept(?)}**是接受员工的名称，并返回该雇员的部门的名称的输入/输出参数。  
  
     当执行语句时，该驱动程序将为参数的数据发送到数据源;\* *ParameterValuePtr*缓冲区必须包含有效的输入的值，或\* *StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或的结果SQL_LEN_DATA_AT_EXEC 宏。 驱动程序执行的语句后，将参数的数据返回给该应用程序;如果数据源不返回输入/输出参数的值，该驱动程序设置 **StrLen_or_IndPtr* SQL_NULL_DATA 缓冲区。  
  
    > [!NOTE]  
    >  在 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 2.0 的驱动程序，驱动程序管理器将此转换为调用**SQLBindParameter**顺序*InputOutputType*参数设置为 SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT。 参数将标记一个过程或输出参数在过程; 中的返回值在任一情况下，这些被称为*输出参数*。 例如中的参数**{？ = 调用 GetNextEmpID}**是输出参数返回下一步的员工 id。  
  
     驱动程序执行的语句后，除非在应用程序，返回了参数的数据*ParameterValuePtr*和*StrLen_or_IndPtr*自变量都是 null 指针，在这种情况下驱动程序将丢弃的输出值。 如果数据源不返回输出参数的值，该驱动程序设置 **StrLen_or_IndPtr* SQL_NULL_DATA 缓冲区。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM。 指示应进行流处理输入/输出参数。 **SQLGetData**可以读取部件中的参数值。 *BufferLength*被忽略，因为将在调用确定缓冲区长度**SQLGetData**。 值*StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DEFAULT_PARAM、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。 必须在输入的数据在执行 (DAE) 参数作为绑定参数，如果它将在输出进行流式处理。 *ParameterValuePtr*可以是将返回的任何非 null 指针值**SQLParamData**如用户定义标记其值与传递*ParameterValuePtr*为这两个输入和输出。 有关详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM。 SQL_PARAM_INPUT_OUTPUT_STREAM，为输出参数相同。 **StrLen_or_IndPtr*忽略在输入。  
  
 下表列出了不同的组合*InputOutputType*和 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|结果|重新标记上 ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|输入中的部分|*ParameterValuePtr*可以是将返回的任何指针值**SQLParamData**如用户定义标记其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|输入绑定缓冲区|*ParameterValuePtr*是输入缓冲区的地址。|  
|SQL_PARAM_OUTPUT|在输入被忽略。|输出绑定的缓冲区|*ParameterValuePtr*是输出缓冲区的地址。|  
|SQL_PARAM_OUTPUT_STREAM|在输入被忽略。|流式处理的输出|*ParameterValuePtr*可以是任何指针值，该值将返回**SQLParamData**如用户定义标记其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|输入中的部件和输出绑定的缓冲区|*ParameterValuePtr*是输出缓冲区，还将通过返回的地址**SQLParamData**如用户定义标记其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|输入绑定缓冲区和输出绑定的缓冲区|*ParameterValuePtr*是共享的输入/输出缓冲区的地址。|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|输入中的部件和流式处理的输出|*ParameterValuePtr*可以是任何非 null 指针值，该值将返回**SQLParamData**如用户定义标记其值与传递*ParameterValuePtr*两个输入和输出。|  
  
> [!NOTE]  
>  该驱动程序必须确定应用程序绑定的输出或输入输出参数，如流式传输时，允许哪些 SQL 类型。 驱动程序管理器将不会生成错误的 SQL 类型无效。  
  
## <a name="valuetype-argument"></a>ValueType 自变量  
 *ValueType*参数指定的参数的 C 数据类型。 此参数设置 APD SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段。 这必须是中的值之一[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型的部分。  
  
 如果*ValueType*自变量是 interval 数据类型的 SQL_DESC_TYPE 字段之一*ParameterNumber* APD 记录设置为 SQL_INTERVAL，APD SQL_DESC_CONCISE_TYPE 字段设置为简洁间隔数据类型和的 SQL_DESC_DATETIME_INTERVAL_CODE 字段*ParameterNumber*记录设置为特定的时间间隔的数据类型的子代码。 (请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)使用数据的默认间隔为 APD，SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段中的组分别前导精度 (2) 和默认时间间隔秒精度 (6)。 如果任一默认精度不合适，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 如果*ValueType*自变量是一个 datetime 数据类型的 SQL_DESC_TYPE 字段*ParameterNumber* APD 记录设置为 SQL_DATETIME， SQL_DESC_CONCISE_TYPE字段*ParameterNumber* APD 记录设置为简洁 datetime C 数据类型和的 SQL_DESC_DATETIME_INTERVAL_CODE 字段*ParameterNumber*记录设置为子代码的特定日期时间数据类型。 (请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)  
  
 如果*ValueType*参数为 SQL_C_NUMERIC 数据类型，则默认精度 （这是驱动程序定义），并且默认规模 (0)，在 APD，SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置使用的数据。 如果默认精度或小数位数不合适，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 SQL_C_DEFAULT 指定参数值从默认 C 数据类型传输，使用指定的 SQL 数据类型为*ParameterType*。  
  
 你还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 有关详细信息，请参阅[默认 C 数据类型](../../../odbc/reference/appendixes/default-c-data-types.md)， [C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)，和[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附录 d： 数据类型中。  
  
## <a name="parametertype-argument"></a>ParameterType 自变量  
 这必须是中列出的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型，或它的部分必须是特定于驱动程序的值。 此参数设置 IPD SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段。  
  
 如果*ParameterType*自变量是一个 datetime 标识符、 IPD SQL_DESC_TYPE 字段设置为 SQL_DATETIME、 IPD SQL_DESC_CONCISE_TYPE 字段设置为简洁 datetime SQL 数据类型和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为适当的日期时间子代码值。  
  
 如果*ParameterType*一个间隔的标识符，IPD SQL_DESC_TYPE 字段设置为 SQL_INTERVAL，IPD SQL_DESC_CONCISE_TYPE 字段设置为简洁的 SQL 间隔数据类型和 SQL_DESC_DATETIME_IPD INTERVAL_CODE 字段设置为适当的间隔子代码。 IPD SQL_DESC_DATETIME_INTERVAL_PRECISION 字段设置为时间间隔前导精度，并且 SQL_DESC_PRECISION 字段设置为间隔秒精度，如果适用。 如果 SQL_DESC_DATETIME_INTERVAL_PRECISION 或 SQL_DESC_PRECISION 的默认值不合适，应用程序应显式设置它通过调用**SQLSetDescField**。 有关任何这些字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*参数为 SQL_NUMERIC 数据类型，则默认精度 （这是驱动程序定义），并且默认规模 (0)，在 IPD，SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置使用的数据。 如果默认精度或小数位数不合适，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 有关转换数据的方式的信息，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)和[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附录 d： 数据类型中。  
  
## <a name="columnsize-argument"></a>Columnsize 类型自变量  
 *Columnsize 类型*参数指定的列或参数标记，该数据，或两个长度所对应的表达式的大小。 此参数设置 IPD，具体取决于 SQL 数据类型的不同字段 ( *ParameterType*自变量)。 以下规则适用于此映射：  
  
-   如果*ParameterType* SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或简洁 SQL 日期时间或间隔数据类型之一，IPD SQL_DESC_LENGTH 字段设置为的值*Columnsize 类型*。 (有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中的部分。)  
  
-   如果*ParameterType*是 SQL_DECIMAL、 SQL_NUMERIC、 SQL_FLOAT、 SQL_REAL 或 SQL_DOUBLE，IPD SQL_DESC_PRECISION 字段设置为值*columnsize 类型*。  
  
-   对于其他数据类型， *columnsize 类型*忽略自变量。  
  
 有关详细信息，请参阅"将传递参数值"和在 SQL_DATA_AT_EXEC"*StrLen_or_IndPtr*参数。"  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 自变量  
 如果*ParameterType*是 SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP、 SQL_INTERVAL_SECOND、 SQL_INTERVAL_DAY_TO_SECOND、 SQL_INTERVAL_HOUR_TO_SECOND 或 SQL_INTERVAL_MINUTE_TO_SECOND，IPD SQL_DESC_PRECISION 字段设置到*DecimalDigits*。 如果*ParameterType* SQL_NUMERIC 或 SQL_DECIMAL，IPD SQL_DESC_SCALE 字段设置为*DecimalDigits*。 对于所有其他数据类型， *DecimalDigits*忽略自变量。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 自变量  
 *ParameterValuePtr*参数指向缓冲区的当**SQLExecute**或**SQLExecDirect**被调用时，包含参数的实际数据。 数据必须在指定的窗体*ValueType*自变量。 此参数设置为 APD SQL_DESC_DATA_PTR 字段。 应用程序可以设置*ParameterValuePtr*自变量为 null 指针，只要 *\*StrLen_or_IndPtr* SQL_NULL_DATA 或 SQL_DATA_AT_EXEC。 （这适用仅为输入参数或输入/输出参数。）  
  
 如果\* *StrLen_or_IndPtr* SQL_LEN_DATA_AT_EXEC 结果 (*长度*) 宏或 SQL_DATA_AT_EXEC，然后*ParameterValuePtr*是与参数相关联的应用程序定义的指针值。 它将返回到应用程序通过**SQLParamData**。 例如， *ParameterValuePtr*可能如参数数目、 一个指向数据或指向应用程序用于将输入的参数绑定的结构的指针的非零令牌。 但是，请注意，如果参数是输入/输出参数， *ParameterValuePtr*必须是指向将存储的输出值的缓冲区的指针。 如果 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1，应用程序可以使用指向由 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性一起使用的值*ParameterValuePtr*自变量。 例如， *ParameterValuePtr*可能指向的值的数组和应用程序可能会使用通过 SQL_ATTR_PARAMS_PROCESSED_PTR 指向的值从数组中检索正确的值。 有关详细信息，请参阅本节后面的"传递参数值"。  
  
 如果*InputOutputType*自变量是 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT， *ParameterValuePtr*指向在其中驱动程序返回的输出值的缓冲区。 如果该过程返回一个或多个结果集， \* *ParameterValuePtr*缓冲区不能保证在处理完所有结果集/行计数之前设置。 如果完成处理之前未设置缓冲区，输出参数和返回值都不可用之前**SQLMoreResults**返回 SQL_NO_DATA。 调用**SQLCloseCursor**或**SQLFreeStmt** SQL_CLOSE 选项将导致丢弃这些值。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1， *ParameterValuePtr*指向数组。 单个 SQL 语句处理的输入或输入/输出参数的输入值的完整数组并返回输出参数或输入/输出的输出值的数组。  
  
## <a name="bufferlength-argument"></a>BufferLength 自变量  
 用于字符和二进制 C 数据*BufferLength*参数指定的长度\* *ParameterValuePtr*缓冲区 （如果它是单个元素） 或中的某个元素的长度\**ParameterValuePtr*数组 （如果 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1）。 此参数设置为 APD SQL_DESC_OCTET_LENGTH 记录字段。 如果应用程序指定多个值， *BufferLength*用于确定的位置中的值 **ParameterValuePtr*数组，在输入和输出。 对于输入/输出和输出参数，它用于确定是否截断字符和二进制 C 数据输出：  
  
-   对于字符 C 数据，可用于返回的字节数是否大于或等于*BufferLength*中的数据\* *ParameterValuePtr*截断为*BufferLength* null 终止字符的长度小于且由驱动程序以 null 结尾。  
  
-   对于二进制 C 数据，可用于返回的字节数是否大于*BufferLength*中的数据\* *ParameterValuePtr*截断为*BufferLength*字节。  
  
 对于所有其他类型的 C 数据*BufferLength*忽略自变量。 长度\* *ParameterValuePtr*缓冲区 （如果它是单个元素） 或中的某个元素的长度\* *ParameterValuePtr*数组 （如果在应用程序调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAMSET_SIZE 指定每个参数的多个值的自变量) 被假定为 C 数据类型的长度。  
  
 对于经过流处理的输出或经过流处理的输入/输出参数， *BufferLength*因为中指定的缓冲区长度，则忽略参数**SQLGetData**。  
  
> [!NOTE]  
>  在 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 3 中。*x*驱动程序，驱动程序管理器将此转换为调用**SQLBindParameter**顺序*BufferLength*自变量始终是 SQL_SETPARAM_VALUE_MAX。 因为如果 ODBC 3，驱动程序管理器将返回错误。*x*应用程序集*BufferLength*到 SQL_SETPARAM_VALUE_MAX，ODBC 3。*x*驱动程序可以使用此来确定当调用 ODBC 1.0 应用程序。  
  
> [!NOTE]  
>  在**SQLSetParam**、 应用程序在其中指定的长度的方式 **ParameterValuePtr*缓冲，以便该驱动程序可以返回字符或二进制数据，以及在其中应用程序发送的方式数组的字符或二进制参数值与驱动程序，驱动程序的定义。  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 自变量  
 *StrLen_or_IndPtr*参数指向缓冲区的当**SQLExecute**或**SQLExecDirect**被调用时，包含以下项之一。 （此参数设置应用程序参数指针 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 记录的字段）。  
  
-   中存储的参数值的长度 **ParameterValuePtr*。 这将被忽略字符或二进制 C 数据除外。  
  
-   SQL_NTS 以。 参数值是以 null 结尾的字符串。  
  
-   SQL_NULL_DATA。 参数值为 NULL。  
  
-   SQL_DEFAULT_PARAM。 一个过程是使用一个参数，默认值而不是从应用程序检索的值。 此值是仅在 ODBC 规范语法中，被调用的过程中有效，然后才*InputOutputType*自变量是 SQL_PARAM_INPUT、 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 当\* *StrLen_or_IndPtr*是 SQL_DEFAULT_PARAM， *ValueType*， *ParameterType*， *columnsize 类型*， *DecimalDigits*， *BufferLength*，和*ParameterValuePtr*参数为输入参数忽略和仅用于定义输入的输出参数值 /输出参数。  
  
-   SQL_LEN_DATA_AT_EXEC 的结果 (*长度*) 宏。 参数的数据将发送与**SQLPutData**。 如果*ParameterType*参数为 SQL_LONGVARBINARY、 SQL_LONGVARCHAR、 或 long 类型的值，数据源 – 特定的数据类型，并且该驱动程序返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是参数; 发送数据的字节数否则为*长度*必须是一个非负的值，并且将被忽略。 有关详细信息，请参阅"将传递参数值，"本部分中更高版本。  
  
     例如，若要指定 10,000 个字节的数据，将发送与**SQLPutData**在一个或多个调用中，为 SQL_LONGVARCHAR 参数，应用程序将设置 **StrLen_or_IndPtr*为 SQL_LEN_DATA_AT_EXEC （10000)。  
  
-   SQL_DATA_AT_EXEC。 参数的数据将发送与**SQLPutData**。 当它们调用 ODBC 3 时，将由 ODBC 1.0 应用程序使用此值。*x*驱动程序。 有关详细信息，请参阅"将传递参数值，"本部分中更高版本。  
  
 如果*StrLen_or_IndPtr*是 null 指针，该驱动程序假定所有的输入的参数值的非 NULL，并且字符和二进制数据是以 null 结尾。 如果*InputOutputType* SQL_PARAM_OUTPUT 或 SQL_PARAM_OUTPUT_STREAM 和*ParameterValuePtr*和*StrLen_or_IndPtr*都是 null 指针，驱动程序丢弃输出值。  
  
> [!NOTE]  
>  应用程序开发人员从指定为 null 指针，强烈建议不要使用*StrLen_or_IndPtr*参数的数据类型时 SQL_C_BINARY。 若要确保驱动程序不意外截断 SQL_C_BINARY 数据*StrLen_or_IndPtr*应包含指向有效的长度值的指针。  
  
 如果*InputOutputType*自变量是 SQL_PARAM_INPUT_OUTPUT、 SQL_PARAM_OUTPUT、 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM， *StrLen_or_IndPtr*指向在其中的缓冲区驱动程序返回 SQL_NULL_DATA，可用于在中返回的字节数\* *ParameterValuePtr* （不包括 null 终止字节的字符数据），或 SQL_NO_TOTAL (如果到可用的字节数返回无法确定）。 如果该过程返回一个或多个结果集，**StrLen_or_IndPtr*不能保证缓冲区之前已提取所有结果设置。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1， *StrLen_or_IndPtr*指向 SQLLEN 值的数组。 这些可以是任何在本部分前面列出的值，并且使用单个 SQL 语句进行处理。  
  
## <a name="passing-parameter-values"></a>传递参数值  
 应用程序可以将参数的值可以传递中\* *ParameterValuePtr*缓冲区或通过一个或多个调用**SQLPutData**。 其数据与一起传递的参数**SQLPutData**称为*数据在执行*参数。 这些通常用于发送数据 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 参数，并可与其他参数组合。  
  
 为传递参数值，应用程序，请执行以下步骤序列：  
  
1.  调用**SQLBindParameter**为每个参数绑定的参数的值的缓冲区 (*ParameterValuePtr*自变量) 和长度/指示器 (*StrLen_or_IndPtr*自变量）。 对于数据在执行参数， *ParameterValuePtr*是应用程序定义的指针值，如参数数量或指向数据的指针。 值将返回更高版本，可以用于确定此参数。  
  
2.  将放置在输入和输入/输出参数的值\* *ParameterValuePtr*和 **StrLen_or_IndPtr*缓冲区：  
  
    -   对于普通参数，应用程序将中的参数值\* *ParameterValuePtr*缓冲区和中的该值的长度 **StrLen_or_IndPtr*缓冲区。 有关详细信息，请参阅[设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   对于数据在执行参数，应用程序放入 SQL_LEN_DATA_AT_EXEC 的结果 (*长度*) 中的宏 （时调用的 ODBC 2.0 的驱动程序） **StrLen_or_IndPtr*缓冲区。  
  
3.  调用**SQLExecute**或**SQLExecDirect**执行 SQL 语句。  
  
    -   如果没有数据在执行参数，该过程已完成。  
  
    -   如果没有任何数据在执行参数，该函数将返回 SQL_NEED_DATA。  
  
4.  调用**SQLParamData**检索中指定的应用程序定义的值*ParameterValuePtr*参数**SQLBindParameter**第一个问题要处理的数据在执行参数。 **SQLParamData**返回 SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  尽管执行中的数据参数类似于执行中的数据列，返回的值**SQLParamData**每个不同。 数据在执行参数是数据将发送与 SQL 语句中的参数**SQLPutData**与执行该语句时**SQLExecDirect**或**SQLExecute**. 它们被绑定与**SQLBindParameter**。 返回的值**SQLParamData**指针值传递给**SQLBindParameter**中*ParameterValuePtr*自变量。 执行中的数据列是包含在行集数据将发送与**SQLPutData**更新或添加与某行时**SQLBulkOperations**或更新与**SQLSetPos**. 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*缓冲区 (通过调用设置**SQLBindCol**) 正在进行。  
  
5.  调用**SQLPutData**一个或多个时间来发送数据的参数。 如果数据值大于需要多个调用\* *ParameterValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**仅当将字符 C 数据发送到具有字符、 binary 或数据源 – 特定数据类型的列或将二进制 C 数据发送到列，但字符，二进制文件，允许相同的参数或数据源 – 特定的数据类型。  
  
6.  调用**SQLParamData**以指示所有数据均已都发送的参数。  
  
    -   如果没有更多的数据在执行参数， **SQLParamData**返回 SQL_NEED_DATA 和下一步的执行中的数据参数的应用程序定义值处理。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的数据在执行参数，则过程已完成。 如果已成功执行该语句， **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 此时， **SQLParamData**可返回用于执行该语句的函数可以返回任何 SQLSTATE (**SQLExecDirect**或**SQLExecute**)。  
  
         输出值的任何输入/输出或输出参数均位于\* *ParameterValuePtr*和 **StrLen_or_IndPtr*缓冲后应用程序中检索所有结果集生成的语句。  
  
 调用**SQLExecute**或**SQLExecDirect**将语句置于 SQL_NEED_DATA 的状态。 此时，应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**与语句或*连接句柄*与语句关联。 如果它调用具有语句或语句与关联的连接的任何其他函数，该函数将返回 SQLSTATE HY010 （函数序列错误）。 SQL_NEED_DATA 状态时语句使**SQLParamData**或**SQLPutData**返回一个错误， **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或将取消该语句。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行中的数据参数的数据，取消语句执行; 然后，应用程序可以调用**SQLExecute**或**SQLExecDirect**试。  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流式处理的输出参数  
 当应用程序设置*InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM，必须通过一个或多个调用检索输出参数值**SQLGetData**。 如果该驱动程序具有要返回到应用程序的流式处理的输出参数值，它将在以下函数的调用的响应中返回 SQL_PARAM_DATA_AVAILABLE: **SQLMoreResults**， **SQLExecute**，和**SQLExecDirect**。 应用程序调用**SQLParamData**以确定哪些参数值为可用。  
  
 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用参数的数组  
 当应用程序准备带参数标记，并传入的参数数组的语句时，有两种不同方式，这可以执行。 一种方法是为驱动程序依赖于后端，用例与数组的参数的整个语句视为一个原子单元的数组处理功能。 Oracle 是一种支持阵列处理功能的数据源。 另一种方法来实现此功能适用于要生成一批 SQL 语句，每个参数集的参数数组中的一条 SQL 语句和执行批处理的驱动程序。 参数数组不能与使用**更新 WHERE CURRENT OF**语句。  
  
 当处理的参数数组时，可以提供单个结果集/行计数 （一个用于每个参数集） 或结果集中的行计数可以汇总成一个。 SQL_PARAM_ARRAY_ROW_COUNTS 选项**SQLGetInfo**指示行计数是可用于每个组参数 (SQL_PARC_BATCH) 还是只有一个行计数是可用 (SQL_PARC_NO_BATCH)。  
  
 SQL_PARAM_ARRAY_SELECTS 选项**SQLGetInfo**指示结果集是可用于每个组参数 (SQL_PAS_BATCH)，还是仅一个结果集是可用 (SQL_PAS_NO_BATCH)。 如果该驱动程序不允许的结果生成集 – 语句的参数数组的情况下执行，SQL_PARAM_ARRAY_SELECTS 返回 SQL_PAS_NO_SELECT。  
  
 有关详细信息，请参阅[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 若要支持的参数数组，SQL_ATTR_PARAMSET_SIZE 语句属性设置为指定的每个参数的值的数目。 如果此字段为大于 1，则 APD SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段必须指向数组。 每个数组的基数等于 SQL_ATTR_PARAMSET_SIZE 的值。  
  
 APD SQL_DESC_ROWS_PROCESSED_PTR 字段指向包含集的已处理，包括错误集的参数数量的缓冲区。 处理每个组参数时，驱动程序将存储在缓冲区中的新值。 如果这是 null 指针，则将返回没有数。 时使用的参数数组，即使设置函数返回 SQL_ERROR 填充指向 APD SQL_DESC_ROWS_PROCESSED_PTR 字段的值。 如果返回 SQL_NEED_DATA，指向 APD SQL_DESC_ROWS_PROCESSED_PTR 字段的值设置为正在处理的参数集。  
  
 当绑定的参数数组和所发生的情况**更新 WHERE CURRENT OF**执行语句是驱动程序定义。  
  
## <a name="column-wise-parameter-binding"></a>列参数绑定  
 在列绑定中，应用程序将单独的参数和长度/指示器数组绑定到每个参数。  
  
 若要使用专用于列的绑定，该应用程序首先 SQL_ATTR_PARAM_BIND_TYPE 语句将该属性设置 SQL_PARAM_BIND_BY_COLUMN。 （这是默认值）。对于每个绑定的列，应用程序执行以下步骤：  
  
1.  将分配一个参数缓冲区数组。  
  
2.  分配一个数组的长度/指示器缓冲区。  
  
    > [!NOTE]  
    >  如果在使用专用于列的绑定时，应用程序将直接写入描述符，单独的数组可以用于长度和指标数据。  
  
3.  调用**SQLBindParameter**使用以下参数：  
  
    -   *ValueType*是参数缓冲区数组中的单个元素的 C 类型。  
  
    -   *ParameterType*是参数的 SQL 类型。  
  
    -   *ParameterValuePtr*是参数缓冲区数组的地址。  
  
    -   *BufferLength*是参数缓冲区数组中的单个元素的大小。 *BufferLength*固定长度的数据的数据时，将忽略自变量。  
  
    -   *StrLen_or_IndPtr*是长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅"注释中，"本部分中后面的"ParameterValuePtr 自变量"。 有关列的绑定参数的详细信息，请参阅[绑定数组的参数](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>按行参数绑定  
 在按行绑定中，应用程序定义包含的每个参数绑定的参数和长度/指示器缓冲区的结构。  
  
 若要使用按行绑定，该应用程序，请执行以下步骤：  
  
1.  定义一种结构来保留一组参数 （包括参数和长度/指示器缓冲区），并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果在使用按行绑定时，应用程序将直接写入描述符，不同的字段，可以用于长度和指标数据。  
  
2.  到包含一组参数的结构的大小或实例的参数将绑定到其中的缓冲区的大小，请设置 SQL_ATTR_PARAM_BIND_TYPE 语句属性。 长度必须包括所有绑定的参数和结构或缓冲区，以确保当绑定参数的地址将递增，具有指定长度，结果将点到中的相同参数的开头的任何填充空间下一步的行。 当你使用*sizeof* ANSI C 中的运算符，此行为保证。  
  
3.  调用**SQLBindParameter**与每个参数绑定的以下参数：  
  
    -   *ValueType*是要绑定到列的参数缓冲区成员的类型。  
  
    -   *ParameterType*是参数的 SQL 类型。  
  
    -   *ParameterValuePtr*是第一个数组元素中的参数缓冲区成员的地址。  
  
    -   *BufferLength*是参数缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅"*ParameterValuePtr*自变量，"本部分中更高版本。 有关按行绑定参数的详细信息，请参阅[绑定数组的参数](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>错误信息  
 如果驱动程序不实现为批处理 （SQL_PARAM_ARRAY_ROW_COUNTS 选项等于 SQL_PARC_NO_BATCH） 的参数数组，就像一个语句已执行处理错误情况。 如果该驱动程序实现为批处理的参数数组，应用程序可以使用 IPD SQL_DESC_ARRAY_STATUS_PTR 标头字段来确定哪个参数的 SQL 语句或中的参数数组的参数导致**SQLExecDirect**或**SQLExecute**返回错误。 此字段包含参数值的每一行的状态信息。 如果字段指示发生错误，则诊断数据结构中的字段将指示失败的参数的行和参数数。 将由 APD，可以通过 SQL_ATTR_PARAMSET_SIZE 语句属性设置中的 SQL_DESC_ARRAY_SIZE 标头字段定义的数组中的元素数。  
  
> [!NOTE]  
>  在 APD SQL_DESC_ARRAY_STATUS_PTR 标头字段用于忽略参数。 有关忽略参数的详细信息，请参阅下一部分中，"忽略一组参数。"  
  
 当**SQLExecute**或**SQLExecDirect**返回 SQL_ERROR，按 IPD 的 SQL_DESC_ARRAY_STATUS_PTR 域指向数组中的元素将包含 SQL_PARAM_ERROR，SQL_PARAM_SUCCESS，SQL_PARAM_SUCCESS_WITH_INFO、 SQL_PARAM_UNUSED 或 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 对于此数组中每个元素，该诊断数据结构包含一个或多个状态记录。 结构的 SQL_DIAG_ROW_NUMBER 字段指示导致错误的参数值的行号。 如果无法确定导致错误的参数的行中的特定参数，则将 SQL_DIAG_COLUMN_NUMBER 字段中输入的参数数量。  
  
 由于强制早期参数中发生了错误尚未使用参数时输入 SQL_PARAM_UNUSED **SQLExecute**或**SQLExecDirect**中止。 例如，如果没有 50 参数和执行时发生错误的参数导致 fortieth 集**SQLExecute**或**SQLExecDirect**中止，则 SQL_PARAM_UNUSED 进入参数 41 至 50 的状态数组。  
  
 驱动程序会参数的数组将作为一个整体的单元，因此它不会生成此单个参数级别的错误信息，则会进入 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 在一组参数的处理某些错误导致数组中要停止处理后续的参数集。 其他错误不会影响后续的参数的处理。 哪些错误将停止处理是驱动程序定义的。 如果不停止处理，数组中的所有参数的都处理、 SQL_SUCCESS_WITH_INFO 返回由于错误，并且由 SQL_ATTR_PARAMS_PROCESSED_PTR 定义的缓冲区设置为的都处理的参数集的总数 (按照定义SQL_ATTR_PARAMSET_SIZE 语句属性），其中包括错误集。  
  
> [!CAUTION]  
>  ODBC 行为的参数数组的处理过程中发生错误时是 ODBC 3 中不同。*x*比 ODBC 2。*x*。 在 ODBC 2。*x*，该函数返回 SQL_ERROR 和处理上限时间停止。 指向缓冲区*pirow*参数**SQLParamOptions**包含的错误行数。 在 ODBC 3。*x*，该函数将返回 SQL_SUCCESS_WITH_INFO 并可以处理可能会停止或继续。 如果它仍然存在，则 SQL_ATTR_PARAMS_PROCESSED_PTR 所指定的缓冲区将设置为所有参数处理，包括那些导致了错误的值。 此行为更改可能导致现有应用程序出现问题。  
  
 当**SQLExecute**或**SQLExecDirect**返回之前完成的参数数组中的所有参数集的处理，如 SQL_ERROR 或 SQL_NEED_DATA 返回时，包含状态数组已处理这些参数的状态。 按 IPD 的 SQL_DESC_ROWS_PROCESSED_PTR 域指向的位置包含导致 SQL_ERROR 或 SQL_NEED_DATA 错误代码的参数数组中的行号。 数组参数发送到 SELECT 语句的可用性状态数组值时，驱动程序定义的;执行的语句或作为结果集提取后，它们可能可用。  
  
## <a name="ignoring-a-set-of-parameters"></a>忽略一组参数  
 （如通过 SQL_ATTR_PARAM_STATUS_PTR 语句特性组） APD SQL_DESC_ARRAY_STATUS_PTR 字段可用于指示应忽略一组 SQL 语句中的绑定参数。 若要指示要在执行过程中忽略的参数的一个或多个集的驱动程序，应用程序应遵循以下步骤：  
  
1.  调用**SQLSetDescField**设置 APD 以指向 SQLUSMALLINT 值，以包含状态信息的数组的 SQL_DESC_ARRAY_STATUS_PTR 标头字段。 此字段也可以通过调用设置**SQLSetStmtAttr**与*属性*的 SQL_ATTR_PARAM_OPERATION_PTR，允许应用程序将字段设置而不获取的描述符句柄。  
  
2.  设置为两个值之一 APD 的 SQL_DESC_ARRAY_STATUS_PTR 字段定义的数组的每个元素：  
  
    -   SQL_PARAM_IGNORE，以指示行不从语句执行。  
  
    -   SQL_PARAM_PROCEED，以指示行包含在语句执行。  
  
3.  调用**SQLExecDirect**或**SQLExecute**执行已准备的语句。  
  
 以下规则适用于 APD 的 SQL_DESC_ARRAY_STATUS_PTR 字段定义的数组：  
  
-   将指针设置为默认情况下 null。  
  
-   如果指针为 null，所有的参数集使用时，就像所有元素都设置为 SQL_ROW_PROCEED。  
  
-   将元素设置为 SQL_PARAM_PROCEED 不保证该操作将使用该特定的一组参数。  
  
-   SQL_PARAM_PROCEED 定义为标头文件中的 0。  
  
 应用程序可以在 IRD 设置 SQL_DESC_ARRAY_STATUS_PTR 中的字段以指向所在的同一阵列 APD 指向按 SQL_DESC_ARRAY_STATUS_PTR 字段。 参数绑定到行数据时，这非常有用。 根据行数据的状态，然后可以忽略参数。 除了 SQL_PARAM_IGNORE，以下代码所导致的中要忽略的 SQL 语句的参数： SQL_ROW_DELETED、 SQL_ROW_UPDATED 和 SQL_ROW_ERROR。 除了 SQL_PARAM_PROCEED，以下代码会导致 SQL 语句以继续： SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 和 SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新绑定参数  
 应用程序可以执行更改绑定的两个操作之一：  
  
-   调用**SQLBindParameter**可指定已绑定的列的新绑定。 该驱动程序替换为新将覆盖旧的绑定。  
  
-   指定要添加到指定的绑定调用的缓冲区地址的偏移量**SQLBindParameter**。 有关详细信息，请参阅下一部分中，"重新绑定偏移量"。  
  
## <a name="rebinding-with-offsets"></a>重新绑定偏移量  
 当应用程序具有可以包含多个参数，但调用一个缓冲区区域设置，则特别有用的参数重新绑定**SQLExecDirect**或**SQLExecute**使用只有几个参数。 缓冲区中剩余的空间可以用于任务的下一步的参数集的一个偏移量修改现有的绑定。  
  
 在 APD SQL_DESC_BIND_OFFSET_PTR 标头字段将指向绑定偏移量。 如果此字段为非 null，驱动程序取消引用指针和，如果 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段中的值不是 null 指针，将取消引用的值添加到描述符中的这些字段在执行时的记录。 执行 SQL 语句时，将使用新的指针值。 重新绑定后，偏移量就保持有效。 由于 SQL_DESC_BIND_OFFSET_PTR 是指向偏移量，而不是本身的偏移量的指针，应用程序可以更改偏移量直接，而无需调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)到更改描述符字段。 将指针设置为默认情况下 null。 可以通过调用设置 ARD SQL_DESC_BIND_OFFSET_PTR 字段[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或通过调用[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)与*fAttribute*的 SQL_ATTR_PARAM_BIND_OFFSET_PTR。  
  
 绑定偏移量是始终直接添加到 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段中的值。 如果偏移量更改为不同的值，新值仍会添加直接向每个描述符字段中的值。 新的偏移量不会添加到的字段值和任何早期的偏移量之和。  
  
## <a name="descriptors"></a>描述符  
 如何将参数绑定已确定 APDs 和 IPDs 的字段。 中的自变量**SQLBindParameter**用于设置这些描述符字段。 也可以通过设置字段**SQLSetDescField**函数，尽管**SQLBindParameter**会更加高效使用，因为应用程序无需获取的描述符句柄调用**SQLBindParameter**。  
  
> [!CAUTION]  
>  调用**SQLBindParameter**为一条语句可能会影响其他语句。 当与语句关联 ARD 显式分配且又与其他语句相关联，将发生这种情况。 因为**SQLBindParameter**修改字段的 APD，修改应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联此描述符从其他语句之前它将调用**SQLBindParameter**。  
  
 从概念上讲， **SQLBindParameter**序列中执行以下步骤：  
  
1.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获得 APD 句柄。  
  
2.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)获取 APD SQL_DESC_COUNT 字段，并且如果的值*ColumnNumber*参数超过 SQL_DESC_COUNT，调用的值**SQLSetDescField**增加到 SQL_DESC_COUNT 值*ColumnNumber*。  
  
3.  调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次将值分配到 APD 以下字段：  
  
    -   SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 设置的值为*ValueType*，只不过如果*ValueType*是日期时间或间隔的子类型的简洁标识符，它将 SQL_DESC_TYPE 设置为 SQL_DATETIME 或 SQL_INTERVAL，分别将 SQL_DESC_CONCISE_TYPE 设置为的简洁的标识符，并将 SQL_DESC_DATETIME_INTERVAL_CODE 设置为相应的日期时间或间隔子代码。  
  
    -   将 SQL_DESC_OCTET_LENGTH 字段设置为的值*BufferLength*。  
  
    -   将 SQL_DESC_DATA_PTR 字段设置为的值*ParameterValue*。  
  
    -   将 SQL_DESC_OCTET_LENGTH_PTR 字段设置为的值*StrLen_or_Ind*。  
  
    -   此外将 SQL_DESC_INDICATOR_PTR 字段设置的值为*StrLen_or_Ind*。  
  
     *StrLen_or_Ind*参数指定的指示器信息以及参数值的长度。  
  
4.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获得 IPD 句柄。  
  
5.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)获取 IPD SQL_DESC_COUNT 字段，并且如果的值*ColumnNumber*参数超过 SQL_DESC_COUNT，调用的值**SQLSetDescField**增加到 SQL_DESC_COUNT 值*ColumnNumber*。  
  
6.  调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次将值分配到 IPD 以下字段：  
  
    -   SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 设置的值为*ParameterType*，只不过如果*ParameterType*是日期时间或间隔的子类型的简洁标识符，它将设置 SQL_DESC_TYPE为 SQL_DATETIME 或 SQL_INTERVAL，可以分别将 SQL_DESC_CONCISE_TYPE 设置为的简洁标识符和集 SQL_DESC_DATETIME_INTERVAL_CODE 到相应的日期时间或间隔子代码。  
  
    -   将一个或多个 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，设置为适合*ParameterType*。  
  
    -   设置的值的 SQL_DESC_SCALE *DecimalDigits*。  
  
 如果调用**SQLBindParameter**将失败，它将设置在 APD 描述符字段的内容是不确定，并且 APD SQL_DESC_COUNT 字段保持不变。 此外，是不确定的 IPD 中相应的记录的 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_TYPE 字段和 IPD SQL_DESC_COUNT 字段保持不变。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>调用与 SQLSetParam 的转换  
 在 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 3 中。*x*驱动程序，ODBC 3。*x*驱动程序管理器映射调用下表中所示。  
  
|调用 ODBC 1.0 应用程序|调用 ODBC 3。*x*驱动程序|  
|----------------------------------|-------------------------------|  
|SQLSetParam （StatementHandle、 ParameterNumber、 ValueType、 ParameterType、 LengthPrecision、 ParameterScale、 ParameterValuePtr、 StrLen_or_IndPtr）;|SQLBindParameter (StatementHandle、 ParameterNumber、 SQL_PARAM_INPUT_OUTPUT、 ValueType、 ParameterType， *columnsize 类型*， *DecimalDigits*，ParameterValuePtr、 SQL_SETPARAM_VALUE_MAX，     StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序准备要 ORDERS 表中插入数据的 SQL 语句。 对于在语句中的每个参数，应用程序调用**SQLBindParameter**指定 ODBC C 数据类型和 SQL 数据类型的参数，并绑定到每个参数的缓冲区。 对于数据每一行，应用程序将数据值分配给每个参数和调用**SQLExecute**执行语句。  
  
 下面的示例假定名为 Northwind 与 Northwind 数据库的计算机上有 ODBC 数据源。  
  
 有关更多的代码示例，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)， [SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)，和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序执行 SQL Server 存储过程，请使用命名的参数。  
  
```  
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|在语句中返回有关参数的信息|[SQLDescribeParam 函数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放参数缓冲区的语句上|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回语句参数的数目|[SQLNumParams 函数](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|返回下一个参数发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多个参数值|[SQLParamOptions 函数](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在执行时发送的参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)

