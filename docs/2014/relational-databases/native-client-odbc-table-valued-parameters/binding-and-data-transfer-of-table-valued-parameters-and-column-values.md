---
title: 绑定及数据传输的表值参数和列值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26bcf31c2d4e0d188e93587dd9bdec1a9ff382e0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533984"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>表值参数和列值的绑定及数据传输
  与其他参数类似，表值参数在传递到服务器之前必须进行绑定。 应用程序绑定表值参数绑定其他参数的相同方式： 通过使用 SQLBindParameter 或 SQLSetDescField 或 SQLSetDescRec 等效调用。 表值参数的服务器数据类型为 SQL_SS_TABLE。 C 类型可以指定为 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，只支持输入表值参数。 因此，任何将 SQL_DESC_PARAMETER_TYPE 设置为 SQL_PARAM_INPUT 之外的值的尝试，都将返回具有 SQLSTATE = HY105 和消息“参数类型无效”的 SQL_ERROR。  
  
 可使用属性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 为整个表值参数列分配默认值。 单个表值参数列的值，但是，不能分配默认值通过使用在 SQL_DEFAULT_PARAM *StrLen_or_IndPtr* SQLBindParameter 使用。 通过使用 SQL_DEFAULT_PARAM 中的，不能作为一个整体的表值参数设置为默认值*StrLen_or_IndPtr* SQLBindParameter 使用。 如果未遵循这些规则，SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR。 诊断记录将生成具有 SQLSTATE = 07S01 和消息"的默认参数的参数使用无效\<p >"，其中\<p > 为 TVP 在查询语句中的序号。  
  
 绑定表值参数之后，应用程序随后必须绑定每个表值参数列。 若要执行此操作，该应用程序首先调用 SQLSetStmtAttr 将 SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后该应用程序将表值参数的列绑定通过调用以下例程：SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField。 将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0 可还原的常见效果 SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField 对常规顶级参数中。  
  
 对于表值参数本身而言，并未发送或接收实际数据，但对于表值参数的每个构成列而言，发送和接收了数据。 由于表值参数是伪列，因此将使用 SQLBindParameter 的参数，如下所示为不同的属性比其他数据类型，请参阅：  
  
|参数|对于非表值参数类型，包括列的相关的属性|表值参数的相关属性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 对于表值参数列，此属性设置必须与表值参数自身的设置相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 此属性必须为 SQL_PARAM_INPUT。|  
|*ValueType*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*ParameterType*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_SS_TABLE。|  
|*ColumnSize*|IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 这取决于值*ParameterType*。|SQL_DESC_ARRAY_SIZE<br /><br /> 当参数焦点设置为表值参数时，也可以使用 SQL_ATTR_PARAM_SET_SIZE 进行设置。<br /><br /> 对于表值参数，此属性为表值参数列缓冲区内的行数。|  
|*DecimalDigits*|IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用。 此属性必须为 0。<br /><br /> 如果此参数为不 0，SQLBindParameter 将返回 SQL_ERROR，并且诊断记录将生成具有 SQLSTATE = HY104 和消息"无效的精度或小数位数"。|  
|*ParameterValuePtr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 此属性对于存储过程调用为可选的，并且如果不需要可以指定为 NULL。 对于非过程调用的 SQL 语句，必须指定此属性。<br /><br /> 在使用可变行绑定时，此参数还可作为应用程序用于标识该表值参数的唯一值。 有关详细信息，请参阅本主题后面的“可变表值参数行绑定”部分。<br /><br /> 当在 SQLBindParameter 调用指定表值参数类型名称时，它必须指定为 Unicode 值，即使在作为 ANSI 应用程序生成的应用程序。 用于参数的值*StrLen_or_IndPtr*应为 SQL_NTS 或乘以 sizeof （wchar） 的名称的字符串长度。|  
|*BufferLength*|APD 中的 SQL_DESC_OCTET_LENGTH。|表值参数类型名称的长度（以字节为单位）。<br /><br /> 如果类型名称为以 NULL 值结束，则它可以是 SQL_NTS；如果不需要表值参数类型名称，则为 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 对于表值参数，此属性为行计数，而非数据长度。|  
  
 表值参数支持两种数据传输模式：固定行绑定和可变行绑定。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定表值参数行绑定  
 在固定行绑定模式中，应用程序会分配足以容纳所有可能的输入列值的缓冲区（或缓冲区数组）。 应用程序执行以下操作：  
  
1.  通过使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 调用绑定所有参数。  
  
    1.  将 SQL_DESC_ARRAY_SIZE 设置为每个表值参数所能传输的最大行数。 这可以在 SQLBindParameter 调用中。  
  
