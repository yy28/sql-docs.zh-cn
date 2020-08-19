---
description: 使用参数的数组
title: 使用参数数组 |Microsoft Docs
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
ms.openlocfilehash: 1a592131165e7dc2370ab1d22a3d9eba5f9609dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424409"
---
# <a name="using-arrays-of-parameters"></a>使用参数的数组
若要使用参数数组，应用程序将调用 **SQLSetStmtAttr** ，并使用 SQL_ATTR_PARAMSET_SIZE 的 *属性* 参数来指定参数集的数目。 它调用具有 SQL_ATTR_PARAMS_PROCESSED_PTR 的*属性*参数的**SQLSetStmtAttr** ，以指定驱动程序可在其中返回处理的参数集（包括错误集）数目的变量的地址。 它使用 SQL_ATTR_PARAM_STATUS_PTR 的*属性*参数调用**SQLSetStmtAttr** ，以指向一个数组，该数组将返回每行参数值的状态信息。 驱动程序将这些地址存储在它为语句维护的结构中。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，调用 **SQLParamOptions** 为参数指定多个值。 ODBC 3 中的。*x*，对 **SQLParamOptions** 的调用已替换为对 **SQLSetStmtAttr** 的调用，以设置 SQL_ATTR_PARAMSET_SIZE 和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 特性。  
  
 在执行语句之前，应用程序将设置每个绑定数组的每个元素的值。 执行语句时，驱动程序将使用存储的信息来检索参数值并将其发送到数据源;如果可能，驱动程序应以数组形式发送这些值。 尽管通过使用数组中的所有参数执行 SQL 语句来实现使用参数数组的最佳方法，只需要对数据源进行一次调用，此功能目前并不广泛适用于 Dbms。 但是，驱动程序可以通过多次执行 SQL 语句来模拟该语句，每个语句都有一组参数。  
  
 在应用程序使用参数数组之前，必须确保应用程序使用的驱动程序支持它们。 有两种方法可以实现此目的：  
  
-   仅使用已知的驱动程序支持参数数组。 应用程序可以对这些驱动程序的名称进行硬编码，也可以指示该用户仅使用这些驱动程序。 自定义应用程序和垂直应用程序通常使用有限的驱动程序集。  
  
-   在运行时检查是否支持参数数组。 如果可以将 SQL_ATTR_PARAMSET_SIZE 语句特性设置为大于1的值，则驱动程序支持参数的数组。 一般的应用程序和垂直应用程序通常会在运行时检查是否支持参数数组。  
  
 可以通过使用 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项调用 **SQLGetInfo** 来确定参数化执行中的行计数和结果集的可用性。 对于 **INSERT**、 **UPDATE**和 **DELETE** 语句，SQL_PARAM_ARRAY_ROW_COUNTS 选项指示单个行计数 (为每个参数集) 可用 (SQL_PARC_BATCH) 还是汇总到 (SQL_PARC_NO_BATCH) 中的行计数。 对于 **SELECT** 语句，SQL_PARAM_ARRAY_SELECTS 选项指示结果集是否可用于 () SQL_PAS_BATCH 的每个参数集，或是否仅有一个结果集可用 (SQL_PAS_NO_BATCH) 。 如果驱动程序不允许使用参数数组来执行结果集生成语句，SQL_PARAM_ARRAY_SELECTS 将返回 SQL_PAS_NO_SELECT。 无论参数数组是否可与其他类型的语句一起使用，它都是特定于数据源的，尤其是因为在这些语句中使用参数将是特定于数据源的，不遵循 ODBC SQL 语法。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 语句特性指向的数组可用于忽略参数行。 如果将数组的元素设置为 SQL_PARAM_IGNORE，则将从 **SQLExecute** 或 **SQLExecDirect** 调用中排除与该元素对应的参数集。 SQL_ATTR_PARAM_OPERATION_PTR 特性指向的数组由应用程序分配并由驱动程序读取。 如果提取的行用作输入参数，则可以在参数操作数组中使用行状态数组的值。  
  
