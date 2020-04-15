---
title: 使用参数数组 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306798"
---
# <a name="using-arrays-of-parameters"></a>使用参数的数组
要使用参数数组，应用程序将**SQLSetStmtAttr**调用*属性参数为*SQL_ATTR_PARAMSET_SIZE，以指定参数集的数量。 它调用**SQLSetStmtAttr，** 其*属性*参数为 SQL_ATTR_PARAMS_PROCESSED_PTR，以指定变量的地址，其中驱动程序可以返回处理的参数集数，包括错误集。 它调用**SQLSetStmtAttr，***属性参数为*SQL_ATTR_PARAM_STATUS_PTR，以指向一个数组，其中返回每行参数值的状态信息。 驱动程序将这些地址存储在它为语句维护的结构中。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*调用**SQLParamOptions**来为参数指定多个值。 在 ODBC 3 中。*x*，对**SQLParamOptions 的**调用已替换为对**SQLSetStmtAttr**的调用，以设置SQL_ATTR_PARAMSET_SIZE和SQL_ATTR_PARAMS_PROCESSED_ARRAY属性。  
  
 在执行语句之前，应用程序设置每个绑定数组的每个元素的值。 执行语句时，驱动程序使用它存储的信息来检索参数值并将其发送到数据源;如果可能，驱动程序应将这些值作为数组发送。 尽管参数数组的使用最好通过执行 SQL 语句与数组中的所有参数执行，对数据源进行单个调用，但此功能在 DBMS 中目前并不广泛可用。 但是，驱动程序可以通过多次执行 SQL 语句来模拟它，每个语句都使用一组参数。  
  
 在应用程序使用参数数组之前，必须确保应用程序使用的驱动程序支持它们。 有两种方法可以实现此目的：  
  
-   仅使用已知支持参数数组的驱动程序。 应用程序可以对这些驱动程序的名称进行硬编码，也可以指示用户仅使用这些驱动程序。 自定义应用程序和垂直应用程序通常使用一组有限的驱动程序。  
  
-   检查在运行时对参数数组的支持。 如果可以将SQL_ATTR_PARAMSET_SIZE语句属性设置为大于 1 的值，则驱动程序支持参数数组。 通用应用程序和垂直应用程序通常在运行时检查参数数组的支持。  
  
 可以通过使用SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS选项调用**SQLGetInfo**来确定参数化执行中的行计数和结果集的可用性。 对于**INSERT、****更新**和**删除**语句，SQL_PARAM_ARRAY_ROW_COUNTS 选项指示单个行计数（每个参数集一个）是否可用（SQL_PARC_BATCH），还是将行计数汇总为一个（SQL_PARC_NO_BATCH）。 对于**SELECT**语句，SQL_PARAM_ARRAY_SELECTS 选项指示结果集是否可用于每组参数（SQL_PAS_BATCH），还是只有一个结果集可用（SQL_PAS_NO_BATCH）。 如果驱动程序不允许使用参数数组执行结果集生成语句，则SQL_PARAM_ARRAY_SELECTS返回SQL_PAS_NO_SELECT。 参数数组是否可以与其他类型的语句一起使用，这是特定于数据源的，特别是因为在这些语句中使用参数是特定于数据源的，并且不会遵循 ODBC SQL 语法。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 语句属性指向的数组可用于忽略参数行。 如果数组的元素设置为SQL_PARAM_IGNORE，则与该元素对应的参数集将从 SQLExecute 或**SQLExecDirect**调用中**SQLExecDirect**排除。 SQL_ATTR_PARAM_OPERATION_PTR属性指向的数组由应用程序分配和填充并由驱动程序读取。 如果提取的行用作输入参数，则行状态数组的值可以在参数操作数组中使用。  
  
## <a name="error-processing"></a>错误处理  
 如果在执行语句时发生错误，执行函数将返回一个错误，并将行号变量设置为包含错误的行数。 它是特定于数据源的，无论是执行除错误集之外的所有行，还是执行错误集之前（但不是之后）之前的所有行。 由于驱动程序处理参数集，因此驱动程序将SQL_ATTR_PARAMS_PROCESSED_PTR语句属性指定的缓冲区设置为当前正在处理的行数。 如果执行除错误集之外的所有集，则驱动程序将此缓冲区设置为处理所有行后SQL_ATTR_PARAMSET_SIZE。  
  
 如果设置了SQL_ATTR_PARAM_STATUS_PTR语句属性 **，SQLExecute**或**SQLExecDirect**将返回*参数状态数组，该数组*提供每组参数的状态。 参数状态数组由应用程序分配并由驱动程序填充。 其元素指示 SQL 语句是否已成功执行参数行，或者在处理参数集时是否发生错误。 如果发生错误，驱动程序将参数状态数组中的相应值设置为SQL_PARAM_ERROR并返回SQL_SUCCESS_WITH_INFO。 应用程序可以检查状态数组以确定已处理的行。 使用行号，应用程序通常可以更正错误并恢复处理。  
  
 参数状态数组的使用方式由调用**SQLGetInfo**返回SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS选项决定。 对于**INSERT、****更新**和**删除**语句，如果为SQL_PARAM_ARRAY_ROW_COUNTS返回SQL_PARC_BATCH，则参数状态数组将填充状态信息，但如果返回SQL_PARC_NO_BATCH则不填写。 对于**SELECT**语句，如果返回SQL_PAS_BATCHSQL_PARAM_ARRAY_SELECT，则填充参数状态数组，但如果返回SQL_PAS_NO_BATCH或SQL_PAS_NO_SELECT则不填写参数状态数组。  
  
## <a name="data-at-execution-parameters"></a>执行时的数据参数  
 如果长度/指示器数组中的任何值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC（*长度*） 宏的结果，则这些值的数据将通常随**SQLPutData**一起发送。 这一进程的以下方面有特别的评论，因为它们并不十分明显：  
  
-   当驱动程序返回SQL_NEED_DATA时，它必须将行号变量的地址设置为需要数据的行。 与单值情况一样，应用程序不能对驱动程序在单个参数集中请求参数值的顺序进行任何假设。 如果在执行执行数据时发生数据执行参数时发生错误，SQL_ATTR_PARAMS_PROCESSED_PTR语句属性指定的缓冲区将设置为发生错误的行数，SQL_ATTR_PARAM_STATUS_PTR语句属性指定的行状态数组中行的状态设置为SQL_PARAM_ERROR，对 SQLExecute、SQLExecDirect、SQLParamData 或**SQLPutData**的调用将返回SQL_ERROR。 **SQLExecute** **SQLExecDirect** **SQLParamData** 如果**SQLExecute、SQLExecDirect****SQLExecute**或**SQLParamData**返回SQL_STILL_EXECUTING，则此缓冲区的内容将未定义。  
  
-   由于驱动程序不解释**SQLBind参数**的*参数中*用于执行时数据参数的值，因此，如果应用程序提供指向数组的指针，**则 SQLParamData**不会提取此数组的元素并将其返回给应用程序。 相反，它返回应用程序提供的标量值。 这意味着**SQLParamData**返回的值不足以指定应用程序需要发送数据的参数;应用程序还需要考虑当前行号。  
  
     当参数数组的某些元素是执行时的数据参数时，应用程序必须通过*参数ValuePtr*中包含所有参数元素的数组的地址。 此数组对于不是执行时的数据参数进行正常解释。 对于执行时的数据参数 **，SQLParamData**向应用程序提供的值始终是数组的地址，该值通常可用于标识驱动程序此时请求的数据。
