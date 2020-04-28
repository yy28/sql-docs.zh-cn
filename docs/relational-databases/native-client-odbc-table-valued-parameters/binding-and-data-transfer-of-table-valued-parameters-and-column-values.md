---
title: 表值参数的数据传输
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b7eecfdac3d42b7a3d8d66ffe1f8ac68652230f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304491"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>表值参数和列值的绑定及数据传输
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  与其他参数类似，表值参数在传递到服务器之前必须进行绑定。 应用程序绑定表值参数的方式与绑定其他参数的方式相同：通过使用 SQLBindParameter 或对 SQLSetDescField 或 SQLSetDescRec 的等效调用。 表值参数的服务器数据类型为 SQL_SS_TABLE。 C 类型可以指定为 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，只支持输入表值参数。 因此，任何将 SQL_DESC_PARAMETER_TYPE 设置为 SQL_PARAM_INPUT 之外的值的尝试，都将返回具有 SQLSTATE = HY105 和消息“参数类型无效”的 SQL_ERROR。  
  
 可使用属性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 为整个表值参数列分配默认值。 但是，不能使用 SQLBindParameter 中*StrLen_or_IndPtr*的 SQL_DEFAULT_PARAM 为单独的表值参数列值分配默认值。 不能将表值参数设置为默认值，方法是使用*StrLen_or_IndPtr* with SQLBindParameter 中的 SQL_DEFAULT_PARAM。 如果未遵循这些规则，则 SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR。 将使用 SQLSTATE = 07S01 和消息 "参数\<p> 使用默认参数无效" 生成诊断记录，其中\<p> 是查询语句中 TVP 的序号。  
  
 绑定表值参数之后，应用程序随后必须绑定每个表值参数列。 为此，应用程序首先调用 SQLSetStmtAttr，将 SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后，应用程序通过调用以下例程来绑定表值参数的列： SQLBindParameter、SQLSetDescRec 和 SQLSetDescField。 如果将 SQL_SOPT_SS_PARAM_FOCUS 设置为0，则会在操作常规顶级参数时还原 SQLBindParameter、SQLSetDescRec 和 SQLSetDescField 的常见影响。
 
 注意：对于使用 unixODBC 2.3.1 到2.3.4 的 Linux 和 Mac ODBC 驱动程序，当使用 SQL_CA_SS_TYPE_NAME 描述符字段将 TVP 名称设置为 SQLSetDescField 时，unixODBC 不会根据调用的确切函数（SQLSetDescFieldA/SQLSetDescFieldW）自动在 ANSI 和 Unicode 字符串之间转换。 需要始终使用带有 Unicode （UTF-16）字符串的 SQLBindParameter 或 SQLSetDescFieldW 来设置 TVP 名称。
  
 对于表值参数本身而言，并未发送或接收实际数据，但对于表值参数的每个构成列而言，发送和接收了数据。 由于表值参数是一个伪列，因此 SQLBindParameter 的参数用于引用不同于其他数据类型的属性，如下所示：  
  
|参数|非表值参数类型的相关属性，包括列|表值参数的相关属性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|InputOutputType |IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 对于表值参数列，此属性设置必须与表值参数自身的设置相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 此属性必须为 SQL_PARAM_INPUT。|  
|*ValueType*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*ParameterType*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_SS_TABLE。|  
|ColumnSize |IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 这取决于*ParameterType*的值。|SQL_DESC_ARRAY_SIZE<br /><br /> 当参数焦点设置为表值参数时，也可以使用 SQL_ATTR_PARAM_SET_SIZE 进行设置。<br /><br /> 对于表值参数，此属性为表值参数列缓冲区内的行数。|  
|DecimalDigits |IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用。 此属性必须为 0。<br /><br /> 如果此参数不是0，则 SQLBindParameter 将返回 SQL_ERROR，并将生成包含 SQLSTATE = HY104 和消息 "precision 或 scale 无效" 的诊断记录。|  
|*ParameterValuePtr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 此属性对于存储过程调用为可选的，并且如果不需要可以指定为 NULL。 对于非过程调用的 SQL 语句，必须指定此属性。<br /><br /> 在使用可变行绑定时，此参数还可作为应用程序用于标识该表值参数的唯一值。 有关详细信息，请参阅本主题后面的“可变表值参数行绑定”部分。<br /><br /> 如果在对 SQLBindParameter 的调用上指定了表值参数类型名称，则它必须指定为 Unicode 值，即使是在作为 ANSI 应用程序生成的应用程序中。 用于参数*StrLen_or_IndPtr*的值应为 SQL_NTS 或名称的字符串长度乘以 SIZEOF （WCHAR）。|  
|*BufferLength*|APD 中的 SQL_DESC_OCTET_LENGTH。|表值参数类型名称的长度（以字节为单位）。<br /><br /> 如果类型名称为以 NULL 值结束，则它可以是 SQL_NTS；如果不需要表值参数类型名称，则为 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 对于表值参数，此属性为行计数，而非数据长度。|  
||||

 表值参数支持两种数据传输模式：固定行绑定和可变行绑定。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定表值参数行绑定  
 在固定行绑定模式中，应用程序会分配足以容纳所有可能的输入列值的缓冲区（或缓冲区数组）。 应用程序执行以下操作：  
  
