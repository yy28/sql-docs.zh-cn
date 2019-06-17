---
title: 使用参数的数组 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ff4a76c38f04c7b9b12842ef800bc8a26a27ed9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312514"
---
# <a name="using-arrays-of-parameters"></a>使用参数的数组
若要使用的参数，应用程序调用数组**SQLSetStmtAttr**与*属性*参数则 SQL_ATTR_PARAMSET_SIZE 指定数量的参数集。 它将调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAMS_PROCESSED_PTR 指定驱动程序可以在其中返回集的处理，参数数量的变量的地址的自变量其中包括错误设置。 它将调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAM_STATUS_PTR 为指向数组中要返回其参数值的每一行的状态信息的自变量。 该驱动程序将这些地址存储在它保留为该语句的结构。  
  
> [!NOTE]  
>  在 ODBC 2。*x*， **SQLParamOptions**调用指定的参数的多个值。 在 ODBC 3。*x*，在调用**SQLParamOptions**已由调用**SQLSetStmtAttr**设置则 SQL_ATTR_PARAMSET_SIZE 和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 属性.  
  
 然后再执行该语句，该应用程序设置的每个绑定数组的每个元素的值。 驱动程序时执行该语句，使用它来检索参数值并将其发送到数据源; 而存储的信息如果可能，该驱动程序应将这些值发送数组形式。 虽然最好通过执行与数据源的单个调用数组中的所有参数的 SQL 语句实现使用的参数的数组，此功能目前不广泛用于 Dbms。 但是，驱动程序可以模拟它的执行 SQL 语句多次，每个都有一组参数。  
  
 应用程序使用的参数数组之前，必须确保应用程序使用的驱动程序支持。 完成这项工作的方法有两种：  
  
-   使用驱动程序，已知能够支持参数的数组。 应用程序可以硬编码的这些驱动程序的名称或用户可以指示你使用这些驱动程序。 自定义应用程序和垂直应用程序通常使用一组有限的驱动程序。  
  
-   在运行时检查支持的参数的数组。 如果可以将 SQL_ATTR_PARAMSET_SIZE 语句属性设置为一个值大于 1，驱动程序支持参数的数组。 通用应用程序和垂直应用程序通常检查的参数的数组的支持在运行时。  
  
 可通过调用确定的行计数和参数化执行中的结果集的可用性**SQLGetInfo** SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项。 有关**插入**，**更新**，并**删除**语句，SQL_PARAM_ARRAY_ROW_COUNTS 选项指示是否单独的行计数 （一个用于每个参数集）可用 (SQL_PARC_BATCH) 或是否行数将累加起来，为一个 (SQL_PARC_NO_BATCH)。 有关**选择**语句，SQL_PARAM_ARRAY_SELECTS 选项指示结果集是否可用于每组参数 (SQL_PAS_BATCH) 或只有一个结果集是否可用 (SQL_PAS_NO_BATCH)。 如果该驱动程序不允许结果集生成语句，以使用参数数组执行，SQL_PARAM_ARRAY_SELECTS 返回 SQL_PAS_NO_SELECT。 是否可以特别是因为这些语句中的参数使用数据源特定于和不遵循 ODBC SQL 语法与其他类型的语句，使用参数的数组，它是数据源特定于。  
  
 可以使用指向 SQL_ATTR_PARAM_OPERATION_PTR 语句属性数组忽略的参数的行。 如果数组的元素设置为 SQL_PARAM_IGNORE，从排除的与该元素对应的参数集**SQLExecute**或**SQLExecDirect**调用。 指向由 SQL_ATTR_PARAM_OPERATION_PTR 属性数组分配和填充应用程序和驱动程序读取。 如果提取的行用作输入参数，则行状态数组的值可以使用参数操作数组中。  
  
## <a name="error-processing"></a>错误处理  
 如果执行语句时出错，执行函数将返回错误，并将行号变量设置为包含错误的行数。 它是数据源特定于是否所有行只执行错误集或是否所有行 （但不是晚于） 之前执行的错误集。 由于它处理的参数集，该驱动程序设置到当前正在处理的行数将 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性指定的缓冲区。 如果所有设置只执行设置出错时，该驱动程序将在此缓冲区处理所有行后设置为 SQL_ATTR_PARAMSET_SIZE。  
  
 如果 SQL_ATTR_PARAM_STATUS_PTR 语句属性尚未设置， **SQLExecute**或**SQLExecDirect**返回*参数状态数组*其中提供的状态每组参数。 参数状态数组是由应用程序分配，并填充驱动程序。 其元素指示是否 SQL 语句成功执行的参数的行或处理的参数集时是否发生错误。 如果遇到错误，该驱动程序 SQL_PARAM_ERROR，参数状态数组中设置相应的值，并返回 SQL_SUCCESS_WITH_INFO。 应用程序可以检查状态数组以确定哪些行已处理。 使用行号，该应用程序可以通常更正错误并继续处理。  
  
 如何使用参数状态数组由调用返回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项**SQLGetInfo**。 有关**插入**，**更新**，并**删除**语句，参数状态数组填充的状态信息，如果为 SQL_PARAM_ARRAY_ 返回 SQL_PARC_BATCHROW_COUNTS，但不返回 SQL_PARC_NO_BATCH 的情况。 有关**选择**语句，参数状态数组填充 SQL_PAS_BATCH 返回为 SQL_PARAM_ARRAY_SELECT，但如果返回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT。  
  
## <a name="data-at-execution-parameters"></a>执行时数据参数  
 如果任一长度/指示器数组中的值为 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 结果 (*长度*) 的宏，这些值不会发送数据**SQLPutData**用通常的方式。 此过程的以下方面请特殊注释，因为它们不是十分明显：  
  
-   当驱动程序将返回 SQL_NEED_DATA 时，它必须设置为它需要数据的行的行数字变量的地址。 如下所示单值的情况下，应用程序不能进行任何假设驱动程序将请求参数的单个集中的参数值的顺序。 如果在执行时数据参数的执行过程中发生错误，将 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性指定的缓冲区设置为在其发生错误，在指定的行状态数组中的行状态的行数SQL_ATTR_PARAM_STATUS_PTR 语句属性设置为 SQL_PARAM_ERROR，并调用**SQLExecute**， **SQLExecDirect**， **SQLParamData**，或**SQLPutData**返回 SQL_ERROR。 此缓冲区的内容是不确定，如果**SQLExecute**， **SQLExecDirect**，或**SQLParamData**返回 SQL_STILL_EXECUTING。  
  
-   因为该驱动程序不会解释中的值*ParameterValuePtr*的参数**SQLBindParameter**对于执行时数据参数，如果应用程序提供一个指针数组，指向**SQLParamData**不提取并返回到应用程序的此数组的元素。 相反，它将返回标量值在应用程序必须提供。 这意味着返回的值**SQLParamData**不是足够，若要为其指定参数在应用程序需要将数据发送; 应用程序还需要考虑的当前行号。  
  
     当只某些参数的数组的元素执行时数据参数，该应用程序必须通过数组中的地址*ParameterValuePtr* ，其中包含的所有参数的元素。 此数组被解释通常不是执行时数据参数的参数。 对于执行时数据参数，值的**SQLParamData**提供对应用程序，通常可以用于标识该驱动程序正在请求这种情况下的数据时，始终是数组的地址。
