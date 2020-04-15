---
title: SQLBind参数函数 |微软文档
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
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301357"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函数

**一致性**  
 版本介绍： ODBC 2.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBind参数**将缓冲区绑定到 SQL 语句中的参数标记。 **SQLBind参数**支持绑定到 Unicode C 数据类型，即使基础驱动程序不支持 Unicode 数据也是如此。  
  
> [!NOTE]  
>  此功能取代了 ODBC 1.0 函数**SQLSetParam**。 有关详细信息，请参阅"注释"。  
  
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

 *语句句柄*  
 [输入]语句句柄。  
  
 *参数编号*  
 [输入]参数编号，按增加参数顺序顺序排序，从 1 开始。  
  
 InputOutputType   
 [输入]参数的类型。 有关详细信息，请参阅"注释"中的"*输入输出类型*参数"。  
  
 *值类型*  
 [输入]参数的 C 数据类型。 有关详细信息，请参阅"注释"中的"*价值类型*参数"。  
  
 *参数类型*  
 [输入]参数的 SQL 数据类型。 有关详细信息，请参阅"注释"中的"*参数类型*参数"。  
  
 ColumnSize   
 [输入]相应参数标记的列或表达式的大小。 有关详细信息，请参阅"注释"中的"*列大小*参数"。  
  
 如果应用程序将在 64 位 Windows 操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 DecimalDigits   
 [输入]列或相应参数标记的表达式的小数位数。 有关列大小的详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *参数值Ptr*  
 [延迟输入]指向参数数据的缓冲区的指针。 有关详细信息，请参阅"注释"中的"*参数值 Ptr*参数"。  
  
 *缓冲区长度*  
 [输入/输出]*参数ValuePtr*缓冲区的长度（以字节为单位）。 有关详细信息，请参阅"注释"中的"*缓冲区长度*参数"。  
  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *StrLen_or_IndPtr*  
 [延迟输入]指向参数长度的缓冲区的指针。 有关详细信息，请参阅"注释"中的 *"StrLen_or_IndPtr*参数"。  
  
## <a name="returns"></a>返回

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断

 当**SQLBind 参数**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLBindParameter**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  

|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|无法将*ValueType*参数标识的数据类型转换为*参数类型*参数标识的数据类型。 请注意，此错误可能由**SQLExecDirect、SQLExecute**或**SQLExecute** **SQLPutData**在执行时返回，而不是由**SQLBind参数**返回。|  
|07009|无效描述符索引|（DM） 为参数*参数编号*指定的值小于 1。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在 @*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY003|无效的应用程序缓冲区类型|参数*ValueType*指定的值不是有效的 C 数据类型或SQL_C_DEFAULT。|  
|HY004|无效的 SQL 数据类型|为参数*参数类型*指定的值既不是有效的 ODBC SQL 数据类型标识符，也不是驱动程序支持的特定于驱动程序的 SQL 数据类型标识符。|  
|HY009|无效参数值|（DM） 参数*参数ValuePtr*是一个空指针，参数*StrLen_or_IndPtr*为空指针，并且参数*InputOutputType*不SQL_PARAM_OUTPUT。<br /><br /> （DM） SQL_PARAM_OUTPUT，其中参数*参数ValuePtr*为空指针，C 类型为字符或二进制，缓冲区长度 *（cbValueMax*） 大于 0。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLBind参数**时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY021|描述符信息不一致|在一致性检查期间检查的描述符信息不一致。 （请参阅**SQLSetDescField**中的"一致性检查"部分。<br /><br /> 为参数*DecimalDigits*指定的值不在数据源支持的参数*类型*参数指定的 SQL 数据类型列的值范围之外。|  
|HY090|无效的字符串或缓冲区长度|（DM）*缓冲区长度*中的值小于 0。 （请参阅**SQLSetDescField**中SQL_DESC_DATA_PTR字段的说明。|  
|HY104|精度或缩放值无效|为参数*ColumnSize*或*DecimalDigits*指定的值超出*数据源支持的参数类型*参数指定的 SQL 数据类型列的值范围。|  
|HY105|无效参数类型|（DM） 为参数*InputOutputType*指定的值无效。 （请参阅"注释"。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持为参数*ValueType*指定的值和为参数*参数类型*指定的特定于驱动程序的值的组合指定的转换。<br /><br /> 为参数*参数类型*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC SQL 数据类型标识符，但驱动程序或数据源不支持该值。<br /><br /> 驱动程序仅支持 ODBC 2。*x*和参数*ValueType*是以下原因之一：<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 以及附录 D 中的 C[数据类型](../../../odbc/reference/appendixes/c-data-types.md)中列出的所有间隔 C 数据类型：数据类型。<br /><br /> 驱动程序仅支持 3.50 之前的 ODBC 版本，并且参数*ValueType*已SQL_C_GUID。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释

 应用程序调用**SQLBind参数**来绑定 SQL 语句中的每个参数标记。 绑定一直有效，直到应用程序再次调用**SQLBind参数**，使用SQL_RESET_PARAMS选项调用**SQLFreeStmt，** 或调用**SQLSetDescField**将 APD 的SQL_DESC_COUNT标头字段设置为 0。  
  
 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。 有关参数数据类型和参数标记的详细信息，请参阅附录 C 中的[参数数据类型](../../../odbc/reference/appendixes/parameter-data-types.md)和[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)：SQL 语法。  
  
## <a name="parameternumber-argument"></a>参数编号参数  
 如果调用**SQLBind 参数**中的*参数编号*大于SQL_DESC_COUNT的值，则调用**SQLSetDescField**将SQL_DESC_COUNT的值增加到*参数编号*。  
  
## <a name="inputoutputtype-argument"></a>输入输出类型参数  
 *"输入输出类型"* 参数指定参数的类型。 此参数设置 IPD 的SQL_DESC_PARAMETER_TYPE字段。 SQL 语句中不调用过程的所有参数（如**INSERT**语句）都是*输入参数*。 过程调用中的参数可以是输入、输入/输出或输出参数。 （应用程序调用**SQLAEK**确定哪些过程调用中的参数类型;无法确定其类型的参数假定为输入参数。  
  
 InputOutputType 参数为以下其中一个值  ：  
  