## <a name="error-processing"></a>错误处理  
 如果在执行语句时出现错误，则执行函数将返回错误，并将行号变量设置为包含错误的行的行号。 它是特定于数据源的，无论是执行除错误之外的所有行，还是在 (之前的所有行，而不是在) 错误集之后。 由于它处理参数集，因此驱动程序将 SQL_ATTR_PARAMS_PROCESSED_PTR 语句特性指定的缓冲区设置为当前正在处理的行号。 如果执行了除错误之外的所有集，则驱动程序将此缓冲区设置为在处理所有行后 SQL_ATTR_PARAMSET_SIZE。  
  
 如果已设置 SQL_ATTR_PARAM_STATUS_PTR 语句特性，则 **SQLExecute** 或 **SQLExecDirect** 将返回 *参数 STATUS 数组，该数组* 提供每组参数的状态。 参数状态数组由应用程序分配并由驱动程序填充。 其元素指示是否已成功为参数行执行了 SQL 语句，或者是否在处理参数集时出现错误。 如果发生错误，则驱动程序将参数状态数组中的相应值设置为 SQL_PARAM_ERROR 并返回 SQL_SUCCESS_WITH_INFO。 应用程序可以检查状态数组以确定已处理的行。 使用行号，应用程序通常可以更正错误并继续处理。  
  
 参数状态数组的使用方式由对 **SQLGetInfo**的调用返回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项决定。 对于 **INSERT**、 **UPDATE**和 **DELETE** 语句，如果为 SQL_PARAM_ARRAY_ROW_COUNTS 返回 SQL_PARC_BATCH，则将填充参数状态数组，如果返回 SQL_PARC_NO_BATCH，则不填充。 对于 **SELECT** 语句，如果为 SQL_PARAM_ARRAY_SELECT 返回 SQL_PAS_BATCH，则会填写参数状态数组，但不会返回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT。  
  
## <a name="data-at-execution-parameters"></a>执行时数据参数  
 如果长度/指示器数组中的任何值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC (*长度*) 宏的结果，则这些值的数据将以常规方式随 **SQLPutData** 一起发送。 此过程的以下方面涉及到特殊的注释，因为这种情况并不明显：  
  
-   当驱动程序返回 SQL_NEED_DATA 时，它必须将行号变量的地址设置为它需要数据的行。 与单值的情况一样，应用程序无法对驱动程序将在一个参数集中请求参数值的顺序作出任何假设。 如果执行执行时数据参数出现错误，则由 SQL_ATTR_PARAMS_PROCESSED_PTR 语句特性指定的缓冲区设置为发生错误的行的行号，由 SQL_ATTR_PARAM_STATUS_PTR 语句特性指定的行状态数组中的行的状态设置为 SQL_PARAM_ERROR，并且调用 **SQLExecute**、 **SQLExecDirect**、 **SQLParamData**或 **SQLPutData** 将返回 SQL_ERROR。 如果 **SQLExecute**、 **SQLExecDirect**或 **SQLParamData** 返回 SQL_STILL_EXECUTING，则不定义此缓冲区的内容。  
  
-   由于驱动程序不解释**SQLBindParameter**的*ParameterValuePtr*参数中的值用于执行时数据参数，因此，如果应用程序提供指向数组的指针，则**SQLParamData**不会提取此数组的元素并将其返回给应用程序。 相反，它将返回应用程序提供的标量值。 这意味着 **SQLParamData** 返回的值不足以指定应用程序需要向其发送数据的参数;应用程序还需要考虑当前行号。  
  
     当仅参数数组的某些元素是执行时数据参数时，应用程序必须传递 *ParameterValuePtr* 中包含所有参数的元素的数组的地址。 对于不是执行时数据参数的参数，此数组通常被解释为。 对于执行时数据参数， **SQLParamData** 提供给应用程序的值（通常可以用来标识此情况下驱动程序所请求的数据）始终为数组的地址。
