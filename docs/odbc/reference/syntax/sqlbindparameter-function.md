---
title: SQLBindParameter 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79f340d95cf1cd15b176069458347b2bea97055c
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420212"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函数

**符合性**  
 版本引入了：ODBC 2.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLBindParameter**将缓冲区绑定到的 SQL 语句中的参数标记。 **SQLBindParameter**支持绑定到 Unicode 的 C 数据类型，即使基础驱动程序不支持 Unicode 数据。  
  
> [!NOTE]  
>  此函数取代了 ODBC 1.0 函数**SQLSetParam**。 有关详细信息，请参阅"注释"。  
  
## <a name="syntax"></a>语法  
  
```cpp  
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
 [输入]参数编号排序按顺序在不断增加的参数顺序，从 1 开始。  
  
 *InputOutputType*  
 [输入]参数的类型。 有关详细信息，请参阅"*InputOutputType*参数"中"注释"。  
  
 *ValueType*  
 [输入]参数的 C 数据类型。 有关详细信息，请参阅"*ValueType*参数"中"注释"。  
  
 *ParameterType*  
 [输入]SQL 数据类型的参数。 有关详细信息，请参阅"*ParameterType*参数"中"注释"。  
  
 *ColumnSize*  
 [输入]列或表达式的相应参数标记的大小。 有关详细信息，请参阅"*ColumnSize*参数"中"注释"。  
  
 如果你的应用程序将在 64 位 Windows 操作系统上运行，请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *DecimalDigits*  
 [输入]十进制数字的列或表达式的相应参数标记。 有关列大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *ParameterValuePtr*  
 [延迟的输入]指向参数的数据的缓冲区的指针。 有关详细信息，请参阅"*ParameterValuePtr*参数"中"注释"。  
  
 *BufferLength*  
 [输入/输出]长度*ParameterValuePtr*以字节为单位的缓冲区。 有关详细信息，请参阅"*BufferLength*参数"中"注释"。  
  
 请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
 *StrLen_or_IndPtr*  
 [延迟的输入]指向参数的长度的缓冲区的指针。 有关详细信息，请参阅"*StrLen_or_IndPtr*参数"中"注释"。  
  
## <a name="returns"></a>返回

 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断

 当**SQLBindParameter**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLBindParameter** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  

|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|由标识的数据类型*ValueType*自变量不能转换为标识的数据类型*ParameterType*参数。 请注意，可能会返回此错误**SQLExecDirect**， **SQLExecute**，或**SQLPutData**在执行时，而不是由**SQLBindParameter**.|  
|07009|描述符索引无效|(DM) 的参数指定的值*ParameterNumber*是小于 1。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 **MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY003|无效的应用程序缓冲区类型|由参数指定的值*ValueType*不是有效的 C 数据类型或 SQL_C_DEFAULT。|  
|HY004|SQL 数据类型无效|为参数指定的值*ParameterType*是既不是有效的 ODBC SQL 数据类型标识符，也不支持驱动程序的特定于驱动程序的 SQL 数据类型标识符。|  
|HY009|参数值无效|(DM) 参数*ParameterValuePtr*是空指针，该参数*StrLen_or_IndPtr*是 null 指针，并将参数*InputOutputType*未 SQL_PARAM_输出。<br /><br /> (DM) SQL_PARAM_OUTPUT，其中参数*ParameterValuePtr*是空指针，C 类型为 char 或二进制和 BufferLength (*cbValueMax*) 是大于 0。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBindParameter**调用。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数*StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY021|描述符信息不一致|一致性检查期间检查的描述符信息不是一致的。 (请参阅中的"一致性检查"一节**SQLSetDescField**。)<br /><br /> 为参数指定的值*DecimalDigits*超出了指定的 SQL 数据类型的列的数据源支持的值的范围*ParameterType*参数。|  
|HY090|字符串或缓冲区长度无效|(DM) 中的值*BufferLength*小于 0。 (请参阅中的 SQL_DESC_DATA_PTR 字段的说明**SQLSetDescField**。)|  
|HY104|无效的精度或小数位数值|为参数指定的值*ColumnSize*或*DecimalDigits*超出了指定的 SQL 数据类型的列的数据源支持的值的范围*ParameterType*参数。|  
|HY105|无效的参数类型|(DM) 的参数指定的值*InputOutputType*无效。 （请参阅"注释"。）|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的参数指定的值的组合来转换*ValueType*和特定于驱动程序的值的参数指定的*ParameterType*.<br /><br /> 为参数指定的值*ParameterType*版本的 ODBC 驱动程序支持，但不受驱动程序或数据源是一个有效的 ODBC SQL 数据类型标识符。<br /><br /> 该驱动程序支持仅 ODBC 2。*x*和参数*ValueType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 和中列出的所有间隔 C 数据类型[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)中附录 d:数据类型。<br /><br /> 该驱动程序仅支持之前需 3.50 和参数的 ODBC 版本*ValueType*已 SQL_C_GUID。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释

 应用程序调用**SQLBindParameter**绑定 SQL 语句中的每个参数标记。 绑定的应用程序调用之前仍然有效**SQLBindParameter**再次调用**SQLFreeStmt** SQL_RESET_PARAMS 选项，或调用**SQLSetDescField**到APD SQL_DESC_COUNT 标头字段设置为 0。  
  
 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。 有关参数数据类型和参数标记的详细信息，请参阅[参数的数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)并[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)附录 c： 驱动器中SQL 语法。  
  
## <a name="parameternumber-argument"></a>ParameterNumber 参数  
 如果*ParameterNumber*调用中**SQLBindParameter** SQL_DESC_COUNT，值大于**SQLSetDescField**调用以增加 SQL_DESC_ 值到计数*ParameterNumber*。  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 参数  
 *InputOutputType*参数指定的参数类型。 此参数设置 IPD 的 SQL_DESC_PARAMETER_TYPE 字段。 如不调用过程的 SQL 语句中的所有参数**插入**语句，都*输入 * * 参数*。 参数在过程调用中的可以输入、 输入/输出或输出参数。 (应用程序调用**SQLProcedureColumns**来确定的过程调用; 中的参数类型不能确定其类型的参数被假定为输入的参数。)  
  
 *InputOutputType*参数是下列值之一：  
  
-   SQL_PARAM_INPUT. 该参数将不会调用过程中，如的 SQL 语句中的参数标记**插入**语句，或者将标记一个过程中的输入的参数。 例如，在参数**INSERT INTO 员工 VALUES (？，？，？)** 而是输入的参数中的参数 **{调用 AddEmp (？，？，？)}** 可以但不一定是，输入的参数。  
  
     驱动程序时执行该语句，将为该参数的数据发送到数据源;\* *ParameterValuePtr*缓冲区必须包含有效的输入的值，或 **StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT 结果_EXEC 宏。  
  
     如果应用程序不能确定在过程调用参数的类型，它会设置*InputOutputType*为 SQL_PARAM_INPUT; 如果数据源返回的值对于参数，驱动程序将放弃它。  
  
-   SQL_PARAM_INPUT_OUTPUT. 该参数将标记一个过程中的输入/输出参数。 例如，在参数 **{调用 GetEmpDept(?)}** 是接受雇员的姓名，并返回该雇员的部门的名称的输入/输出参数。  
  
     驱动程序时执行该语句，将为该参数的数据发送到数据源;\* *ParameterValuePtr*缓冲区必须包含有效的输入的值，则\* *StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或的结果SQL_LEN_DATA_AT_EXEC 宏。 执行该语句后，驱动程序将参数数据返回到应用程序，如果数据源不返回输入/输出参数的值，该驱动程序设置 **StrLen_or_IndPtr*缓冲区为 SQL_NULL_DATA。  
  
    > [!NOTE]  
    >  在 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 2.0 的驱动程序，在驱动程序管理器将此转换为调用**SQLBindParameter**所在*InputOutputType*参数设置为 SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT。 参数标记的过程或过程; 中的输出参数的返回值在任一情况下，这些参数称为*输出参数*。 例如中的参数 **{？ = 调用 GetNextEmpID}** 是一个输出参数，返回下一步的员工 id。  
  
     执行该语句后，该驱动程序返回参数的数据应用程序，除非*ParameterValuePtr*并*StrLen_or_IndPtr*参数都是 null 指针，在这种情况下驱动程序将放弃输出值。 如果数据源不返回输出参数的值，该驱动程序设置 **StrLen_or_IndPtr*缓冲区为 SQL_NULL_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. 指示应进行流处理输入/输出参数。 **SQLGetData**可以读取部件中的参数值。 *BufferLength*被忽略，因为缓冲区长度取决于调用**SQLGetData**。 值*StrLen_or_IndPtr*缓冲区必须包含 SQL_NULL_DATA、 SQL_DEFAULT_PARAM、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。 如果它将输出在流式传输，必须在输入的数据在执行 (DAE) 参数作为绑定参数。 *ParameterValuePtr*可以是任何非 null 指针值，将返回该值**SQLParamData**如用户定义令牌，其值与传递*ParameterValuePtr*为这两个输入和输出。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM. SQL_PARAM_INPUT_OUTPUT_STREAM，为输出参数相同。 **StrLen_or_IndPtr*在输入上被忽略。  
  
 下表列出了不同的组合*InputOutputType*和 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|结果|上 ParameterValuePtr 评价|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 sql_data_at_exec，那么|输入中的部件|*ParameterValuePtr*可将返回的任何指针值**SQLParamData**如用户定义令牌，其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 sql_data_at_exec，那么|绑定的输入缓冲区|*ParameterValuePtr*是输入缓冲区的地址。|  
|SQL_PARAM_OUTPUT|在输入被忽略。|输出绑定的缓冲区|*ParameterValuePtr*是输出缓冲区的地址。|  
|SQL_PARAM_OUTPUT_STREAM|在输入被忽略。|流式处理的输出|*ParameterValuePtr*可以是任何指针值，将返回**SQLParamData**如用户定义令牌，其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 sql_data_at_exec，那么|输入中的部件和输出绑定的缓冲区|*ParameterValuePtr*是将返回的输出缓冲区的地址**SQLParamData**如用户定义令牌，其值与传递*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 sql_data_at_exec，那么|输入绑定的缓冲区和输出绑定的缓冲区|*ParameterValuePtr*是共享的输入/输出缓冲区的地址。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 或 sql_data_at_exec，那么|输入中的部件和流式处理的输出|*ParameterValuePtr*可以是任何非 null 指针值，将返回**SQLParamData**如用户定义令牌，其值与传递*ParameterValuePtr*为这两个输入和输出。|  
  
> [!NOTE]  
>  该驱动程序必须确定应用程序绑定的输出或输入输出参数，如流式传输时，允许哪些 SQL 类型。 驱动程序管理器不会生成无效的 SQL 类型的错误。  
  
## <a name="valuetype-argument"></a>ValueType 参数

 *ValueType*参数指定的参数的 C 数据类型。 此参数设置 APD 的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段。 这必须是中的值之一[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分的附录 d:数据类型。  
  
 如果*ValueType*参数是一个时间间隔数据类型的 SQL_DESC_TYPE 字段*ParameterNumber* APD 记录设置为 SQL_INTERVAL，APD SQL_DESC_CONCISE_TYPE 字段设置为简洁的时间间隔数据类型和的 SQL_DESC_DATETIME_INTERVAL_CODE 字段*ParameterNumber*记录设置为特定的时间间隔数据类型的子代码。 (请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)数据使用领先的精度 (2) 和默认时间间隔的秒精度 (6)，按照中的 APD SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段分别的默认时间间隔。 如果任一默认的精度不适当，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 如果*ValueType*参数是日期时间数据类型的 SQL_DESC_TYPE 字段之一*ParameterNumber* APD 记录设置为 SQL_DATETIME， SQL_DESC_CONCISE_TYPE字段*ParameterNumber* APD 记录设置为简明 datetime C 数据类型和的 SQL_DESC_DATETIME_INTERVAL_CODE 字段*ParameterNumber*记录设置为特定的日期/时间子代码数据类型。 (请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)  
  
 如果*ValueType*参数为 SQL_C_NUMERIC 数据类型，默认的精度 （这是驱动程序定义），并且默认小数位数 (0)，按照 APD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中使用的数据。 如果默认精度或小数位数不适当，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 SQL_C_DEFAULT 指定默认 C 数据类型从传输参数值为使用指定的 SQL 数据类型*ParameterType*。  
  
 此外可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 有关详细信息，请参阅[默认 C 数据类型](../../../odbc/reference/appendixes/default-c-data-types.md)，[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)，并[转换将数据从 SQL 到 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中附录 d:数据类型。  
  
## <a name="parametertype-argument"></a>ParameterType 参数

 这必须是所列的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)部分的附录 d:数据类型，或它必须是特定于驱动程序的值。 此参数设置 IPD 的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段。  
  
 如果*ParameterType*参数是一个日期时间的标识符、 IPD 的 SQL_DESC_TYPE 字段设置为 SQL_DATETIME、 IPD SQL_DESC_CONCISE_TYPE 字段设置为简明 datetime SQL 数据类型和 SQL_DESC_DATETIME_INTERVAL_CODE 字段设置为适当的日期时间子代码值。  
  
 如果*ParameterType*是一个时间间隔的标识符，IPD 的 SQL_DESC_TYPE 字段设置为 SQL_INTERVAL，IPD SQL_DESC_CONCISE_TYPE 字段设置为简明的 SQL 时间间隔数据类型和 SQL_DESC_DATETIME_INTERVAL_CODE IPD 字段设置为适当的时间间隔子代码。 IPD SQL_DESC_DATETIME_INTERVAL_PRECISION 字段设置为时间间隔前导精度，并且 SQL_DESC_PRECISION 字段设置为秒的时间间隔精度，如果适用。 如果 SQL_DESC_DATETIME_INTERVAL_PRECISION 或 SQL_DESC_PRECISION 的默认值不合适，应用程序应显式将其设置通过调用**SQLSetDescField**。 任何这些字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*参数为 SQL_NUMERIC 数据类型，默认的精度 （这是驱动程序定义），并且默认小数位数 (0)，在 IPD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置使用的数据。 如果默认精度或小数位数不适当，应用程序显式应通过调用设置描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
 有关如何转换数据的信息，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)并[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中附录 d:数据类型。  
  
## <a name="columnsize-argument"></a>ColumnSize 参数

 *ColumnSize*参数指定的列或参数标记，该数据，或两者的长度与对应的表达式的大小。 此参数设置 IPD，具体取决于 SQL 数据类型的不同字段 ( *ParameterType*参数)。 以下规则适用于此映射：  
  
-   如果*ParameterType* SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY 和 SQL_LONGVARBINARY、 或一个简明 SQL 日期时间间隔数据类型，IPD 的 SQL_DESC_LENGTH 字段设置为的值*ColumnSize*。 (有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 中的部分数据类型。）  
  
-   如果*ParameterType* SQL_DECIMAL、 SQL_NUMERIC、 SQL_FLOAT、 SQL_REAL，或 SQL_DOUBLE，IPD 的 SQL_DESC_PRECISION 字段设置为值*ColumnSize*。  
  
-   对于其他数据类型， *ColumnSize*忽略参数。  
  
 有关详细信息，请参阅"传递参数值"和 SQL_DATA_AT_EXEC 中的"*StrLen_or_IndPtr*参数。"  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 参数

 如果*ParameterType*是 SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP、 SQL_INTERVAL_SECOND、 SQL_INTERVAL_DAY_TO_SECOND、 SQL_INTERVAL_HOUR_TO_SECOND，还是 SQL_INTERVAL_MINUTE_TO_SECOND，IPD 的 SQL_DESC_PRECISION 字段设置向*DecimalDigits*。 如果*ParameterType* SQL_NUMERIC 或 SQL_DECIMAL，IPD SQL_DESC_SCALE 字段设置为*DecimalDigits*。 对于所有其他数据类型， *DecimalDigits*忽略参数。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 参数

 *ParameterValuePtr*自变量指向缓冲区的当**SQLExecute**或**SQLExecDirect**被调用时，包含参数的实际数据。 数据必须在指定的窗体*ValueType*参数。 此参数设置 APD SQL_DESC_DATA_PTR 字段。 应用程序可以设置*ParameterValuePtr*参数为 null 指针，只要 *\*StrLen_or_IndPtr* SQL_NULL_DATA 或 SQL_DATA_AT_EXEC。 （这适用仅为输入参数或输入/输出参数）。  
  
 如果\* *StrLen_or_IndPtr*经过 SQL_LEN_DATA_AT_EXEC (*长度*) 宏或 SQL_DATA_AT_EXEC，然后*ParameterValuePtr*是与参数相关联的应用程序定义的指针值。 它将返回到应用程序通过**SQLParamData**。 例如， *ParameterValuePtr*可能是如参数数目、 指向数据的指针或指向应用程序用于将输入的参数绑定结构的指针的非零值令牌。 但是，请注意，如果参数是输入/输出参数， *ParameterValuePtr*必须是指向将存储的输出值的缓冲区的指针。 则 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1，如果应用程序可以使用指向 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性一起使用的值*ParameterValuePtr*自变量。 例如， *ParameterValuePtr*可能指向值的数组和应用程序可能会使用通过 SQL_ATTR_PARAMS_PROCESSED_PTR 指向的值从数组中检索正确的值。 有关详细信息，请参阅本节后面的"传递参数值"。  
  
 如果*InputOutputType*自变量是 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT， *ParameterValuePtr*指向在其中驱动程序返回的输出值的缓冲区。 如果该过程将返回一个或多个结果集\* *ParameterValuePtr*缓冲区不保证为以进行设置，直到处理完所有结果集/行计数。 如果缓冲区未完成处理前设置，输出参数和返回值是不可用，直到**SQLMoreResults**返回 sql_no_data 为止。 调用**SQLCloseCursor**或**SQLFreeStmt** SQL_CLOSE 选项将导致丢弃这些值。  
  
 大于 1，则 SQL_ATTR_PARAMSET_SIZE 语句属性中的值是否*ParameterValuePtr*指向的数组。 单个 SQL 语句处理为输入或输入/输出参数的输入值的完整数组并返回输出参数或输入/输出的输出值的数组。  
  
## <a name="bufferlength-argument"></a>BufferLength 参数

 字符和 C 的二进制数据， *BufferLength*参数指定的长度\* *ParameterValuePtr*缓冲区 （如果它是一个单一元素） 或中的元素的长度\**ParameterValuePtr*数组 （如果 SQL_ATTR_PARAMSET_SIZE 语句属性中的值大于 1）。 此参数设置 APD SQL_DESC_OCTET_LENGTH 记录字段。 如果应用程序指定多个值， *BufferLength*用来确定的位置中的值 **ParameterValuePtr*数组，包括输入和输出。 输入/输出和输出参数，它用于确定是否要截断字符和二进制输出上的 C 数据：  
  
-   C 字符数据，可用来返回的字节数是否大于或等于*BufferLength*中的数据\* *ParameterValuePtr*截断为*BufferLength*小于 null 终止字符的长度是由驱动程序以 null 结尾。  
  
-   对于二进制 C 数据，可用来返回的字节数是否大于*BufferLength*中的数据\* *ParameterValuePtr*截断为*BufferLength*字节。  
  
 对于所有其他类型的 C 数据*BufferLength*忽略参数。 长度\* *ParameterValuePtr*缓冲区 （如果它是一个单一元素） 或中的元素的长度\* *ParameterValuePtr*数组 （如果应用程序调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAMSET_SIZE 指定每个参数的多个值的自变量) 被假定为 C 数据类型的长度。  
  
 对于经过流处理的输出或经过流处理的输入/输出参数*BufferLength*自变量被忽略，因为中指定的缓冲区长度**SQLGetData**。  
  
> [!NOTE]  
>  在 ODBC 1.0 应用程序调用**SQLSetParam**在 ODBC 3。*x*驱动程序，驱动程序管理器将此转换为调用**SQLBindParameter**顺序*BufferLength*参数始终是 SQL_SETPARAM_VALUE_MAX。 因为如果 ODBC 3，驱动程序管理器将返回错误。*x*应用程序设置*BufferLength*到 SQL_SETPARAM_VALUE_MAX，ODBC 3。*x*驱动程序可以使用此来确定调用 ODBC 1.0 应用程序时。  
  
> [!NOTE]  
>  在中**SQLSetParam**，在其中应用程序指定的长度的方式 **ParameterValuePtr*缓冲，以便该驱动程序可以返回字符或二进制数据，以及在其中应用程序发送的方法数组的字符或二进制参数值与驱动程序，驱动程序的定义。  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 参数

 *StrLen_or_IndPtr*自变量指向缓冲区的当**SQLExecute**或**SQLExecDirect**被调用时，包含以下值之一。 （此参数设置的应用程序参数指针的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 记录字段。）  
  
-   中存储的参数值的长度 **ParameterValuePtr*。 这将忽略除字符或二进制 C 数据。  
  
-   SQL_NTS. 参数值是一个以 null 结尾的字符串。  
  
-   SQL_NULL_DATA. 参数值为 NULL。  
  
-   SQL_DEFAULT_PARAM. 一个过程是使用一个参数，默认值而不是从应用程序检索的值。 此值是仅在 ODBC 规范语法中，被调用的过程中有效，然后才*InputOutputType*参数为 SQL_PARAM_INPUT、 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 当\* *StrLen_or_IndPtr*是 SQL_DEFAULT_PARAM， *ValueType*， *ParameterType*， *ColumnSize*， *DecimalDigits*， *BufferLength*，和*ParameterValuePtr*参数对于输入参数，将忽略和仅用于定义输入输出参数值 /输出参数。  
  
-   结果 SQL_LEN_DATA_AT_EXEC (*长度*) 宏。 参数的数据将发送具有**SQLPutData**。 如果*ParameterType*参数为 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或长时间，数据源特定的数据类型，并且驱动程序将返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是要为参数; 发送数据的字节数，否则为*长度*必须是一个非负值，并且将被忽略。 有关详细信息，请参阅"传递参数值，稍后在本部分中。  
  
     例如，若要指定将与发送的数据的 10,000 个字节**SQLPutData**在一个或多个调用时，SQL_LONGVARCHAR 参数，应用程序设置 **StrLen_or_IndPtr*为 SQL_LEN_DATA_AT_EXEC （10000)。  
  
-   SQL_DATA_AT_EXEC. 参数的数据将发送具有**SQLPutData**。 当它们调用 ODBC 3 时，ODBC 1.0 应用程序使用此值。*x*驱动程序。 有关详细信息，请参阅"传递参数值，稍后在本部分中。  
  
 如果*StrLen_or_IndPtr*是 null 指针，该驱动程序假定所有输入的参数值均非空并且字符和二进制数据是以 null 结尾。 如果*InputOutputType* SQL_PARAM_OUTPUT 或 SQL_PARAM_OUTPUT_STREAM 和*ParameterValuePtr*并*StrLen_or_IndPtr*都是 null 指针，驱动程序将放弃输出值。  
  
> [!NOTE]  
>  应用程序开发人员是强烈建议您不要指定为 null 指针*StrLen_or_IndPtr*参数的数据类型时 SQL_C_BINARY。 若要确保驱动程序不会意外地截断 SQL_C_BINARY 数据*StrLen_or_IndPtr*应包含一个指向有效的长度值。  
  
 如果*InputOutputType*自变量是 SQL_PARAM_INPUT_OUTPUT、 SQL_PARAM_OUTPUT、 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM， *StrLen_or_IndPtr*指向在其中的缓冲区驱动程序将返回 SQL_NULL_DATA，可用来返回中的字节数\* *ParameterValuePtr* （不包括 null 终止字节的字符数据），或 SQL_NO_TOTAL (如果到可用的字节数返回不能确定）。 如果该过程返回一个或多个结果集，**StrLen_or_IndPtr*缓冲区不保证为以进行设置，直到已提取的所有结果。  
  
 大于 1，则 SQL_ATTR_PARAMSET_SIZE 语句属性中的值是否*StrLen_or_IndPtr*指向 SQLLEN 值的数组。 这些可以是任何前面在本部分中列出的值，并使用单个 SQL 语句处理。  
  
## <a name="passing-parameter-values"></a>传递参数值

 应用程序也可以将传递某个参数的值中\* *ParameterValuePtr*缓冲区或通过一个或多个调用**SQLPutData**。 其数据传递与参数**SQLPutData**称为*执行时数据*参数。 这些通常用于发送数据对于 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 参数，并可以混合使用其他参数。  
  
 若要将参数值传递，应用程序，请执行以下步骤序列：  
  
1.  调用**SQLBindParameter**为每个参数绑定参数的值的缓冲区 (*ParameterValuePtr*参数) 和长度/指示器 (*StrLen_or_IndPtr*自变量）。 对于执行时数据参数， *ParameterValuePtr*是应用程序定义的指针值，如参数数目或指向数据的指针。 值会更高版本返回，并可用于确定此参数。  
  
2.  将中的输入和输入/输出参数的值放\* *ParameterValuePtr*和 **StrLen_or_IndPtr*缓冲区：  
  
    -   对于普通参数，应用程序将放置中的参数值\* *ParameterValuePtr*缓冲区和中该值的长度 **StrLen_or_IndPtr*缓冲区。 有关详细信息，请参阅[设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   对于执行时数据参数，该应用程序放入结果的 SQL_LEN_DATA_AT_EXEC (*长度*) 中的宏 （当调用 ODBC 2.0 驱动程序） **StrLen_or_IndPtr*缓冲区。  
  
3.  调用**SQLExecute**或**SQLExecDirect**来执行 SQL 语句。  
  
    -   如果没有任何执行时数据参数，该过程已完成。  
  
    -   如果有任何执行时数据参数，该函数将返回 SQL_NEED_DATA。  
  
4.  调用**SQLParamData**检索中指定的应用程序定义的值*ParameterValuePtr*自变量**SQLBindParameter**第一个问题执行时数据参数，以进行处理。 **SQLParamData**返回 SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  返回的值执行时数据参数类似于执行时数据列，尽管**SQLParamData**是为每个不同。 执行时数据参数是数据将发送与 SQL 语句中的参数**SQLPutData**时执行语句**SQLExecDirect**或**SQLExecute**. 它们被绑定与**SQLBindParameter**。 返回的值**SQLParamData**一个指针值传递给**SQLBindParameter**中*ParameterValuePtr*参数。 执行时数据列是包含在行集数据将发送具有**SQLPutData**更新或添加的行时**SQLBulkOperations**的或更新与**SQLSetPos**. 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*缓冲区 (通过调用设置**SQLBindCol**) 正在处理。  
  
5.  调用**SQLPutData**一个或多个次多次以发送参数数据。 如果数据值大于，则需要多次调用\* *ParameterValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**只有在将字符 C 数据发送到包含的字符、 二进制或数据源特定的数据类型的列或二进制 C 数据发送到具有二进制文件，一个字符的列时允许相同的参数或数据源特定的数据类型。  
  
6.  调用**SQLParamData**再次以指示已将该参数的所有数据。  
  
    -   如果有多个执行时数据参数， **SQLParamData**返回 SQL_NEED_DATA 和下一步执行时数据参数的应用程序定义值处理。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的执行时数据参数，该过程已完成。 如果成功执行语句， **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 在此情况下， **SQLParamData**可以返回任何可由用于执行语句，该函数返回的 SQLSTATE (**SQLExecDirect**或**SQLExecute**)。  
  
         所有输入/输出或输出参数的输出值都位于\* *ParameterValuePtr*和 **StrLen_or_IndPtr*缓冲后应用程序中检索所有结果集生成的语句。  
  
 调用**SQLExecute**或**SQLExecDirect**语句置于 SQL_NEED_DATA 状态。 此时，应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**与语句或*连接句柄*与语句相关联。 如果它调用任何其他函数与语句或用语句相关联的连接，该函数将返回 SQLSTATE HY010 （函数序列错误）。 SQL_NEED_DATA 运行时语句叶**SQLParamData**或**SQLPutData**返回一个错误， **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或将取消该语句。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行时数据参数的数据时，取消语句执行; 然后，应用程序可以调用**SQLExecute**或**SQLExecDirect**试。  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流的输出参数

 当应用程序设置*InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM，必须通过一个或多个调用检索输出参数值**SQLGetData**。 当驱动程序具有流式处理的输出参数值以返回到应用程序时，它将在响应对以下函数调用返回 SQL_PARAM_DATA_AVAILABLE:**SQLMoreResults**， **SQLExecute**，和**SQLExecDirect**。 应用程序调用**SQLParamData**来确定哪些参数值为可用。  
  
 有关 SQL_PARAM_DATA_AVAILABLE 和流式处理的输出参数的详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用参数的数组

 应用程序准备具有参数标记，并传入的参数数组的语句，时可以执行这两种不同方式。 一种方法是驱动程序依赖于后端，用例的参数数组与整个语句视为一个原子单元的数组处理功能。 Oracle 的数据源的支持数组处理功能，例如。 另一种方法来实现此功能适用于要生成一批 SQL 语句，每个参数集的参数数组中的一条 SQL 语句执行批处理的驱动程序。 参数的数组不能用于**UPDATE WHERE CURRENT OF**语句。  
  
 当处理数组参数时，可以提供单个结果集/行计数 （一个用于每个参数集） 或结果集/行计数可以汇总成一个。 在选项 SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo**指示行计数是可用于每组参数 (SQL_PARC_BATCH) 还是只有一个行计数是可用 (SQL_PARC_NO_BATCH)。  
  
 在选项 SQL_PARAM_ARRAY_SELECTS **SQLGetInfo**指示结果集是可用于每组参数 (SQL_PAS_BATCH) 还是只有一个结果集是可用 (SQL_PAS_NO_BATCH)。 如果该驱动程序不允许一个结果集生成的语句使用的参数数组执行，SQL_PARAM_ARRAY_SELECTS 返回 SQL_PAS_NO_SELECT。  
  
 有关详细信息，请参阅[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 若要支持参数的数组，则 SQL_ATTR_PARAMSET_SIZE 语句属性设置为指定的每个参数的值的数目。 如果此字段为大于 1，APD 的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段必须指向数组。 每个数组的基数是 SQL_ATTR_PARAMSET_SIZE 的值相等。  
  
 APD SQL_DESC_ROWS_PROCESSED_PTR 字段指向包含已处理，包括错误集的参数集的数量的缓冲区。 处理每个组的参数时，该驱动程序将在缓冲区中存储新值。 如果这是 null 指针，则将返回无编号。 当使用参数的数组时，即使设置函数返回 SQL_ERROR 填充指向 APD SQL_DESC_ROWS_PROCESSED_PTR 字段的值。 如果将返回 SQL_NEED_DATA，指向由 APD SQL_DESC_ROWS_PROCESSED_PTR 字段的值设置为正在处理的参数集。  
  
 当绑定参数数组和所发生的情况**UPDATE WHERE CURRENT OF**执行语句是驱动程序定义。  
  
## <a name="column-wise-parameter-binding"></a>按列参数绑定

 在按列绑定中，应用程序将单独的参数和长度/指示器数组绑定到每个参数。  
  
 若要使用按列绑定，该应用程序将首先为 sql_param_bind_by_column，可以设置 SQL_ATTR_PARAM_BIND_TYPE 语句属性。 （这是默认值）。对于要绑定每个列，该应用程序执行以下步骤：  
  
1.  分配参数缓冲区数组。  
  
2.  分配长度/指示器缓冲区的数组。  
  
    > [!NOTE]  
    >  如果在使用按列绑定时，应用程序将直接写入描述符，独立的数组可以用于长度和指示器数据。  
  
3.  调用**SQLBindParameter**使用以下参数：  
  
    -   *ValueType*是参数缓冲区数组中的单个元素的 C 类型。  
  
    -   *ParameterType*是参数的 SQL 类型。  
  
    -   *ParameterValuePtr*是参数缓冲区数组的地址。  
  
    -   *BufferLength*是参数缓冲区数组中的单个元素的大小。 *BufferLength*固定长度的数据的数据时，将忽略参数。  
  
    -   *StrLen_or_IndPtr*是长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅"注释中，"更高版本在本部分中的"ParameterValuePtr 自变量"。 参数按列绑定的详细信息，请参阅[绑定数组的参数](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>按行参数绑定

 在按行绑定中，应用程序定义包含为每个参数绑定的参数和长度/指示器缓冲区的结构。  
  
 若要使用按行绑定，应用程序，请执行以下步骤：  
  
1.  定义结构来保存一组参数 （包括参数和长度/指示器缓冲区），并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果在使用按行绑定时，应用程序将直接写入描述符，单独的字段可用于长度和指示器数据。  
  
2.  包含一组参数的结构的大小或实例的参数将绑定到其中的缓冲区大小设置 SQL_ATTR_PARAM_BIND_TYPE 语句属性。 长度必须包括所有绑定的参数和结构或缓冲区，以确保当绑定参数的地址与指定的长度递增时，结果将点到中的相同参数的开头的任何填充大小的空间下一步的行。 当你使用*sizeof* ANSI C 中的运算符，将保证该行为。  
  
3.  调用**SQLBindParameter**与每个参数绑定的以下参数：  
  
    -   *ValueType*是要绑定到列的参数缓冲区成员的类型。  
  
    -   *ParameterType*是参数的 SQL 类型。  
  
    -   *ParameterValuePtr*是第一个数组元素中的参数缓冲区成员的地址。  
  
    -   *BufferLength*是参数缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅"*ParameterValuePtr*参数，"在本部分中更高版本。 有关按行绑定参数的详细信息，请参阅[绑定数组的参数](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>错误的信息

 如果驱动程序不实现批次 （SQL_PARAM_ARRAY_ROW_COUNTS 选项是等于 SQL_PARC_NO_BATCH） 的参数数组，就像一条语句已执行处理错误的情况。 如果该驱动程序实现了作为批处理的参数数组，应用程序可以使用 IPD 的 SQL_DESC_ARRAY_STATUS_PTR 标头字段来确定哪些参数的 SQL 语句或参数的数组中的参数导致**SQLExecDirect**或**SQLExecute**返回错误。 此字段包含参数值的每个行的状态信息。 如果该字段指示已发生错误，诊断数据结构中的字段将指示失败的参数的行和参数数量。 将由 APD，可以通过将 SQL_ATTR_PARAMSET_SIZE 语句属性设置中的 SQL_DESC_ARRAY_SIZE 标头字段定义的数组中的元素数。  
  
> [!NOTE]  
>  APD 中的 SQL_DESC_ARRAY_STATUS_PTR 标头字段用于忽略参数。 有关忽略参数的详细信息，请参阅下一部分中，"将忽略的一组参数。"  
  
 当**SQLExecute**或**SQLExecDirect**返回 SQL_ERROR，IPD 中的 SQL_DESC_ARRAY_STATUS_PTR 字段指向数组中的元素将包含 SQL_PARAM_ERROR，SQL_PARAM_SUCCESS，SQL_PARAM_SUCCESS_WITH_INFO、 SQL_PARAM_UNUSED 或 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 为此数组中每个元素，该诊断数据结构包含一个或多个状态记录。 结构的 SQL_DIAG_ROW_NUMBER 字段指示导致了错误的参数值的行号。 如果无法确定导致该错误的参数的某一行中的特定参数，则将 SQL_DIAG_COLUMN_NUMBER 字段中输入的参数编号。  
  
 因为强制早期参数中出现错误尚未使用参数时，将输入 SQL_PARAM_UNUSED **SQLExecute**或**SQLExecDirect**中止。 例如，如果有 50 参数和一个执行时出现错误的参数导致 fortieth 集**SQLExecute**或**SQLExecDirect**中止，则进入 SQL_PARAM_UNUSED参数 41 到 50 的状态数组。  
  
 驱动程序会参数的数组将作为一个整体化单元，以便它不会生成此单个参数级别的错误的信息时，将输入 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 一组参数的处理中的某些错误导致数组中要停止处理后续参数集。 其他错误不会影响后续的参数的处理。 哪些错误将停止处理是驱动程序定义的。 如果不停止处理，数组中的所有参数的都处理、 SQL_SUCCESS_WITH_INFO 返回错误，并且由 SQL_ATTR_PARAMS_PROCESSED_PTR 定义缓冲区设置为已都处理的参数集的总数 (由定义则 SQL_ATTR_PARAMSET_SIZE 语句属性），其中包括错误集。  
  
> [!CAUTION]  
>  ODBC 行为的参数数组的处理过程中发生错误时是在 ODBC 3 不同。*x*比 ODBC 2。*x*。 在 ODBC 2。*x*，该函数返回 SQL_ERROR 和处理时间。 指向缓冲区*pirow*的参数**SQLParamOptions**包含的错误行数。 在 ODBC 3。*x*，该函数将返回 SQL_SUCCESS_WITH_INFO 以及可以处理可能停止或继续。 如果继续，将所有已处理的参数，包括那些导致了错误的值设置 SQL_ATTR_PARAMS_PROCESSED_PTR 指定的缓冲区。 此行为更改可能会导致现有应用程序出现问题。  
  
 当**SQLExecute**或**SQLExecDirect**返回之前完成的参数数组中的所有参数集的处理，如时返回 SQL_ERROR 或 SQL_NEED_DATA 时，包含状态数组已处理这些参数的状态。 IPD 中的 SQL_DESC_ROWS_PROCESSED_PTR 字段指向的位置包含导致 SQL_ERROR 或 SQL_NEED_DATA 错误代码的参数数组中的行号。 数组参数发送到 SELECT 语句，可用性状态数组值时，驱动程序定义的;执行该语句或作为结果集提取后，它们可能可用。  
  
## <a name="ignoring-a-set-of-parameters"></a>忽略一的组参数

 （作为由 SQL_ATTR_PARAM_STATUS_PTR 语句属性设置） APD SQL_DESC_ARRAY_STATUS_PTR 字段可用于指示应忽略的一组 SQL 语句中的绑定参数。 若要指示要在执行过程中忽略的参数的一个或多个集的驱动程序，应用程序应执行以下步骤：  
  
1.  调用**SQLSetDescField**设置 APD 以指向 SQLUSMALLINT 值以包含状态信息的数组的 SQL_DESC_ARRAY_STATUS_PTR 标头字段。 此外可以通过调用设置此字段**SQLSetStmtAttr**与*属性*的 SQL_ATTR_PARAM_OPERATION_PTR，允许应用程序而不获取描述符句柄设置该字段。  
  
2.  设置为两个值之一 APD 的 SQL_DESC_ARRAY_STATUS_PTR 字段定义的数组的每个元素：  
  
    -   SQL_PARAM_IGNORE，以指示该行语句执行中排除。  
  
    -   SQL_PARAM_PROCEED，以指示在语句执行过程中包括的行。  
  
3.  调用**SQLExecDirect**或**SQLExecute**执行已准备的语句。  
  
 以下规则适用于 APD 的 SQL_DESC_ARRAY_STATUS_PTR 字段定义的数组：  
  
-   将指针设置为默认情况下为 null。  
  
-   如果指针为 null，所有参数使用不同的集，如同 SQL_ROW_PROCEED 到已设置的所有元素。  
  
-   将元素设置为 SQL_PARAM_PROCEED 不保证该操作将使用该特定的一组参数。  
  
-   SQL_PARAM_PROCEED 被定义为标头文件中为 0。  
  
 应用程序可以将 SQL_DESC_ARRAY_STATUS_PTR 字段设置为指向所在的同一阵列 APD 中指向的 SQL_DESC_ARRAY_STATUS_PTR 字段在 IRD 中。 参数绑定到行数据时，这很有用。 根据行数据的状态，然后可以忽略参数。 除了 SQL_PARAM_IGNORE，以下代码中要忽略的 SQL 语句导致参数：SQL_ROW_DELETED、 SQL_ROW_UPDATED 和 SQL_ROW_ERROR。 除了 SQL_PARAM_PROCEED，以下代码会导致 SQL 语句以继续：SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 和 SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新绑定参数

 应用程序可以执行两项操作才能更改绑定之一：  
  
-   调用**SQLBindParameter**以指定新的绑定已绑定的列。 该驱动程序将使用新覆盖旧的绑定。  
  
-   指定要添加到绑定调用中所指定的缓冲区地址的偏移量**SQLBindParameter**。 有关详细信息，请参阅下一部分中，"重新绑定，偏移量"。  
  
## <a name="rebinding-with-offsets"></a>重新绑定，偏移量

 当应用程序具有可包含多个参数，但调用的缓冲区区域设置的参数绑定方法特别有用**SQLExecDirect**或**SQLExecute**使用只有几个参数。 通过修改现有的绑定的偏移量，可以为下一组参数使用缓冲区中的剩余空间。  
  
 APD 中的 SQL_DESC_BIND_OFFSET_PTR 标头字段将指向绑定偏移量。 如果该字段为非 null，驱动程序取消引用指针和，如果无 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段中的值为 null 指针，将取消引用的值添加到描述符中这些字段在执行时的记录。 执行 SQL 语句时，将使用新的指针值。 偏移量重新绑定后保持有效。 SQL_DESC_BIND_OFFSET_PTR 是指向偏移量，而不是自身的偏移量，因为应用程序可以更改偏移量，直接，而无需调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)到将描述符字段的更改。 将指针设置为默认情况下为 null。 可以通过调用设置 ARD SQL_DESC_BIND_OFFSET_PTR 字段[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或通过调用[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)与*fAttribute*的 SQL_ATTR_PARAM_BIND_OFFSET_PTR。  
  
 绑定偏移量会始终直接添加到中的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段的值。 如果偏移量更改为不同的值，新值是仍直接添加到每个描述符字段中的值。 新的偏移量不添加到字段值和任何早期的偏移量的总和。  
  
## <a name="descriptors"></a>描述符

 参数绑定的方式取决于 Apd 和 Ipd 的字段。 中的自变量**SQLBindParameter**用于设置这些描述符字段。 此外可以通过设置字段**SQLSetDescField**函数，尽管**SQLBindParameter**更高效使用，因为该应用程序无需获取描述符句柄来调用**SQLBindParameter**。  
  
> [!CAUTION]  
>  调用**SQLBindParameter**为一条语句可能会影响其他语句。 当与语句相关联 ARD 显式分配，并且仍与其他语句相关联时，将发生这种情况。 因为**SQLBindParameter**修改字段的 APD，所做的修改将应用于此说明符与之关联的所有语句。 如果这不是所需的行为，应用程序应取消关联此描述符的其他语句之前它将调用**SQLBindParameter**。  
  
 从概念上讲， **SQLBindParameter**序列中执行以下步骤：  
  
1.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获得 APD 句柄。  
  
2.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)若要获取 APD SQL_DESC_COUNT 字段中，并且如果的值*ColumnNumber*自变量超出 SQL_DESC_COUNT，调用的值**SQLSetDescField**增加到 SQL_DESC_COUNT 值*ColumnNumber*。  
  
3.  调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次将值分配到 APD 的以下字段：  
  
    -   设置的值的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *ValueType*，只不过如果*ValueType*是一个 datetime 或间隔子类型的简洁标识符，它将 SQL_DESC_TYPE 设置为 SQL_日期时间或 SQL_INTERVAL，分别 SQL_DESC_CONCISE_TYPE 简洁的标识符，和设置 SQL_DESC_DATETIME_INTERVAL_CODE 到相应的日期时间或间隔子代码。  
  
    -   设置的值的 SQL_DESC_OCTET_LENGTH 字段*BufferLength*。  
  
    -   设置 SQL_DESC_DATA_PTR 字段的值*ParameterValue*。  
  
    -   SQL_DESC_OCTET_LENGTH_PTR 字段设置为值*StrLen_or_Ind*。  
  
    -   此外将 SQL_DESC_INDICATOR_PTR 字段设置为的值*StrLen_or_Ind*。  
  
     *StrLen_or_Ind*参数指定的指标信息和参数值的长度。  
  
4.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获得 IPD 句柄。  
  
5.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)若要获取 IPD 的 SQL_DESC_COUNT 字段中，并且如果的值*ColumnNumber*自变量超出 SQL_DESC_COUNT，调用的值**SQLSetDescField**增加到 SQL_DESC_COUNT 值*ColumnNumber*。  
  
6.  调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次将值分配到 IPD 的以下字段：  
  
    -   设置的值的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *ParameterType*，只不过如果*ParameterType*是一个 datetime 或间隔子类型的简洁标识符，它会设置 SQL_DESC_TYPE为 SQL_DATETIME 或 SQL_INTERVAL，分别设置为的简洁标识符和对应的日期时间或间隔子代码集 SQL_DESC_DATETIME_INTERVAL_CODE SQL_DESC_CONCISE_TYPE。  
  
    -   将一个或多个 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，设置为适合*ParameterType*。  
  
    -   设置的值 SQL_DESC_SCALE *DecimalDigits*。  
  
 如果在调用**SQLBindParameter**将失败，该值将设置在 APD 中的描述符字段的内容是不确定，并且 APD SQL_DESC_COUNT 字段保持不变。 此外，在 IPD 中的相应记录的 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和的 SQL_DESC_TYPE 字段是不确定和 IPD SQL_DESC_COUNT 字段保持不变。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>调用与 SQLSetParam 的转换

 在 ODBC 1.0 应用程序调用**SQLSetParam**在 ODBC 3。*x*驱动程序，ODBC 3。*x*驱动程序管理器将调用映射以下表中所示。  
  
|调用 ODBC 1.0 应用程序|对 ODBC 3 的调用。*x*驱动程序|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle、 ParameterNumber、 SQL_PARAM_INPUT_OUTPUT、 ValueType、 ParameterType， *ColumnSize*， *DecimalDigits*，ParameterValuePtr、 SQL_SETPARAM_VALUE_MAX，     StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序准备的 SQL 语句来将数据插入到 ORDERS 表。 对于在语句中的每个参数，该应用程序调用**SQLBindParameter**指定 ODBC C 数据类型和 SQL 数据类型的参数，并将缓冲区绑定到每个参数。 对于每一行的数据，应用程序将数据值分配给每个参数并调用**SQLExecute**执行语句。  
  
 下面的示例假定名为 Northwind 与 Northwind 数据库关联的计算机上有 ODBC 数据源。  
  
 有关更多的代码示例，请参阅[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)， [SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)，和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
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

 在以下示例中，应用程序执行 SQL Server 存储过程，请使用命名的参数。  
  
```cpp
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
|释放语句的参数缓冲区|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回语句参数的数目|[SQLNumParams 函数](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|返回下一个参数将数据发送用于|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多个参数值|[SQLParamOptions 函数](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>请参阅

 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