1.  使用 SQLBindParameter、SQLSetDescRec 或 SQLSetDescField 调用来绑定所有参数。  
  
    1.  将 SQL_DESC_ARRAY_SIZE 设置为每个表值参数所能传输的最大行数。 这可以在 SQLBindParameter 调用中完成。  
  
2.  调用 SQLSetStmtAttr，将 SQL_SOPT_SS_PARAM_FOCUS 设置为每个表值参数的序号。  
  
    1.  对于每个表值参数，使用 SQLBindParameter、SQLSetDescRec 或 SQLSetDescField 调用来绑定表值参数列。  
  
    2.  对于将具有默认值的每个表值参数列，调用 SQLSetDescField 将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 设置为1。  
  
3.  调用 SQLSetStmtAttr，将 SQL_SOPT_SS_PARAM_FOCUS 设置为0。 此操作必须在调用 SQLExecute 或 SQLExecDirect 之前完成。 否则，将返回 SQL_ERROR，且生成具有 SQLSTATE=HY024 和消息“属性值 SQL_SOPT_SS_PARAM_FOCUS 无效(执行时必须为零)”的诊断记录。  
  
4.  将*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 设置为无行的表值参数 SQL_DEFAULT_PARAM，或在下一次调用 SQLExecute 或 SQLExecDirect 时，如果表值参数包含行，则为要传输的行数。 由于表值参数不可为 null （尽管表值参数构成列可以为 null），因此不能将*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 设置为表值参数 SQL_NULL_DATA。 如果此值设置为无效值，则 SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR，并使用 SQLSTATE = HY090 和消息 "参数\<p> 的字符串或缓冲区长度无效" 生成诊断记录，其中 p 是参数号。  
  
5.  调用 SQLExecute 或 SQLExecDirect。  
  
 如果将*StrLen_or_IndPtr*设置为列的 SQL_LEN_DATA_AT_EXEC （*长度*）或 SQL_DATA_AT_EXEC，则输入表值参数列值可以在块中传递。 这类似于使用参数数组时的分块传递值。 与所有执行时数据参数一样，SQLParamData 不指示驱动程序要向哪个数组行请求数据;应用程序必须对此进行处理。 应用程序不能对驱动程序将请求值的顺序做出任何假设。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>可变表值参数行绑定  
 在可变行绑定模式中，行在执行时进行批量传输，且应用程序根据需要将行传递给驱动程序。 这类似于单个参数值的执行时数据。 对于可变行绑定，应用程序执行以下操作：  
  
1.  按照上一部分“固定表值参数行绑定”中的步骤 1 到 3 所述，绑定参数和表值参数列。  
  
2.  为要在执行时传递到 SQL_DATA_AT_EXEC 的任何表值参数设置*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR。 如果未设置这两个参数，则将按照上一部分中所述步骤处理参数。  
  
3.  调用 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 参数处理为执行时数据参数，则调用将返回 SQL_NEED_DATA。 在这种情况下，应用程序执行以下操作：  
  
    -   调用 SQLParamData。 这会返回执行时数据参数的*ParameterValuePtr*值和返回代码 SQL_NEED_DATA。 所有参数数据都传递到驱动程序后，SQLParamData 将返回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 对于执行时数据参数， *ParameterValuePtr*与描述符字段 SQL_DESC_DATA_PTR 相同，可将其视为一个标记，用于唯一标识需要其值的参数。 此“标记”在绑定时从应用程序传递给驱动程序，在执行时传递回应用程序。  
  
4.  若要为 null 表值参数发送表值参数行数据，如果表值参数没有任何行，应用程序将调用 SQLPutData 并将*StrLen_or_Ind*设置为 SQL_DEFAULT_PARAM。  
  
     对于非 Null TVP，应用程序会：  
  
    -   将所有表值参数列*Str_Len_or_Ind*设置为适当的值，并填充不是执行时数据参数的表值参数列的数据缓冲区。 可以采用类似于将普通参数分块传递给驱动程序的方式，使用表值参数列的执行时数据。  
  
    -   调用 SQLPutData，将*Str_Len_or_Ind*设置为要发送到服务器的行数。 范围 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 以外的任何值都将生成错误，并将返回 SQLSTATE HY090 和消息“字符串或缓冲区长度无效”。 0 表示已发送所有行，已不存在任何表值参数数据（如本列表的第二个项目符号项中所述）。 只有在驱动程序第一次请求表值参数数据时，才能使用 SQL_DEFAULT_PARAM（如本列表的第二个项目符号项中所述）。  
  
5.  发送完所有行后，将使用*Str_Len_or_Ind*值0对表值参数调用 SQLPutData，然后继续执行上述步骤3a。  
  
6.  再次调用 SQLParamData。 如果表值参数列中有任何执行时数据参数，则这些参数将由 SQLParamData 返回的值*ValuePtrPtr*标识。 当所有列值都可用时，SQLParamData 将再次返回表值参数的*ParameterValuePtr*值，并且该应用程序将再次开始。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
