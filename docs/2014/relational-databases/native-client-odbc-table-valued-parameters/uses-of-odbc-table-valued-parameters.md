---
title: 使用 ODBC 表值参数 |Microsoft 文档
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
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8dd9c815d1d7636218bd4ff33505388597800876
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027675"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>ODBC 表值参数的用法
  本主题介绍将表值参数用于 ODBC 时的主要用户情况：  
  
-   完全绑定多行缓冲区情况下的表值参数（在所有值都位于内存中时将数据作为 TVP 发送）  
  
-   行流式处理情况下的表值参数（使用执行时数据将数据作为 TVP 发送）  
  
-   从系统目录中检索表值参数元数据  
  
-   检索准备的语句的表值参数元数据  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>完全绑定多行缓冲区情况下的表值参数（在所有值都位于内存中时将数据作为 TVP 发送）  
 用于完全绑定多行缓冲区时，所有参数值都位于内存中。 这是 OLTP 事务（举例来说）的典型情况，在这种情况下，可以将表值参数封装到单个存储过程中。 如果不使用表值参数，这通常需要动态生成复杂的多语句批处理，或者执行多个针对服务器的调用。  
  
 通过使用绑定的表值参数本身[SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328)以及其他参数。 所有参数都具有已都绑定后，应用程序的每个表值参数设置的参数焦点属性： SQL_SOPT_SS_PARAM_FOCUS，并为表值参数列调用 SQLBindParameter。  
  
 表值参数的服务器类型是特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新增类型 SQL_SS_TABLE。 SQL_SS_TABLE 的绑定 C 类型必须始终为 SQL_C_DEFAULT。 不为表值参数绑定参数传输任何数据；该参数用于传递表元数据，并且控制如何传递表值参数各构成列中的数据。  
  
 表值参数的长度设置为要发送到服务器的行数。 *Columnsize 类型*SQLBindParameter 参数表值参数指定的最大可以发送的行数; 这是列缓冲区的数组大小。 *ParameterValuePtr*是参数缓冲区，SQLBindParameter 中表值参数。 *ParameterValuePtr*及其关联*BufferLength*用来在传递时所需的表值参数的类型名称。 类型名称不是存储过程调用必需的，但却是 SQL 语句所必需的。  
  
 当在 SQLBindParameter 调用指定的表值参数类型名称时，它必须始终指定为 Unicode 值，即使在应用程序生成为 ANSI 应用程序。 当使用 SQLSetDescField 指定表值参数类型名称时，可以使用文本符合生成应用程序的方式。 ODBC 驱动程序管理器将执行任何所需的 Unicode 转换。  
  
 表值参数和表值参数列的元数据可以通过使用 SQLGetDescRec、 SQLSetDescRec、 SQLGetDescField 和 SQLSetDescField 单独和显式操作。 但是，重载 SQLBindParameter 通常更为方便，并且不需要在大多数情况下显式描述符访问。 此方法具有与其他数据类型，SQLBindParameter 的定义一致的只不过表值参数的受影响的描述符字段略有不同。  
  
 有时，应用程序将表值参数用于动态 SQL，此时必须提供该表值参数的类型名称。 如果是这种情况和连接的当前默认架构中未定义表值参数，则 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 必须通过使用 SQLSetDescField 设置。 由于表类型定义和表值参数必须位于同一数据库中，在应用程序使用表值参数时不能设置 SQL_CA_SS_TYPE_CATALOG_NAME。 否则，SQLSetDescField 将报告错误。  
  
 对于此方案的示例代码是在过程中`demo_fixed_TVP_binding`中[使用表值参数&#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>行流式处理情况下的表值参数（使用执行时数据将数据作为 TVP 发送）  
 在此情况下，应用程序在驱动程序请求行时向其提供行，并且这些行流向服务器。 这样就无需将所有行缓存在内存中。 这是大容量插入/更新时的典型情况。 表值参数提供了介于参数数组和大容量复制之间的某个性能点。 也就是说：表值参数可以像参数数组那样易于编程，但它们在服务器端提供更高的灵活性。  
  
 表值参数及其列按上一节“完全绑定多行缓冲区情况下的表值参数”所述进行绑定，但是表值参数本身的长度指示器设置为 SQL_DATA_AT_EXEC。 该驱动程序响应 SQLExecute 或 SQLExecuteDirect 按照通常的方式执行中的数据参数-即，通过返回 SQL_NEED_DATA。 SQLParamData 驱动程序准备好接受表值参数的数据时，返回的值*ParameterValuePtr* SQLBindParameter 中。  
  
 应用程序使用表值参数的 SQLPutData 指明表值参数构成列数据的可用性。 为表值参数，调用 SQLPutData 时*DataPtr*必须始终为 null 和*StrLen_or_Ind*必须是 0 或数字小于或等于指定的数组大小表值参数缓冲区 ( *columnsize 类型*SQLBindParameter 参数)。 0 表示表值参数没有更多的行，驱动程序将继续处理下一个实际过程参数。 当*StrLen_or_Ind*是不为 0，驱动程序将表值参数构成列相同的方式按照处理非 – 表值参数绑定参数： 每个表值参数列可以指定其实际的数据长度、 SQL_NULL_DATA，或它可以指定在执行通过其长度/指示器缓冲区的数据。 在字符或二进制值是要在片段中传递时，可以通过传递值的表值参数列将像往常一样重复 SQLPutData 对的调用。  
  
 处理完所有表值参数列后，驱动程序将返回到表值参数以处理更多的表值参数数据行。 因此，对于执行时数据表值参数，驱动程序不遵循通常的顺序扫描绑定参数的方式。 将轮询绑定的表值参数，直到使用调用 SQLPutData *StrLen_Or_IndPtr*等于 0，在这段时间的驱动程序跳过表值参数列和将移到下一步的实际存储的过程参数。  当 SQLPutData 通过指示器值大于或等于 1 时，该驱动程序处理表值参数列和行按顺序直到其所有绑定的行和列的值。 然后驱动程序返回到表值参数。 从 SQLParamData 接收表值参数的标记，表值参数调用 SQLPutData (hstmt，NULL，n)，应用程序必须设置表值参数构成的列数据和指标的缓冲区内容下一步的行或行要传递到服务器。  
  
 对于此方案的示例代码位于例程`demo_variable_TVP_binding`中[使用表值参数&#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>从系统目录中检索表值参数元数据  
 当应用程序需要具有表值参数参数的过程 SQLProcedureColumns 时，DATA_TYPE 将返回如 SQL_SS_TABLE 和类型 _ 名称是表值参数的表类型的名称。 两个其他列添加到 SQLProcedureColumns 所返回的结果集： SS_TYPE_CATALOG_NAME 返回其中定义表值参数的表类型，并 SS_TYPE_SCHEMA_NAME 返回的架构名称的目录的名称，其中定义表值参数的表类型。 符合 ODBC 规范，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 出现在之前的早期版本中已添加的所有驱动程序特定列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和之后由 ODBC 本身规定的所有列。  
  
 不仅将为表值参数填充这些新列，还将为 CLR 用户定义类型参数填充这些新列。 仍将填充 UDT 参数的现有架构和目录列，但是为数据类型提供所需的常见架构和目录列将简化未来的应用程序开发。 （请注意，XML 架构集合稍有不同，未包括在此更改中。）  
  
 应用程序使用 SQLTables 以确定它持久表、 系统表和视图执行的相同方式的表类型的名称。 引入了一个新的表类型 TABLE TYPE，该类型支持应用程序标识与表值参数关联的表类型。 表类型和常规表使用不同的命名空间。 这意味着可以对表类型和实际表使用相同的名称。 为处理同名情况，引入了一个新的语句属性 SQL_SOPT_SS_NAME_SCOPE。 此属性指定是否 SQLTables 和采用作为参数的表名称的其他目录函数应解释为实际的表的名称的表名称或表类型的名称。  
  
 应用程序使用 SQLColumns 对于持久表，但必须首先设置 SQL_SOPT_SS_NAME_SCOPE 以指示它正在使用表类型，而不是实际的表相同的方式确定的表类型的列。 此外可以与表类型，使用 SQL_SOPT_SS_NAME_SCOPE 再次使用 SQLPrimaryKeys。  
  
 对于此方案的示例代码位于例程`demo_metadata_from_catalog_APIs`中[使用表值参数&#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>检索准备的语句的表值参数元数据  
 在此方案中，应用程序使用 SQLNumParameters 和 SQLDescribeParam 来检索元数据的表值参数。  
  
 IPD 字段 SQL_CA_SS_TYPE_NAME 用于检索表值参数的类型名称。 IPD 字段 SQL_CA_SS_TYPE_SCHEMA_NAME 和 SQL_CA_SS_TYPE_CATALOG_NAME 分别用于检索表值参数的目录和架构。  
  
 表类型定义和表值参数必须位于同一数据库中。 如果应用程序设置 SQL_CA_SS_TYPE_CATALOG_NAME 使用表值参数时，SQLSetDescField 将报告错误。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 还可以用于检索与 CLR 用户定义类型参数关联的目录和架构。 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 是 CLR UDT 类型的现有类型特定目录架构属性的替代属性。  
  
 应用程序使用 SQLColumns 检索列元数据，表值参数在此方案中，过，因为 SQLDescribeParam 并不返回表值参数列的列的元数据。  
  
 对此用例的示例代码位于例程`demo_metadata_from_prepared_statement`中[使用表值参数&#40;ODBC&#41;](../native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  