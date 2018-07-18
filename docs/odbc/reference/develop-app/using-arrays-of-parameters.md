---
title: 使用的参数数组 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ace7c9efebf23c25099ca1864debaae3296bc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32919292"
---
# <a name="using-arrays-of-parameters"></a>使用参数的数组
若要使用的参数，则应用程序调用数组**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAMSET_SIZE 可指定数目的参数集的自变量。 它调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAMS_PROCESSED_PTR 指定驱动程序可以在其中返回集的处理，参数个数的变量的地址的自变量包括错误设置。 它调用**SQLSetStmtAttr**与*属性*SQL_ATTR_PARAM_STATUS_PTR 为指向数组中要返回其参数值的每一行的状态信息的自变量。 该驱动程序将这些地址存储在它还为该语句保留的结构。  
  
> [!NOTE]  
>  在 ODBC 2。*x*， **SQLParamOptions**调用来指定多个参数的值。 在 ODBC 3。*x*，调用**SQLParamOptions**已通过调用替换为**SQLSetStmtAttr**设置 SQL_ATTR_PARAMSET_SIZE 和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 特性.  
  
 在执行语句前, 应用程序设置的每个绑定的数组的每个元素的值。 驱动程序时执行该语句，使用它存储检索参数值并将它们发送到数据源; 的信息如果可能，该驱动程序应将这些值发送为数组。 尽管使用的参数数组最实现通过执行到数据源一次调用数组中的所有参数的 SQL 语句，此功能不是广泛用于 Dbms 今天。 但是，驱动程序可以对其进行模拟通过执行 SQL 语句多次，每个都有一组参数。  
  
 应用程序使用的参数数组之前，它必须确保应用程序使用的驱动程序支持。 完成这项工作的方法有两种：  
  
-   使用驱动程序，已知支持的参数数组。 应用程序可以硬编码的这些驱动程序的名称，或指示用户可以使用仅这些驱动程序。 自定义应用程序和垂直的应用程序通常使用一组有限的驱动程序。  
  
-   在运行时检查支持的参数数组。 如果可能将 SQL_ATTR_PARAMSET_SIZE 语句特性设置为一个值大于 1，驱动程序支持的参数的数组。 通用应用程序和垂直的应用程序通常检查支持的参数数组在运行时。  
  
 可以调用来确定的行计数和参数化的执行中的结果集的可用性**SQLGetInfo**使用 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项。 有关**插入**，**更新**，和**删除**语句，SQL_PARAM_ARRAY_ROW_COUNTS 选项表明单个行计数 （一个用于每个参数集） 是否为可用 (SQL_PARC_BATCH) 或是否行数将累加起来，为一个 (SQL_PARC_NO_BATCH)。 有关**选择**语句，SQL_PARAM_ARRAY_SELECTS 选项指示结果集是否可用的参数 (SQL_PAS_BATCH) 每组或者只有一个结果集是否可用 (SQL_PAS_NO_BATCH)。 如果该驱动程序不允许结果生成集 – 语句得以执行具有参数的数组，SQL_PARAM_ARRAY_SELECTS 返回 SQL_PAS_NO_SELECT。 它是数据源 – 特定是否能够与其他类型的语句中使用的参数数组，尤其是因为这些语句中的参数使用将数据源 – 特定并且将不遵循 ODBC SQL 语法。  
  
 指向由 SQL_ATTR_PARAM_OPERATION_PTR 语句属性数组可用来忽略参数的行。 如果数组的元素设置为 SQL_PARAM_IGNORE，从排除的对应于该元素的参数集**SQLExecute**或**SQLExecDirect**调用。 由 SQL_ATTR_PARAM_OPERATION_PTR 属性指向数组的本质分配填写应用程序和驱动程序读取。 如果读取的行被用作输入参数，则行状态数组的值可以使用参数操作数组中。  
  
## <a name="error-processing"></a>错误处理  
 如果执行的语句时发生错误，请执行函数将返回一个错误，并将行号变量设置为包含错误的行数。 它是数据源 – 特定是否只执行错误组，或是否所有行之前 （但不是晚于） 执行错误组的所有行。 由于它处理的参数集，该驱动程序将设置为当前正在处理的行数的 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性指定的缓冲区。 如果所有设置只执行错误组，该驱动程序将在此缓冲区处理所有行后设置为 SQL_ATTR_PARAMSET_SIZE。  
  
 如果已经设置了 SQL_ATTR_PARAM_STATUS_PTR 语句特性， **SQLExecute**或**SQLExecDirect**返回*参数状态数组*其提供的状态每个组的参数。 参数状态数组是由应用程序分配的和填写由驱动程序。 其元素指示是否 SQL 语句已成功执行的行的参数或是否处理的参数集时出现错误。 如果出现了错误，该驱动程序到 SQL_PARAM_ERROR 参数状态数组中设置相应的值，并返回 SQL_SUCCESS_WITH_INFO。 应用程序可以检查要确定哪些行已处理的状态数组。 使用行号，应用程序可以通常更正该错误并恢复处理。  
  
 如何使用参数状态数组由调用返回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项**SQLGetInfo**。 有关**插入**，**更新**，和**删除**如果 SQL_PARC_BATCH 返回 SQL_PARAM_ARRAY_，使用状态信息填充的语句，参数状态数组ROW_COUNTS，但如果返回 SQL_PARC_NO_BATCH。 有关**选择**语句，参数状态数组以填充 SQL_PAS_BATCH 返回为 SQL_PARAM_ARRAY_SELECT，但如果返回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT。  
  
## <a name="data-at-execution-parameters"></a>执行中的数据参数  
 如果任一长度/指示器数组中的值是 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 的结果 (*长度*) 宏，不会发送这些值的数据**SQLPutData**按照通常的方式。 此过程的以下方面须自行承担特殊的注释，因为它们不十分明显：  
  
-   在驱动程序返回 SQL_NEED_DATA 时，它必须设置为它需要数据的行的行号变量的地址。 如下所示单值的情况下，应用程序不能进行任何假设该驱动程序将在其中请求一组参数中的参数值的顺序。 如果数据在执行参数执行过程中发生错误，SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性指定的缓冲区设置为在其出错，请通过指定的行状态数组中的行的状态的行数SQL_ATTR_PARAM_STATUS_PTR 语句特性设置为 SQL_PARAM_ERROR 和对**SQLExecute**， **SQLExecDirect**， **SQLParamData**，或**SQLPutData**返回 SQL_ERROR。 如果将此缓冲区的内容是不确定**SQLExecute**， **SQLExecDirect**，或**SQLParamData**返回 SQL_STILL_EXECUTING。  
  
-   因为该驱动程序不解释中的值*ParameterValuePtr*参数**SQLBindParameter**对于数据在执行参数，如果应用程序提供了指向数组中， **SQLParamData**不提取，返回到应用程序的此数组的元素。 相反，它将返回的标量值应用程序必须提供。 这意味着返回的值**SQLParamData**不是足够，若要为其指定参数应用程序需要发送数据; 应用程序还需要考虑的当前行号。  
  
     当只某些参数的数组的元素执行中的数据参数，应用程序必须传递一个数组中的地址*ParameterValuePtr*包含元素的所有参数。 此数组被解释通常不是执行中的数据参数的参数。 对于数据在执行参数，值的**SQLParamData**提供对应用程序，通常可以使用以确定该驱动程序正在请求在此情况下的数据，这始终是数组的地址。
