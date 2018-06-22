---
title: 绑定和数据传输的表值参数和列的值 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 088eaca337654ef4c8f67fc8014bee0bbcf9de85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018165"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>表值参数和列值的绑定及数据传输
  与其他参数类似，表值参数在传递到服务器之前必须进行绑定。 应用程序将表值参数绑定相同的方式，它将绑定的其他参数： 通过使用 SQLBindParameter 或等效调用 SQLSetDescField 或 SQLSetDescRec。 表值参数的服务器数据类型为 SQL_SS_TABLE。 C 类型可以指定为 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，只支持输入表值参数。 因此，任何将 SQL_DESC_PARAMETER_TYPE 设置为 SQL_PARAM_INPUT 之外的值的尝试，都将返回具有 SQLSTATE = HY105 和消息“参数类型无效”的 SQL_ERROR。  
  
 可使用属性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 为整个表值参数列分配默认值。 单个表值参数列的值，不过，不会分配默认值通过使用在 SQL_DEFAULT_PARAM *StrLen_or_IndPtr*与 SQLBindParameter。 通过使用 SQL_DEFAULT_PARAM 中的，不能作为一个整体的表值参数设置为默认值*StrLen_or_IndPtr*与 SQLBindParameter。 如果未遵循这些规则，则 SQLExecute 或 SQLExecDirect 将返回 SQL_ERROR。 将使用 SQLSTATE 生成诊断记录 = 07S01 和消息"参数不允许使用默认参数\<p >"，其中\<p > 是查询语句中 TVP 的序号。  
  
 绑定表值参数之后，应用程序随后必须绑定每个表值参数列。 若要执行此操作，在应用程序首先调用 SQLSetStmtAttr 将： SQL_SOPT_SS_PARAM_FOCUS 设置为表值参数的序号。 然后应用程序将表值参数的列绑定通过调用以下例程： SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField。 将设置： SQL_SOPT_SS_PARAM_FOCUS 为 0 的还原 SQLBindParameter、 SQLSetDescRec 和 SQLSetDescField 的常用效果在正则顶级参数运营。  
  
 对于表值参数本身而言，并未发送或接收实际数据，但对于表值参数的每个构成列而言，发送和接收了数据。 因为表值参数是一个伪列，SQLBindParameter 的参数用于指比其他数据类型，不同的属性，如下所示：  
  
|参数|非表值参数类型的相关属性，包括列|表值参数的相关属性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 对于表值参数列，此属性设置必须与表值参数自身的设置相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 此属性必须为 SQL_PARAM_INPUT。|  
|*ValueType*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*ParameterType*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_SS_TABLE。|  
|*Columnsize 类型*|IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 这取决于值*ParameterType*。|SQL_DESC_ARRAY_SIZE<br /><br /> 当参数焦点设置为表值参数时，也可以使用 SQL_ATTR_PARAM_SET_SIZE 进行设置。<br /><br /> 对于表值参数，此属性为表值参数列缓冲区内的行数。|  
|*DecimalDigits*|IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用。 此属性必须为 0。<br /><br /> 如果此参数为不 0，SQLBindParameter 将返回 SQL_ERROR 和诊断记录将生成与 SQLSTATE = HY104 和消息"无效的精度或小数位数"。|  
|*ParameterValuePtr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 此属性对于存储过程调用为可选的，并且如果不需要可以指定为 NULL。 对于非过程调用的 SQL 语句，必须指定此属性。<br /><br /> 在使用可变行绑定时，此参数还可作为应用程序用于标识该表值参数的唯一值。 有关详细信息，请参阅本主题后面的“可变表值参数行绑定”部分。<br /><br /> 当在 SQLBindParameter 调用指定的表值参数类型名称时，它必须指定为 Unicode 值，即使在应用程序生成为 ANSI 应用程序中。 用于参数的值*StrLen_or_IndPtr*应 sql_nts 以或乘以 sizeof(WCHAR) 的名称的字符串长度。|  
|*BufferLength*|APD 中的 SQL_DESC_OCTET_LENGTH。|表值参数类型名称的长度（以字节为单位）。<br /><br /> 如果类型名称为以 NULL 值结束，则它可以是 SQL_NTS；如果不需要表值参数类型名称，则为 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 对于表值参数，此属性为行计数，而非数据长度。|  
  
 表值参数支持两种数据传输模式：固定行绑定和可变行绑定。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定表值参数行绑定  
 在固定行绑定模式中，应用程序会分配足以容纳所有可能的输入列值的缓冲区（或缓冲区数组）。 应用程序执行以下操作：  
  
1.  通过使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 调用将绑定的所有参数。  
  
    1.  将 SQL_DESC_ARRAY_SIZE 设置为每个表值参数所能传输的最大行数。 进行这种 SQLBindParameter 调用中。  
  