-   SQL_PARAM_INPUT 参数在 SQL 语句中标记不调用过程（如**INSERT**语句）的参数，或者在过程中标记输入参数。 例如，**插入员工值 （?, ?, ?）** 中的参数是输入参数，而 **[调用 AddEmp（?, ?, ?）]** 中的参数可以是，但不一定是输入参数。  
  
     执行语句时，驱动程序会将参数的数据发送到数据源;\**参数ValuePtr*缓冲区必须包含有效的输入值，或者 **StrLen_or_IndPtr*缓冲区必须包含SQL_NULL_DATA、SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的结果。  
  
     如果应用程序无法确定过程调用中的参数类型，它将 InputOutputType 设置为SQL_PARAM_INPUT;如果应用程序无法确定过程调用中参数的类型，则将 InputOutputType 将其设置为"*输入输出类型*"。"""""如果"过程调用"中参数的类型。"如果"应用程序"无法确定参数的类型。如果数据源返回参数的值，驱动程序将丢弃它。  
  
-   SQL_PARAM_INPUT_OUTPUT 参数在过程中标记输入/输出参数。 例如 **，[调用 GetEmpDept（？）]** 中的参数是一个输入/输出参数，该参数接受员工的姓名并返回员工部门的名称。  
  
     执行语句时，驱动程序会将参数的数据发送到数据源;\**参数ValuePtr*缓冲区必须包含有效的输入值，或者\**StrLen_or_IndPtr*缓冲区必须包含SQL_NULL_DATA、SQL_DATA_AT_EXEC 或SQL_LEN_DATA_AT_EXEC宏的结果。 执行语句后，驱动程序将参数的数据返回给应用程序;如果数据源未返回输入/输出参数的值，驱动程序将 **StrLen_or_IndPtr*缓冲区设置为SQL_NULL_DATA。  
  
    > [!NOTE]  
    >  当 ODBC 1.0 应用程序在 ODBC 2.0 驱动程序中调用**SQLSetParam**时，驱动程序管理器将其转换为**SQLBind参数**的调用，其中*输入输出类型*参数设置为SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT 参数在过程中标记过程或输出参数的返回值;在这两种情况下，这些参数称为*输出参数*。 例如 **，{？**  
  
     执行语句后，驱动程序将参数的数据返回给应用程序，除非*参数ValuePtr*和*StrLen_or_IndPtr*参数都是空指针，在这种情况下，驱动程序将丢弃输出值。 如果数据源不返回输出参数的值，驱动程序将 **StrLen_or_IndPtr*缓冲区设置为SQL_NULL_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM 指示应流式传输输入/输出参数。 **SQLGetData**可以读取零件中的参数值。 *缓冲区长度*被忽略，因为缓冲区长度将在**SQLGetData**调用时确定。 *StrLen_or_IndPtr*缓冲区的值必须包含SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_DATA_AT_EXEC 或SQL_LEN_DATA_AT_EXEC宏的结果。 如果参数将在输出时进行流式传输，则必须在输入时将参数绑定为在输入处的数据执行 （DAE） 参数。 *参数ValuePtr*可以是**SQLParamData**将作为用户定义的令牌返回的任何非空指针值，其值与*参数ValuePtr*一起传递用于输入和输出。 有关详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM 与输出参数的SQL_PARAM_INPUT_OUTPUT_STREAM相同。 **StrLen_or_IndPtr*在输入时被忽略。  
  
 下表列出了*输入输出类型*和 **StrLen_or_IndPtr*的不同组合：  
  
|InputOutputType |**StrLen_or_IndPtr*|业务成效|参数值Ptr 的评论|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC（*len*） 或SQL_DATA_AT_EXEC|零件输入|*参数ValuePtr*可以是**SQLParamData**将作为用户定义的令牌返回的任何指针值，其值是使用*参数ValuePtr*传递的。|  
|SQL_PARAM_INPUT|不SQL_LEN_DATA_AT_EXEC（*len*） 或SQL_DATA_AT_EXEC|输入绑定缓冲区|*参数值Ptr*是输入缓冲区的地址。|  
|SQL_PARAM_OUTPUT|在输入时忽略。|输出绑定缓冲区|*参数值Ptr*是输出缓冲区的地址。|  
|SQL_PARAM_OUTPUT_STREAM|在输入时忽略。|流输出|*参数ValuePtr*可以是任何指针值 **，SQLParamData**将作为用户定义的令牌返回，其值是使用*参数ValuePtr*传递的。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC（*len*） 或SQL_DATA_AT_EXEC|零件和输出绑定缓冲区中的输入|*参数ValuePtr*是输出缓冲区的地址 **，SQLParamData**也将作为用户定义的令牌返回，其值随*参数ValuePtr*传递。|  
|SQL_PARAM_INPUT_OUTPUT|不SQL_LEN_DATA_AT_EXEC（*len*） 或SQL_DATA_AT_EXEC|输入绑定缓冲区和输出绑定缓冲区|*参数值Ptr*是共享输入/输出缓冲区的地址。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC（*len*） 或SQL_DATA_AT_EXEC|零件输入和流输出|*参数ValuePtr*可以是任何非空指针值 **，SQLParamData**将作为用户定义的令牌返回，其值与*参数ValuePtr*一起传递用于输入和输出。|  
  
> [!NOTE]  
>  当应用程序将输出或输入输出参数绑定为流式处理时，驱动程序必须决定允许哪些 SQL 类型。 驱动程序管理器不会为无效的 SQL 类型生成错误。  
  
## <a name="valuetype-argument"></a>值类型参数

 *ValueType*参数指定参数的 C 数据类型。 此参数设置 APD 的SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE字段。 这必须是附录 D：数据类型的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分中的值之一。  
  
 如果*ValueType*参数是间隔数据类型之一，则 APD*的参数编号*记录的SQL_DESC_TYPE字段设置为SQL_INTERVAL，APD 的SQL_DESC_CONCISE_TYPE字段设置为简洁的间隔数据类型，*并且参数编号*记录的SQL_DESC_DATETIME_INTERVAL_CODE字段设置为特定间隔数据类型的子代码。 （参见[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。数据分别用于 APD 的SQL_DESC_DATETIME_INTERVAL_PRECISION和SQL_DESC_PRECISION字段中设置的默认间隔前导精度 （2） 和默认间隔秒精度 （6）。 如果任一默认精度不合适，则应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置描述符字段。  
  
 如果*ValueType*参数是日期时间数据类型之一，则 APD*的参数编号*记录的SQL_DESC_TYPE字段设置为SQL_DATETIME，APD*的参数编号*记录的SQL_DESC_CONCISE_TYPE字段设置为简明的日期时间 C 数据类型，*并且参数编号*记录的SQL_DESC_DATETIME_INTERVAL_CODE字段设置为特定日期时间数据类型的子代码。 （参见[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 如果*ValueType*参数是SQL_C_NUMERIC数据类型，则数据将使用在 APD 的SQL_DESC_PRECISION和SQL_DESC_SCALE字段中设置的默认精度（即驱动程序定义）和默认比例 （0）。 如果默认精度或比例不合适，则应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置描述符字段。  
  
 SQL_C_DEFAULT指定参数值从参数*类型*指定的 SQL 数据类型的默认 C 数据类型传输。  
  
 您还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 有关详细信息，请参阅默认[C 数据类型](../../../odbc/reference/appendixes/default-c-data-types.md)、[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)，以及将[数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)，参见附录 D：数据类型。  
  
## <a name="parametertype-argument"></a>参数类型参数

 这必须是附录 D：数据类型的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)部分中列出的值之一，或者它必须是特定于驱动程序的值。 此参数设置 IPD 的SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE字段。  
  
 如果*参数类型*参数是日期时间标识符之一，则 IPD 的SQL_DESC_TYPE字段设置为SQL_DATETIME，IPD 的SQL_DESC_CONCISE_TYPE字段设置为简明的日期时间 SQL 数据类型，并且SQL_DESC_DATETIME_INTERVAL_CODE字段设置为相应的日期时间子代码值。  
  
 如果*参数类型*是间隔标识符之一，则 IPD 的SQL_DESC_TYPE字段设置为SQL_INTERVAL，IPD 的SQL_DESC_CONCISE_TYPE字段设置为简洁的 SQL 间隔数据类型，并且 IPD 的SQL_DESC_DATETIME_INTERVAL_CODE字段设置为相应的间隔子代码。 IPD 的SQL_DESC_DATETIME_INTERVAL_PRECISION字段设置为间隔前导精度，SQL_DESC_PRECISION字段设置为间隔秒精度（如果适用）。 如果SQL_DESC_DATETIME_INTERVAL_PRECISION或SQL_DESC_PRECISION的默认值不合适，则应用程序应通过调用**SQLSetDescField**显式设置它。 有关这些字段中的任何一个的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*参数是SQL_NUMERIC数据类型，则数据将使用在 IPD SQL_DESC_PRECISION和SQL_DESC_SCALE字段中设置的默认精度（即驱动程序定义）和默认比例 （0）。 如果默认精度或比例不合适，则应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置描述符字段。  
  
 有关数据转换方式的信息，请参阅在附录 D：数据类型中[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)以及[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
## <a name="columnsize-argument"></a>列大小参数

 *ColumnSize*参数指定对应于参数标记的列或表达式的大小、该数据的长度或两者。 此参数设置 IPD 的不同字段，具体取决于 SQL 数据类型（*参数类型*参数）。 以下规则适用于此映射：  
  
-   如果*参数类型*为SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY或其中一个简洁的 SQL 日期时间或间隔数据类型，则 IPD 的SQL_DESC_LENGTH字段将设置为*列Size*的值。 （有关详细信息，请参阅附录 D：数据类型中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)部分。  
  
-   如果*参数类型*为SQL_DECIMAL、SQL_NUMERIC、SQL_FLOAT、SQL_REAL或SQL_DOUBLE，则 IPD 的SQL_DESC_PRECISION字段将设置为*列Size*的值。  
  
-   对于其他数据类型，将忽略*ColumnSize*参数。  
  
 有关详细信息，请参阅"传递参数值"和 *"StrLen_or_IndPtr*参数"中的SQL_DATA_AT_EXEC。  
  
## <a name="decimaldigits-argument"></a>十进制数字参数

 如果*参数类型*为SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、SQL_INTERVAL_SECOND、SQL_INTERVAL_DAY_TO_SECOND、SQL_INTERVAL_HOUR_TO_SECOND或SQL_INTERVAL_MINUTE_TO_SECOND，则 IPD 的SQL_DESC_PRECISION字段设置为*十进制数字*。 如果*参数类型*为SQL_NUMERIC或SQL_DECIMAL，则 IPD 的SQL_DESC_SCALE字段设置为*十进制数字*。 对于所有其他数据类型，将忽略*十进制数字*参数。  
  
## <a name="parametervalueptr-argument"></a>参数值 Ptr 参数

 *参数ValuePtr*参数指向一个缓冲区，当调用**SQLExecute**或**SQLExecDirect**时，该缓冲区包含参数的实际数据。 数据必须采用*ValueType*参数指定的格式。 此参数设置 APD 的SQL_DESC_DATA_PTR字段。 应用程序可以将*参数ValuePtr*参数设置为空指针，只要*\*StrLen_or_IndPtrSQL_NULL_DATA*或SQL_DATA_AT_EXEC。 （这仅适用于输入或输入/输出参数。  
  
 如果\**StrLen_or_IndPtr*是SQL_LEN_DATA_AT_EXEC（*长度*）宏或SQL_DATA_AT_EXEC的结果，则*参数ValuePtr*是与参数关联的应用程序定义的指针值。 它通过**SQLParamData**返回到应用程序。 例如，*参数ValuePtr*可能是非零令牌，如参数编号、指向数据的指针或指向应用程序用于绑定输入参数的结构的指针。 但是，请注意，如果参数是输入/输出参数，*则参数ValuePtr*必须是指向将存储输出值的缓冲区的指针。 如果SQL_ATTR_PARAMSET_SIZE语句属性中的值大于 1，则应用程序可以使用SQL_ATTR_PARAMS_PROCESSED_PTR语句属性指向的值以及*参数ValuePtr*参数。 例如 *，ParameterValuePtr*可能指向值数组，应用程序可能使用SQL_ATTR_PARAMS_PROCESSED_PTR指向的值从数组中检索正确的值。 有关详细信息，请参阅本节后面的"传递参数值"。  
  
 如果*输入输出类型*参数SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT，*则参数ValuePtr*指向一个缓冲区，其中驱动程序返回输出值。 如果过程返回一个或多个结果集，\*则在处理完所有结果集/行计数之前，不能保证设置*参数ValuePtr*缓冲区。 如果在处理完成之前未设置缓冲区，则在**SQLMore 结果**返回SQL_NO_DATA之前，输出参数和返回值不可用。 使用SQL_CLOSE选项调用**SQLCloseCursor 或** **SQLFreeStmt**将导致丢弃这些值。  
  
 如果SQL_ATTR_PARAMSET_SIZE语句属性中的值大于 1，*则参数ValuePtr*指向数组。 单个 SQL 语句处理输入或输入/输出参数的完整输入值数组，并返回输入/输出参数的输出值数组。  
  
## <a name="bufferlength-argument"></a>缓冲区长度参数

 对于字符和二进制 C 数据 *，BufferLength*参数指定\**参数ValuePtr*缓冲区的长度（如果是单个元素）或\**参数ValuePtr*数组中元素的长度（如果SQL_ATTR_PARAMSET_SIZE语句属性中的值大于 1）。 此参数设置 APD SQL_DESC_OCTET_LENGTH记录字段。 如果应用程序指定多个值，*则缓冲区长度*用于确定在输入和输出上在 **参数ValuePtr*数组中的值的位置。 对于输入/输出和输出参数，它用于确定是否截截输出上的字符和二进制 C 数据：  
  
-   对于字符 C 数据，如果可供返回的字节数大于或等于*BufferLength，* 则\**参数ValuePtr*中的数据被截断为*BufferLength 减去*空终止字符的长度，并且被驱动程序终止。  
  
-   对于二进制 C 数据，如果可供返回的字节数大于*BufferLength，* 则\**参数ValuePtr*中的数据将被截断为*缓冲区长度*字节。  
  
 对于所有其他类型的 C 数据，将忽略*BufferLength*参数。 \**参数ValuePtr*缓冲区的长度（如果是单个元素）或\**参数ValuePtr*数组中元素的长度（如果应用程序调用**SQLSetStmtAttr，***属性*参数为 SQL_ATTR_PARAMSET_SIZE为每个参数指定多个值）假定为 C 数据类型的长度。  
  
 对于流式输出或流输入/输出参数，*将忽略缓冲区长度*参数，因为缓冲区长度是在**SQLGetData**中指定的。  
  
> [!NOTE]  
>  当 ODBC 1.0 应用程序在 ODBC 3 中调用**SQLSetParam**时。*x*驱动程序，驱动程序管理器将其转换为**SQLBind参数**的调用，其中*缓冲区长度*参数始终SQL_SETPARAM_VALUE_MAX。 因为如果 ODBC 3，驱动程序管理器将返回错误。*x*应用程序将*缓冲区长度*设置为 SQL_SETPARAM_VALUE_MAX，即 ODBC 3。*x*驱动程序可以用它来确定 ODBC 1.0 应用程序何时调用它。  
  
> [!NOTE]  
>  在**SQLSetParam**中，应用程序指定 **参数ValuePtr*缓冲区的长度，以便驱动程序可以返回字符或二进制数据的方式，以及应用程序向驱动程序发送字符或二进制参数值数组的方式是驱动程序定义的。  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr参数

 *StrLen_or_IndPtr*参数指向一个缓冲区，当调用**SQLExecute**或**SQLExecDirect**时，该缓冲区包含以下一个缓冲区。 （此参数设置应用程序参数指针的SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR记录字段。  
  
-   存储在 **参数值Ptr*中的参数值的长度。 除字符或二进制 C 数据外，将忽略此。  
  
-   SQL_NTS 参数值是 null 端接字符串。  
  
-   SQL_NULL_DATA 参数值为 NULL。  
  
-   SQL_DEFAULT_PARAM 过程是使用参数的默认值，而不是从应用程序检索的值。 此值仅在 ODBC 规范语法中调用的过程中有效，并且仅当*inputOutputType*参数SQL_PARAM_INPUT、SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_INPUT_OUTPUT_STREAM时才有效。 \* *SQL_DEFAULT_PARAMStrLen_or_IndPtr*时，*值类型*、*参数类型*、*列大小*、*十进制数字*、*缓冲区长度*和*参数值Ptr*参数将被忽略输入参数，并且仅用于定义输入/输出参数的输出参数值。  
  
-   SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果。 参数的数据将与**SQLPutData 一**起发送。 如果*参数类型*参数为 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或特定于数据源的长数据类型，并且驱动程序返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型的"Y"，*则长度*是要为参数发送的数据字节数;否则，*长度*必须为非负值，并且将被忽略。 有关详细信息，请参阅本节后面的"传递参数值"。  
  
     例如，为了指定在一个或多个调用中使用**SQLPutData**发送 10，000 字节的数据，对于SQL_LONGVARCHAR参数，应用程序集 =*StrLen_or_IndPtrSQL_LEN_DATA_AT_EXEC* （10000）。  
  
-   SQL_DATA_AT_EXEC 参数的数据将与**SQLPutData 一**起发送。 当 ODBC 1.0 应用程序调用 ODBC 3 时，将使用此值。*x*驱动程序。 有关详细信息，请参阅本节后面的"传递参数值"。  
  
 如果*StrLen_or_IndPtr*为空指针，则驱动程序假定所有输入参数值为非 NULL，并且该字符和二进制数据为 null 终止。 如果*输入输出类型*为SQL_PARAM_OUTPUT或SQL_PARAM_OUTPUT_STREAM*参数ValuePtr*和*StrLen_or_IndPtr*均为空指针，则驱动程序将丢弃输出值。  
  
> [!NOTE]  
>  当参数的数据类型SQL_C_BINARY时，强烈建议应用程序开发人员为*StrLen_or_IndPtr*指定空指针。 为了确保驱动程序不会意外截截SQL_C_BINARY数据 *，StrLen_or_IndPtr*应包含指向有效长度值的指针。  
  
 如果*InputOutputType*参数SQL_PARAM_INPUT_OUTPUT、SQL_PARAM_OUTPUT、SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM，*则StrLen_or_IndPtr*指向驱动程序返回SQL_NULL_DATA的缓冲区、\**可在参数ValuePtr*中返回的字节数（不包括字符数据的空端字节）或SQL_NO_TOTAL（如果无法确定可供返回的字节数）。 如果过程返回一个或多个结果集，则在提取所有结果之前，不保证设置*StrLen_or_IndPtr缓冲区*。  
  
 如果SQL_ATTR_PARAMSET_SIZE语句属性中的值大于 1，*则StrLen_or_IndPtr*指向 SQLLEN 值数组。 这些值可以是本节前面列出的任何值，并且使用单个 SQL 语句进行处理。  
  
## <a name="passing-parameter-values"></a>传递参数值

 应用程序可以在\**参数ValuePtr*缓冲区中传递参数的值，也可以通过对**SQLPutData**的一个或多个调用来传递参数的值。 其数据随**SQLPutData**传递的参数称为*执行时的数据*参数。 这些参数通常用于发送SQL_LONGVARBINARY和SQL_LONGVARCHAR参数的数据，并可以与其他参数混合。  
  
 要传递参数值，应用程序将执行以下步骤序列：  
  
1.  为每个参数调用**SQLBind参数**以绑定参数值（*参数值Ptr*参数）和长度/指示器 *（StrLen_or_IndPtr*参数）的缓冲区。 对于执行时的数据参数，*参数ValuePtr*是应用程序定义的指针值，如参数编号或数据的指针。 该值稍后将返回，可用于标识参数。  
  
2.  在\**参数ValuePtr*和 **StrLen_or_IndPtr*缓冲区中放置输入和输入/输出参数的值：  
  
    -   对于普通参数，应用程序将参数值放在\**参数ValuePtr*缓冲区中，并将该值的长度放在 **StrLen_or_IndPtr*缓冲区中。 有关详细信息，请参阅[设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   对于执行时的数据参数，应用程序将SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果（在调用 ODBC 2.0 驱动程序时）放入 **StrLen_or_IndPtr*缓冲区中。  
  
3.  调用**SQLExecute**或**SQLExecDirect**以执行 SQL 语句。  
  
    -   如果没有执行时的数据参数，该过程将完成。  
  
    -   如果存在任何执行时的数据参数，则函数将返回SQL_NEED_DATA。  
  
4.  调用**SQLParamData**检索**SQLBind参数***的参数ValuePtr*参数中指定的应用程序定义值，以便处理第一个执行时的数据参数。 **SQLParamData**返回SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  尽管执行时的数据参数类似于执行时的数据列，但**SQLParamData**返回的值因每个参数而异。 执行时的数据参数是 SQL 语句中的参数，当使用**SQLExecDirect**或**SQLExecute**执行语句时，将随**SQLPutData**一起发送数据。 它们与**SQLBind 参数**绑定。 **SQLParamData**返回的值是参数*ValuePtr*参数中传递给**SQLBind参数**的指针值。 执行时的数据列是行集中的列，当使用**SQLBulk 操作**更新或添加行或使用**SQLSetPos**更新行时，将随**SQLPutData**一起发送数据。 它们与**SQLBindCol**绑定。 **SQLParamData**返回的值是正在处理的 **TargetValuePtr*缓冲区中的行的地址（由对**SQLBindCol**的调用设置）。  
  
5.  调用**SQLPutData**一次或多次以发送参数的数据。 如果数据值大于\* **SQLPutData**中指定的*参数ValuePtr*缓冲区，则需要多个调用。仅当将字符 C 数据发送到具有字符、二进制或数据源特定数据类型的列或将二进制 C 数据发送到具有字符、二进制或数据源特定数据类型的列时，才允许对同一参数的**SQLPutData**进行多次调用。  
  
6.  再次调用**SQLParamData**以发出已为参数发送所有数据的信号。  
  
    -   如果有更多的执行数据参数 **，SQLParamData**将返回SQL_NEED_DATA和应用程序定义的值，以便处理下一个执行时的数据参数。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的数据执行参数，该过程就完成了。 如果语句成功执行 **，SQLParamData**将返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果执行失败，它将返回SQL_ERROR。 此时 **，SQLParamData**可以返回任何 SQLSTATE，该 SQLSTATE 可以由用于执行语句的函数 **（SQLExecDirect**或**SQLExecute）** 返回。  
  
         在应用程序检索语句生成的所有结果集后，\**参数ValuePtr*和 **StrLen_or_IndPtr*缓冲区中提供了任何输入/输出参数的输出值。  
  
 调用**SQLExecute**或**SQLExecDirect**将语句置于SQL_NEED_DATA状态。 此时，应用程序只能调用 SQLCancel、SQLGetDiagField、SQLGetDiagRec、SQLGet**函数****、SQLParamData**或**SQLPutData**与语句或与语句关联的*连接句柄*。 **SQLCancel** **SQLGetDiagField** **SQLGetDiagRec** 如果调用具有语句或与 语句关联的连接的任何其他函数，则函数将返回 SQLSTATE HY010（函数序列错误）。 当**SQLParamData**或**SQLPutData**返回错误 **、SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO或取消该语句时，该语句将保留SQL_NEED_DATA状态。  
  
 如果应用程序调用**SQLCancel，** 而驱动程序仍然需要执行时的数据参数，则驱动程序将取消语句执行;如果驱动程序仍需要执行时的数据，则驱动程序将取消语句执行。然后，应用程序可以再次调用**SQLExecute**或**SQLExecDirect。**  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流输出参数

 当应用程序将*InputOutputType*集到SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM时，输出参数值必须通过对**SQLGetData**的一个或多个调用来检索。 当驱动程序具有要返回到应用程序的流输出参数值时，它将返回SQL_PARAM_DATA_AVAILABLE以响应对以下函数的调用 **：SQLMore结果****、SQLExecute**和**SQLExecDirect**。 应用程序调用**SQLParamData**以确定可用的参数值。  
  
 有关SQL_PARAM_DATA_AVAILABLE和流式输出参数的详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用参数的数组

 当应用程序准备一个包含参数标记的语句并在参数数组中传递时，可以执行两种不同的方法。 一种方法是驱动程序依赖于后端的数组处理功能，在这种情况下，包含参数数组的整个语句被视为一个原子单元。 Oracle 是支持阵列处理功能的数据源的示例。 实现此功能的另一种方法是驱动程序生成一批 SQL 语句，为参数数组中每组参数生成一个 SQL 语句，并执行批处理。 参数数组不能与**更新 WHERE"当前语句**"一起使用。  
  
 处理参数数组时，单个结果集/行计数（每个参数集一个）可用，或者结果集/行计数可以汇总为一个。 **SQLGetInfo**中的SQL_PARAM_ARRAY_ROW_COUNTS选项指示行计数是可用于每组参数（SQL_PARC_BATCH）还是只有一个行计数可用（SQL_PARC_NO_BATCH）。  
  
 **SQLGetInfo**中的SQL_PARAM_ARRAY_SELECTS选项指示结果集是可用于每组参数（SQL_PAS_BATCH），还是只有一个结果集可用（SQL_PAS_NO_BATCH）。 如果驱动程序不允许使用参数数组执行结果集生成语句，SQL_PARAM_ARRAY_SELECTS返回SQL_PAS_NO_SELECT。  
  
 有关详细信息，请参阅[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 为了支持参数数组，SQL_ATTR_PARAMSET_SIZE语句属性设置为指定每个参数的值数。 如果字段大于 1，则 APD 的SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR字段必须指向数组。 每个数组的基数等于SQL_ATTR_PARAMSET_SIZE的值。  
  
 APD 的SQL_DESC_ROWS_PROCESSED_PTR字段指向包含已处理的参数集数（包括错误集）的缓冲区。 处理每组参数时，驱动程序在缓冲区中存储一个新值。 如果这是空指针，则不会返回任何数字。 使用参数数组时，即使设置函数返回SQL_ERROR，也会填充 APD SQL_DESC_ROWS_PROCESSED_PTR 字段指向的值。 如果返回SQL_NEED_DATA，则 APD 的SQL_DESC_ROWS_PROCESSED_PTR字段指向的值将设置为正在处理的参数集。  
  
 绑定参数数组并执行**更新 WHERE CURRENT 语句**时发生的情况是驱动程序定义的。  
  
## <a name="column-wise-parameter-binding"></a>列-威斯参数绑定

 在按列绑定中，应用程序将单独的参数和长度/指标数组绑定到每个参数。  
  
 要使用按列绑定，应用程序首先将SQL_ATTR_PARAM_BIND_TYPE语句属性设置为SQL_PARAM_BIND_BY_COLUMN。 （这是默认值。对于要绑定的每个列，应用程序执行以下步骤：  
  
1.  分配参数缓冲区数组。  
  
2.  分配长度/指示器缓冲区的数组。  
  
    > [!NOTE]  
    >  如果使用按列绑定时应用程序直接写入描述符，则可以将单独的数组用于长度和指标数据。  
  
3.  使用以下参数调用**SQLBind 参数**：  
  
    -   *ValueType*是参数缓冲区数组中单个元素的 C 类型。  
  
    -   *参数类型*是参数的 SQL 类型。  
  
    -   *参数ValuePtr*是参数缓冲区数组的地址。  
  
    -   *缓冲区长度*是参数缓冲区数组中单个元素的大小。 当数据为固定长度数据时，将忽略*BufferLength*参数。  
  
    -   *StrLen_or_IndPtr*长度/指示器数组的地址。  
  
 有关如何使用此信息的详细信息，请参阅本节后面的"注释"中的"参数值驱动器"。 有关参数的按列绑定的详细信息，请参阅[参数的绑定数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>行-威斯参数绑定

 在按行绑定中，应用程序定义一个结构，该结构包含要绑定的每个参数的参数和长度/指示器缓冲区。  
  
 要使用行绑定，应用程序将执行以下步骤：  
  
1.  定义一个结构来容纳一组参数（包括参数和长度/指标缓冲区），并分配这些结构的数组。  
  
    > [!NOTE]  
    >  如果使用按行绑定时应用程序直接写入描述符，则可以将单独的字段用于长度和指标数据。  
  
2.  将SQL_ATTR_PARAM_BIND_TYPE语句属性设置为包含单个参数集的结构大小，或将参数绑定到的缓冲区实例的大小。 长度必须包括所有绑定参数的空间以及结构或缓冲区的任何填充，以确保当绑定参数的地址以指定长度递增时，结果将指向下一行中同一参数的开头。 当您在 ANSI C 中使用*大小运算符*时，此行为是有保证的。  
  
3.  调用**SQLBind 参数**，对要绑定的每个参数进行以下参数：  
  
    -   *ValueType*是要绑定到列的参数缓冲区成员的类型。  
  
    -   *参数类型*是参数的 SQL 类型。  
  
    -   *参数ValuePtr*是第一个数组元素中的参数缓冲区成员的地址。  
  
    -   *缓冲区长度*是参数缓冲区成员的大小。  
  
    -   *StrLen_or_IndPtr*是要绑定的长度/指示器成员的地址。  
  
 有关如何使用此信息的详细信息，请参阅本节后面的"*参数值驱动器*"。 有关参数行绑定的详细信息，请参阅[参数的绑定数组](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>错误信息

 如果驱动程序未将参数数组实现为批处理（SQL_PARAM_ARRAY_ROW_COUNTS 选项等于SQL_PARC_NO_BATCH），则错误情况将像执行一个语句一样处理。 如果驱动程序确实将参数数组实现为批处理，则应用程序可以使用 IPD 的SQL_DESC_ARRAY_STATUS_PTR标头字段来确定 SQL 语句的哪个参数或参数数组中的哪个参数导致**SQLExecDirect**或**SQLExecute**返回错误。 此字段包含每行参数值的状态信息。 如果字段指示已发生错误，则诊断数据结构中的字段将指示失败的参数的行和参数编号。 数组中的元素数将由 APD 中的SQL_DESC_ARRAY_SIZE标头字段定义，该字段可以由SQL_ATTR_PARAMSET_SIZE语句属性设置。  
  
> [!NOTE]  
>  APD 中的SQL_DESC_ARRAY_STATUS_PTR标头字段用于忽略参数。 有关忽略参数的详细信息，请参阅下一节"忽略一组参数"。  
  
 当 SQLExecute 或**SQLExecDirect**返回SQL_ERROR时，IPD 中SQL_DESC_ARRAY_STATUS_PTR字段指向的数组中的元素将包含SQL_PARAM_ERROR、SQL_PARAM_SUCCESS、SQL_PARAM_SUCCESS_WITH_INFO、SQL_PARAM_UNUSED或SQL_PARAM_DIAG_UNAVAILABLE。 **SQLExecDirect**  
  
 对于此数组中的每个元素，诊断数据结构包含一个或多个状态记录。 结构的SQL_DIAG_ROW_NUMBER字段指示导致错误的参数值的行号。 如果可以确定导致错误的参数行中的特定参数，则参数编号将在SQL_DIAG_COLUMN_NUMBER字段中输入。  
  
 当未使用参数时，将输入SQL_PARAM_UNUSED，因为早期参数中发生错误，迫使**SQLExecute**或**SQLExecDirect**中止。 例如，如果执行导致 SQLExecute 或**SQLExecDirect**中止的第四十个参数集时出现 50 个参数**SQLExecDirect**并发生错误，则在参数 41 到 50 的状态数组中输入SQL_PARAM_UNUSED。  
  
 当驱动程序将参数数组视为单片单元时，将输入SQL_PARAM_DIAG_UNAVAILABLE，因此不会生成此单个参数级别的错误信息。  
  
 处理单个参数集时出现一些错误会导致数组中后续参数集的处理停止。 其他错误不会影响后续参数的处理。 哪些错误将停止处理是驱动程序定义的。 如果未停止处理，则处理数组中的所有参数，SQL_SUCCESS_WITH_INFO由于错误而返回，SQL_ATTR_PARAMS_PROCESSED_PTR定义的缓冲区设置为处理的参数集总数（由SQL_ATTR_PARAMSET_SIZE语句属性定义），其中包括错误集。  
  
> [!CAUTION]  
>  ODBC 处理参数数组时发生错误时，ODBC 行为在 ODBC 3 中是不同的。*x*比在ODBC 2中。*x*. . 在 ODBC 2 中。*x，SQL_ERROR*返回的功能，处理停止。 **SQLParamOptions** *的 pirow*参数指向的缓冲区包含错误行的数量。 在 ODBC 3 中。*x*，函数返回SQL_SUCCESS_WITH_INFO，处理可以停止或继续。 如果继续，SQL_ATTR_PARAMS_PROCESSED_PTR指定的缓冲区将设置为处理的所有参数的值，包括导致错误的参数的值。 这种行为更改可能会导致现有应用程序出现问题。  
  
 当 SQLExecute 或**SQLExecDirect**在完成参数数组中所有参数集的处理之前返回时（例如返回SQL_ERROR或SQL_NEED_DATA时，状态数组包含已处理的参数的状态。 **SQLExecDirect** IPD 中SQL_DESC_ROWS_PROCESSED_PTR字段指向的位置包含参数数组中导致SQL_ERROR或SQL_NEED_DATA错误代码的行号。 当参数数组发送到 SELECT 语句时，状态数组值的可用性由驱动程序定义;在执行语句或提取结果集后，它们可能可用。  
  
## <a name="ignoring-a-set-of-parameters"></a>忽略一组参数

 APD 的SQL_DESC_ARRAY_STATUS_PTR字段（由SQL_ATTR_PARAM_STATUS_PTR语句属性设置）可用于指示应忽略 SQL 语句中的一组绑定参数。 要指示驱动程序在执行期间忽略一组或多组参数，应用程序应遵循以下步骤：  
  
1.  调用**SQLSetDescField**将 APD 的SQL_DESC_ARRAY_STATUS_PTR标头字段设置为指向 SQLUSMALLINT 值数组以包含状态信息。 此字段也可以通过使用 SQL_ATTR_PARAM_OPERATION_PTR 属性调用**SQLSetStmtAttr**来设置，该*属性*允许应用程序在不获取描述符句柄的情况下设置字段。  
  
2.  将 APD SQL_DESC_ARRAY_STATUS_PTR字段定义的数组的每个元素设置为两个值之一：  
  
    -   SQL_PARAM_IGNORE，以指示该行从语句执行中排除。  
  
    -   SQL_PARAM_PROCEED，以指示该行包含在语句执行中。  
  
3.  调用**SQLExecDirect**或**SQLExecute**以执行准备好的语句。  
  
 以下规则适用于 APD 的SQL_DESC_ARRAY_STATUS_PTR字段定义的数组：  
  
-   默认情况下，指针设置为 null。  
  
-   如果指针为空，则使用所有参数集，就像所有元素都设置为SQL_ROW_PROCEED一样。  
  
-   将元素设置为SQL_PARAM_PROCEED并不保证该操作将使用该特定参数集。  
  
-   SQL_PARAM_PROCEED在头文件中定义为 0。  
  
 应用程序可以将 APD 中的SQL_DESC_ARRAY_STATUS_PTR字段设置为指向与 IRD 中SQL_DESC_ARRAY_STATUS_PTR字段指向的数组相同的数组。 当将参数绑定到行数据时，这非常有用。 然后，可以根据行数据的状态忽略参数。 除了SQL_PARAM_IGNORE之外，以下代码还会导致忽略 SQL 语句中的参数：SQL_ROW_DELETED、SQL_ROW_UPDATED和SQL_ROW_ERROR。 除了SQL_PARAM_PROCEED，以下代码还会导致 SQL 语句继续：SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO和SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新绑定参数

 应用程序可以执行两个操作中的任何一个来更改绑定：  
  
-   调用**SQLBind 参数**为已绑定的列指定新的绑定。 驱动程序用新绑定覆盖旧绑定。  
  
-   指定要添加到由绑定调用**SQLBind参数**指定的缓冲区地址的偏移量。 有关详细信息，请参阅下一节"使用偏移重新绑定"。  
  
## <a name="rebinding-with-offsets"></a>使用偏移重新绑定

 当应用程序具有可以包含许多参数的缓冲区设置，但调用**SQLExecDirect**或**SQLExecute**仅使用少数参数时，参数的重新绑定特别有用。 缓冲区中的剩余空间可以通过偏移量修改现有绑定来用于下一组参数。  
  
 APD 中的SQL_DESC_BIND_OFFSET_PTR标头字段指向绑定偏移量。 如果该字段为非空，则驱动程序将引用指针，如果SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR字段中没有任何值是空指针，则在执行时将已引用的值添加到描述符记录中的这些字段。 执行 SQL 语句时，将使用新的指针值。 重新绑定后偏移量仍然有效。 由于SQL_DESC_BIND_OFFSET_PTR是指向偏移量的指针，而不是偏移本身，因此应用程序可以直接更改偏移量，而无需调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)来更改描述符字段。 默认情况下，指针设置为 null。 ARD 的SQL_DESC_BIND_OFFSET_PTR字段可以通过调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或调用[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)进行设置，该字段具有 SQL_ATTR_PARAM_BIND_OFFSET_PTR*属性*。  
  
 绑定偏移量始终直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR字段中的值。 如果偏移更改为其他值，则新值仍直接添加到每个描述符字段中的值。 新偏移量不会添加到字段值和任何较早的偏移量之和中。  
  
## <a name="descriptors"></a>描述符

 参数的绑定方式由 AD 和 IpD 的字段决定。 **SQLBind参数**中的参数用于设置这些描述符字段。 字段也可以由**SQLSetDescField**函数设置，尽管**SQLBind参数**的使用效率更高，因为应用程序不必获取描述符句柄来调用**SQLBind参数**。  
  
> [!CAUTION]  
>  为一个语句调用**SQLBind 参数**可能会影响其他语句。 当显式分配与语句关联的 ARD 并且也与其他语句关联时，将发生这种情况。 由于**SQLBindParameter**修改 APD 的字段，因此修改将应用于与此描述符关联的所有语句。 如果这不是必需的行为，则应用程序应在调用**SQLBind参数**之前将此描述符与其他语句分离。  
  
 从概念上讲 **，SQLBind参数**按顺序执行以下步骤：  
  
1.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获取 APD 句柄。  
  
2.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)获取 APD 的SQL_DESC_COUNT字段，如果*列数*参数的值超过SQL_DESC_COUNT的值，则调用**SQLSetDescField**以将SQL_DESC_COUNT的值增加到*列号*。  
  
3.  多次调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)将值分配给 APD 的以下字段：  
  
    -   将SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE*的值设置为 ValueType，* 但除非*ValueType*是日期时间或间隔子类型的简洁标识符之一，则它将SQL_DESC_TYPE分别设置为SQL_DATETIME或SQL_INTERVAL，将SQL_DESC_CONCISE_TYPE设置为简洁标识符，并将SQL_DESC_DATETIME_INTERVAL_CODE设置为相应的日期时间或间隔子代码。  
  
    -   将SQL_DESC_OCTET_LENGTH字段设置为*缓冲区长度*的值。  
  
    -   将SQL_DESC_DATA_PTR字段设置为*参数值*的值。  
  
    -   将SQL_DESC_OCTET_LENGTH_PTR字段设置为*StrLen_or_Ind*的值。  
  
    -   将SQL_DESC_INDICATOR_PTR字段也设置为*StrLen_or_Ind*的值。  
  
     *StrLen_or_Ind*参数指定指标信息和参数值的长度。  
  
4.  调用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以获取 IPD 句柄。  
  
5.  调用[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)获取 IPD 的SQL_DESC_COUNT字段，如果*列号*参数的值超过SQL_DESC_COUNT的值，则调用**SQLSetDescField**将SQL_DESC_COUNT的值增加到*列号*。  
  
6.  多次调用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)将值分配给 IPD 的以下字段：  
  
    -   将参数*类型*的值集SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE，但参数*类型*是日期时间或间隔子类型的简洁标识符之一，则SQL_DESC_TYPE设置为SQL_DATETIME或SQL_INTERVAL，分别将SQL_DESC_CONCISE_TYPE设置为简洁标识符，并将SQL_DESC_DATETIME_INTERVAL_CODE设置为相应的日期时间或间隔子代码。  
  
    -   设置一个或多个SQL_DESC_LENGTH、SQL_DESC_PRECISION和SQL_DESC_DATETIME_INTERVAL_PRECISION，适用于*参数类型*。  
  
    -   SQL_DESC_SCALE将"*小数位数"* 的值设置。  
  
 如果对**SQLBind参数**的调用失败，它将在 APD 中设置的描述符字段的内容未定义，并且 APD 的SQL_DESC_COUNT字段保持不变。 此外，IPD 中相应记录SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_TYPE字段未定义，IPD 的SQL_DESC_COUNT字段保持不变。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>转换呼叫到和从 SQLSetParam

 当 ODBC 1.0 应用程序在 ODBC 3 中调用**SQLSetParam**时。*x*驱动程序，ODBC 3。*x*驱动程序管理器映射调用，如下表所示。  
  
|ODBC 1.0 应用程序呼叫|致电 ODBC 3。*x*驱动程序|  
|----------------------------------|-------------------------------|  
|SQLSetParam（语句处理、参数编号、值类型、参数类型、长度精度、参数刻度、参数值Ptr、StrLen_or_IndPtr）;|SQLBind参数（语句句柄、参数编号、SQL_PARAM_INPUT_OUTPUT、值类型、参数类型、*列大小*、*十进制数字*、参数值Ptr、SQL_SETPARAM_VALUE_MAX、StrLen_or_IndPtr）;|  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序准备一个 SQL 语句将数据插入到 ORDERS 表中。 对于语句中的每个参数，应用程序调用**SQLBindparameter**来指定参数的 ODBC C 数据类型和 SQL 数据类型，并将缓冲区绑定到每个参数。 对于每行数据，应用程序为每个参数分配数据值，并调用**SQLExecute**执行语句。  
  
 以下示例假定您的计算机上具有与北风数据库关联的称为北风的 ODBC 数据源。  
  
 有关更多代码示例，请参阅[SQLBulk 操作函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQL程序函数](../../../odbc/reference/syntax/sqlprocedures-function.md)[、SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)和[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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

 在下面的示例中，应用程序使用命名参数执行 SQL Server 存储过程。  
  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回语句中有关参数的信息|[SQLDescribeParam 函数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在语句上释放参数缓冲区|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回语句参数数|[SQLNumParams 函数](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|返回下一个参数以发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多个参数值|[SQLParamOptions 函数](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另请参阅

 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
