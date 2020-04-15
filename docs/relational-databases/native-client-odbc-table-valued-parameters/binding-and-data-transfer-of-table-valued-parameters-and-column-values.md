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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304491"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>表值参数和列值的绑定及数据传输
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  与其他参数类似，表值参数在传递到服务器之前必须进行绑定。 应用程序绑定表值参数的方式与绑定其他参数的方式相同：通过使用 SQLBind 参数或等效调用 SQLSetDescField 或 SQLSetDescRec。 表值参数的服务器数据类型为 SQL_SS_TABLE。 C 类型可以指定为 SQL_C_DEFAULT 或 SQL_C_BINARY。  
  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，只支持输入表值参数。 因此，任何将 SQL_DESC_PARAMETER_TYPE 设置为 SQL_PARAM_INPUT 之外的值的尝试，都将返回具有 SQLSTATE = HY105 和消息“参数类型无效”的 SQL_ERROR。  
  
 可使用属性 SQL_CA_SS_COL_HAS_DEFAULT_VALUE 为整个表值参数列分配默认值。 但是，无法使用 sqlBind*参数StrLen_or_IndPtr中*使用SQL_DEFAULT_PARAM来分配单个表值参数列值。 不能通过将SQL_DEFAULT_PARAM与 SQLBind 参数一起使用*StrLen_or_IndPtr，* 将整个表值参数设置为默认值。 如果未遵循这些规则，SQLExecute 或 SQLExecDirect 将返回SQL_ERROR。 将使用 SQLSTATE_07S01 和消息"参数\<p>的默认参数无效使用"生成诊断记录，其中\<p>是查询语句中 TVP 的表位。  
  
 绑定表值参数之后，应用程序随后必须绑定每个表值参数列。 为此，应用程序首先调用 SQLSetStmtAttr 将SQL_SOPT_SS_PARAM_FOCUS设置为表值参数的表位。 然后，应用程序通过调用以下例程（SQLBind参数、SQLSetDescRec 和 SQLSetDescField）绑定表值参数的列。 将SQL_SOPT_SS_PARAM_FOCUS设置为 0 将恢复 SQLBind参数、SQLSetDescRec 和 SQLSetDescField 在常规顶级参数上操作的通常效果。
 
 注意：对于具有 unixODBC 2.3.1 到 2.3.4 的 Linux 和 Mac ODBC 驱动程序，当使用SQL_CA_SS_TYPE_NAME描述符字段通过 SQLSetDescField 设置 TVP 名称时，unixODBC 不会根据调用的确切函数（SQLSetDescFieldA/ SQLSetDescfieldW）自动在 ANSI 和 Unicode 字符串之间转换。 必须始终使用 SQLBind 参数或 SQLSetDescFieldW 与 Unicode （UTF-16） 字符串来设置 TVP 名称。
  
 对于表值参数本身而言，并未发送或接收实际数据，但对于表值参数的每个构成列而言，发送和接收了数据。 由于表值参数是伪列，因此 SQLBind参数的参数用于引用与其他数据类型不同的属性，如下所示：  
  
|参数|非表值参数类型的相关属性，包括列|表值参数的相关属性|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|InputOutputType |IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 对于表值参数列，此属性设置必须与表值参数自身的设置相同。|IPD 中的 SQL_DESC_PARAMETER_TYPE。<br /><br /> 此属性必须为 SQL_PARAM_INPUT。|  
|*值类型*|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|APD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_C_DEFAULT 或 SQL_C_BINARY。|  
|*参数类型*|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。|IPD 中的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE。<br /><br /> 此属性必须为 SQL_SS_TABLE。|  
|ColumnSize |IPD 中的 SQL_DESC_LENGTH 或 SQL_DESC_PRECISION。<br /><br /> 这取决于*参数类型的值*。|SQL_DESC_ARRAY_SIZE<br /><br /> 当参数焦点设置为表值参数时，也可以使用 SQL_ATTR_PARAM_SET_SIZE 进行设置。<br /><br /> 对于表值参数，此属性为表值参数列缓冲区内的行数。|  
|DecimalDigits |IPD 中的 SQL_DESC_PRECISION 或 SQL_DESC_SCALE。|未使用。 此属性必须为 0。<br /><br /> 如果此参数不是 0，SQLBind参数将返回SQL_ERROR，并且将生成诊断记录与 SQLSTATE® HY104 和消息"无效精度或缩放"。|  
|*参数值Ptr*|APD 中的 SQL_DESC_DATA_PTR。|SQL_CA_SS_TYPE_NAME。<br /><br /> 此属性对于存储过程调用为可选的，并且如果不需要可以指定为 NULL。 对于非过程调用的 SQL 语句，必须指定此属性。<br /><br /> 在使用可变行绑定时，此参数还可作为应用程序用于标识该表值参数的唯一值。 有关详细信息，请参阅本主题后面的“可变表值参数行绑定”部分。<br /><br /> 当在调用 SQLBindParameter 时指定表值参数类型名称时，必须将其指定为 Unicode 值，即使在构建为 ANSI 应用程序的应用程序中也是如此。 参数*StrLen_or_IndPtr*使用的值应为SQL_NTS，或者名称的字符串长度乘以大小（WCHAR）。|  
|*缓冲区长度*|APD 中的 SQL_DESC_OCTET_LENGTH。|表值参数类型名称的长度（以字节为单位）。<br /><br /> 如果类型名称为以 NULL 值结束，则它可以是 SQL_NTS；如果不需要表值参数类型名称，则为 0。|  
|*StrLen_or_IndPtr*|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。|APD 中的 SQL_DESC_OCTET_LENGTH_PTR。<br /><br /> 对于表值参数，此属性为行计数，而非数据长度。|  
||||

 表值参数支持两种数据传输模式：固定行绑定和可变行绑定。  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>固定表值参数行绑定  
 在固定行绑定模式中，应用程序会分配足以容纳所有可能的输入列值的缓冲区（或缓冲区数组）。 应用程序执行以下操作：  
  