2.  调用 SQLSetStmtAttr 将： SQL_SOPT_SS_PARAM_FOCUS 设置为每个表值参数的序号。  
  
    1.  每个表值参数，将表值参数列绑定使用 SQLBindParameter、 SQLSetDescRec 或 SQLSetDescField 调用。  
  
    2.  对于每个表值参数列都具有默认值，调用 SQLSetDescField 将 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 设置为 1。  
  
3.  调用 SQLSetStmtAttr 将： SQL_SOPT_SS_PARAM_FOCUS 设为 0。 此操作必须执行之前 SQLExecute 或 SQLExecDirect 称为。 否则，将返回 SQL_ERROR，且生成具有 SQLSTATE=HY024 和消息“属性值 SQL_SOPT_SS_PARAM_FOCUS 无效(执行时必须为零)”的诊断记录。  
  
4.  集*StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 到 SQL_DEFAULT_PARAM 表值参数与任何行或行数，如果要传输的 SQLExecute 或 SQLExecDirect 下次调用表值参数包含的行。 *StrLen_or_IndPtr*或 SQL_DESC_OCTET_LENGTH_PTR 不能设置为 SQL_NULL_DATA 表值参数是表值参数不是可以为 null （尽管表值参数构成的列可以为可以为 null）。 如果此设置为无效值、 SQLExecute 或 SQLExecDirect 返回 SQL_ERROR，和诊断记录将生成带有 SQLSTATE = HY090 和消息"的参数的字符串或缓冲区长度无效\<p >"，其中 p 是参数号。  
  
5.  调用 SQLExecute 或 SQLExecDirect。  
  
 输入表值参数列的值可以传递部分中，是否*StrLen_or_IndPtr*设置为 SQL_LEN_DATA_AT_EXEC (*长度*) 或 SQL_DATA_AT_EXEC 的列。 这类似于使用参数数组时的分块传递值。 如 SQLParamData 不使用所有数据在执行参数，指示哪些行的数组驱动程序正在请求数据;应用程序必须对此进行处理。 应用程序不能对驱动程序将请求值的顺序做出任何假设。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>可变表值参数行绑定  
 在可变行绑定模式中，行在执行时进行批量传输，且应用程序根据需要将行传递给驱动程序。 这类似于单个参数值的执行时数据。 对于可变行绑定，应用程序执行以下操作：  
  
1.  按照上一部分“固定表值参数行绑定”中的步骤 1 到 3 所述，绑定参数和表值参数列。  
  
2.  集*StrLen_or_IndPtr*或任何表值参数的要在执行时传递给 SQL_DATA_AT_EXEC SQL_DESC_OCTET_LENGTH_PTR。 如果未设置这两个参数，则将按照上一部分中所述步骤处理参数。  
  
3.  调用 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 参数处理为执行时数据参数，则调用将返回 SQL_NEED_DATA。 在这种情况下，应用程序执行以下操作：  
  
    -   调用 SQLParamData。 这将返回*ParameterValuePtr*数据在执行参数和返回代码为 SQL_NEED_DATA 的值。 当所有参数数据已都传递到该驱动程序时，SQLParamData 返回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 对于数据在执行参数， *ParameterValuePtr*，即描述符相同字段 SQL_DESC_DATA_PTR 中，可以被认为是用于唯一标识为其值是必需的参数的令牌。 此“标记”在绑定时从应用程序传递给驱动程序，在执行时传递回应用程序。  
  
4.  若要发送表值参数行数据对于 null 表值参数，如果表值参数不具有任何行，应用程序调用了与 SQLPutData *StrLen_or_Ind*设置为 SQL_DEFAULT_PARAM。  
  
     对于非 Null TVP，应用程序会：  
  
    -   集*Str_Len_or_Ind*为适当的值的所有表值参数列，并填充，则不为执行中的数据参数的表值参数列的数据缓冲区。 可以采用类似于将普通参数分块传递给驱动程序的方式，使用表值参数列的执行时数据。  
  
    -   调用与 SQLPutData *Str_Len_or_Ind*设置为的行数，以发送到服务器。 范围 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 以外的任何值都将生成错误，并将返回 SQLSTATE HY090 和消息“字符串或缓冲区长度无效”。 0 表示已发送所有行，已不存在任何表值参数数据（如本列表的第二个项目符号项中所述）。 只有在驱动程序第一次请求表值参数数据时，才能使用 SQL_DEFAULT_PARAM（如本列表的第二个项目符号项中所述）。  
  
5.  当已发送的所有行时，将使用表值参数调用 SQLPutData *Str_Len_or_Ind* 0，则继续步骤 3a 上面的值。  
  
6.  再次调用该 SQLParamData。 如果没有任何表值参数列之间的数据在执行参数，这些结果将能识别的值*ValuePtrPtr* SQLParamData 返回。 当所有列的值可用时，将再次返回 SQLParamData *ParameterValuePtr*表值参数中，和应用程序的值重新开始。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  