2.  调用 SQLSetStmtAttr 将 SQL_SOPT_SS_PARAM_FOCUS 设置为每个表值参数的序号。  
  
    1.  每个表值参数，通过使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 调用绑定表值参数列。  
  
    2.  对于具有默认值是每个表值参数列，都会调用 SQLSetDescField 将 sql_ca_ss_col_has_default_value 设置为 1。  
  
3.  调用 SQLSetStmtAttr 将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0。 SQLExecute 之前必须进行此类也称为 SQLExecDirect。 否则，将返回 SQL_ERROR，且生成具有 SQLSTATE=HY024 和消息“属性值 SQL_SOPT_SS_PARAM_FOCUS 无效(执行时必须为零)”的诊断记录。  
  
4.  集*StrLen_or_IndPtr*或 sql_desc_octet_length_ptr 设置为 SQL_DEFAULT_PARAM 具有任何行或行数的表值参数如果要传输的下一个调用 SQLExecute 或 SQLExecDirect 的表值参数包含行。 *StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 不能设置为 SQL_NULL_DATA 为表值参数由于表值参数不可为 null （尽管表值参数构成列可以为 null）。 如果此值设置为无效值，SQLExecute 或 SQLExecDirect 返回 SQL_ERROR，并诊断记录生成具有 SQLSTATE = HY090 和消息"参数的字符串或缓冲区长度无效\<p >"，其中 p 是参数数目。  
  
5.  调用 SQLExecute 或 SQLExecDirect。  
  
 输入表值参数列值可以分块传递，是否*StrLen_or_IndPtr*设置为 SQL_LEN_DATA_AT_EXEC (*长度*) 或 sql_data_at_exec，那么列。 这类似于使用参数数组时的分块传递值。 因为所有执行时数据参数，使用 SQLParamData 不指示数组的哪一行驱动程序正在请求数据;这必须处理应用程序。 应用程序不能对驱动程序将请求值的顺序做出任何假设。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>可变表值参数行绑定  
 在可变行绑定模式中，行在执行时进行批量传输，且应用程序根据需要将行传递给驱动程序。 这类似于单个参数值的执行时数据。 对于可变行绑定，应用程序执行以下操作：  
  
1.  按照上一部分“固定表值参数行绑定”中的步骤 1 到 3 所述，绑定参数和表值参数列。  
  
2.  集*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 所要在执行时传递给 SQL_DATA_AT_EXEC 的任何表值参数。 如果未设置这两个参数，则将按照上一部分中所述步骤处理参数。  
  
3.  调用 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 参数处理为执行时数据参数，则调用将返回 SQL_NEED_DATA。 在这种情况下，应用程序执行以下操作：  
  
    -   调用 SQLParamData。 这将返回*ParameterValuePtr*值执行时数据参数和返回代码为 SQL_NEED_DATA。 当所有参数数据都传递给驱动程序时，SQLParamData 返回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 对于执行时数据参数， *ParameterValuePtr*，这等同于描述符字段 SQL_DESC_DATA_PTR 中，可被视作用于唯一地标识为其值是必需的参数的令牌。 此“标记”在绑定时从应用程序传递给驱动程序，在执行时传递回应用程序。  
  
4.  若要发送 null 表值参数的表值参数行数据，如果表值参数不的任何行，应用程序调用使用 SQLPutData *StrLen_or_Ind*设置为 SQL_DEFAULT_PARAM。  
  
     对于非 Null TVP，应用程序会：  
  
    -   集*Str_Len_or_Ind*为适当的值的所有表值参数列，并填充表值参数列不是执行时数据参数的数据缓冲区。 可以采用类似于将普通参数分块传递给驱动程序的方式，使用表值参数列的执行时数据。  
  
    -   调用与 SQLPutData *Str_Len_or_Ind*设置为行数，以发送到服务器。 范围 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 以外的任何值都将生成错误，并将返回 SQLSTATE HY090 和消息“字符串或缓冲区长度无效”。 0 表示已发送所有行，已不存在任何表值参数数据（如本列表的第二个项目符号项中所述）。 只有在驱动程序第一次请求表值参数数据时，才能使用 SQL_DEFAULT_PARAM（如本列表的第二个项目符号项中所述）。  
  
5.  在发送所有行后，使用表值参数调用 SQLPutData *Str_Len_or_Ind*值为 0，然后继续执行上述步骤 3a。  
  
6.  会再次调用 SQLParamData。 如果表值参数列之间的任何执行时数据参数，这些将能识别的值*ValuePtrPtr* SQLParamData 返回。 所有列的值可用时，将再次返回 SQLParamData *ParameterValuePtr*表值参数和应用程序的值将重新开始。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