1.  使用 SQLBind 参数、SQLSetDescRec 或 SQLSetDescField 调用绑定所有参数。  
  
    1.  将 SQL_DESC_ARRAY_SIZE 设置为每个表值参数所能传输的最大行数。 这可以在 SQLBind 参数调用中完成。  
  
2.  调用 SQLSetStmtAttr 将SQL_SOPT_SS_PARAM_FOCUS设置为每个表值参数的表位。  
  
    1.  对于每个表值参数，使用 SQLBind 参数、SQLSetDescRec 或 SQLSetDescField 调用绑定表值参数列。  
  
    2.  对于每个具有默认值的表值参数列，调用 SQLSetDescField 将SQL_CA_SS_COL_HAS_DEFAULT_VALUE设置为 1。  
  
3.  调用 SQLSetStmtAttr 将SQL_SOPT_SS_PARAM_FOCUS设置为 0。 在调用 SQLExecute 或 SQLExecDirect 之前，必须完成此操作。 否则，将返回 SQL_ERROR，且生成具有 SQLSTATE=HY024 和消息“属性值 SQL_SOPT_SS_PARAM_FOCUS 无效(执行时必须为零)”的诊断记录。  
  
4.  将*StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR集，以SQL_DEFAULT_PARAM没有行的表值参数，或者将 SQLExecute 或 SQLExecDirect 的下一次调用时传输的行数（如果表值参数具有行）。 *StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR无法设置为表值参数的SQL_NULL_DATA，因为表值参数不是空的（尽管表值参数组成列可能是空的）。 如果将其设置为无效值，SQLExecute 或 SQLExecDirect 将返回SQL_ERROR，并且使用 SQLSTATE_HY090 和消息"参数\<p>的无效字符串或缓冲区长度"生成诊断记录，其中 p 是参数编号。  
  
5.  调用 SQLExecute 或 SQLExecDirect。  
  
 如果*StrLen_or_IndPtr*设置为SQL_LEN_DATA_AT_EXEC（*长度*）或SQL_DATA_AT_EXEC，则可以分段传递输入表值参数列值。 这类似于使用参数数组时的分块传递值。 与执行时所有数据参数一样，SQLParamData 不指示驱动程序请求数据的数组的哪一行;应用程序必须处理好这一点。 应用程序不能对驱动程序将请求值的顺序做出任何假设。  
  
## <a name="variable-table-valued-parameter-row-binding"></a>可变表值参数行绑定  
 在可变行绑定模式中，行在执行时进行批量传输，且应用程序根据需要将行传递给驱动程序。 这类似于单个参数值的执行时数据。 对于可变行绑定，应用程序执行以下操作：  
  
1.  按照上一部分“固定表值参数行绑定”中的步骤 1 到 3 所述，绑定参数和表值参数列。  
  
2.  为在执行时传递给SQL_DATA_AT_EXEC的任何表值参数设置*StrLen_or_IndPtr*或SQL_DESC_OCTET_LENGTH_PTR。 如果未设置这两个参数，则将按照上一部分中所述步骤处理参数。  
  
3.  调用 SQLExecute 或 SQLExecDirect。 如果有任何 SQL_PARAM_INPUT 或 SQL_PARAM_INPUT_OUTPUT 参数处理为执行时数据参数，则调用将返回 SQL_NEED_DATA。 在这种情况下，应用程序执行以下操作：  
  
    -   调用 SQLParamData。 这将返回执行时数据参数的*参数ValuePtr*值和SQL_NEED_DATA返回代码。 将所有参数数据传递给驱动程序后，SQLParamData 将返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或SQL_ERROR。 对于执行时的数据参数，*参数ValuePtr（* 与描述符字段SQL_DESC_DATA_PTR相同）可视为唯一标识需要值的参数的令牌。 此“标记”在绑定时从应用程序传递给驱动程序，在执行时传递回应用程序。  
  
4.  要发送空表值参数的表值参数行数据，如果表值参数没有行，则应用程序将 SQLPutData 调用 *，StrLen_or_Ind*设置为SQL_DEFAULT_PARAM。  
  
     对于非 Null TVP，应用程序会：  
  
    -   将所有表值参数列*的Str_Len_or_Ind*设置为适当的值，并为不为执行时的数据值参数列填充数据缓冲区。 可以采用类似于将普通参数分块传递给驱动程序的方式，使用表值参数列的执行时数据。  
  
    -   调用*SQLPutData，Str_Len_or_Ind*设置为要发送到服务器的行数。 范围 0 到 SQL_DESC_ARRAY_SIZE 或 SQL_DEFAULT_PARAM 以外的任何值都将生成错误，并将返回 SQLSTATE HY090 和消息“字符串或缓冲区长度无效”。 0 表示已发送所有行，已不存在任何表值参数数据（如本列表的第二个项目符号项中所述）。 只有在驱动程序第一次请求表值参数数据时，才能使用 SQL_DEFAULT_PARAM（如本列表的第二个项目符号项中所述）。  
  
5.  发送所有行后，调用 sqlPutData 的表值参数的值*Str_Len_or_Ind为*0，然后继续执行上面的步骤 3a。  
  
6.  再次调用 SQLParamData。 如果表值参数列中有任何数据执行参数，则这些参数将由 SQLParamData 返回的值*ValuePtrPtr*标识。 当所有列值都可用时，SQLParamData 将再次返回表值参数的*参数ValuePtr*值，应用程序将再次启动。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
