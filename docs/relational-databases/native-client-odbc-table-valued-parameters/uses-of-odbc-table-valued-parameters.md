---
title: ODBC 表值参数的用法 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 25c8da6552446f7c34cd6deb050b2074da67443c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673106"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>ODBC 表值参数的用法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题介绍将表值参数用于 ODBC 时的主要用户情况：  
  
-   完全绑定多行缓冲区情况下的表值参数（在所有值都位于内存中时将数据作为 TVP 发送）  
  
-   行流式处理情况下的表值参数（使用执行时数据将数据作为 TVP 发送）  
  
-   从系统目录中检索表值参数元数据  
  
-   检索准备的语句的表值参数元数据  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>完全绑定多行缓冲区情况下的表值参数（在所有值都位于内存中时将数据作为 TVP 发送）  
 用于完全绑定多行缓冲区时，所有参数值都位于内存中。 这是 OLTP 事务（举例来说）的典型情况，在这种情况下，可以将表值参数封装到单个存储过程中。 如果不使用表值参数，这通常需要动态生成复杂的多语句批处理，或者执行多个针对服务器的调用。  
  
 通过使用绑定表值参数本身[SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)以及其他参数。 绑定所有参数后，应用程序上每个表值参数设置参数焦点属性 SQL_SOPT_SS_PARAM_FOCUS，并调用 SQLBindParameter 为表值参数的列。  
  
 表值参数的服务器类型是特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新增类型 SQL_SS_TABLE。 SQL_SS_TABLE 的绑定 C 类型必须始终为 SQL_C_DEFAULT。 不为表值参数绑定参数传输任何数据；该参数用于传递表元数据，并且控制如何传递表值参数各构成列中的数据。  
  
 表值参数的长度设置为要发送到服务器的行数。 *ColumnSize* SQLBindParameter 的表值参数的参数指定的最大可以发送的行数; 这是列缓冲区的数组大小。 *ParameterValuePtr*是在 SQLBindParameter 中为表值参数的参数缓冲区。 *ParameterValuePtr*及其关联*BufferLength*用于传递表值参数时所需的类型名称。 类型名称不是存储过程调用必需的，但却是 SQL 语句所必需的。  
  
 当在 SQLBindParameter 调用指定表值参数类型名称时，它必须始终指定为 Unicode 值，即使在作为 ANSI 应用程序生成的应用程序。 当通过使用 SQLSetDescField 指定表值参数类型名称时，可以使用生成应用程序的方式一致的文字。 ODBC 驱动程序管理器将执行任何所需的 Unicode 转换。  
  
 表值参数和表值参数列元数据可以通过使用 SQLGetDescRec、 SQLSetDescRec、 SQLGetDescField 和 SQLSetDescField 分别且显式操作。 但是，重载 SQLBindParameter 通常更为方便，并且不需要在大多数情况下显式描述符访问权限。 不过，对于表值参数的受影响的描述符字段是略有不同，这种方法在与其他数据类型，SQLBindParameter 的定义一致。  
  
 有时，应用程序将表值参数用于动态 SQL，此时必须提供该表值参数的类型名称。 如果出现这种情况，并且该连接的当前默认架构中未定义表值参数，必须通过使用 SQLSetDescField 设置 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME。 由于表类型定义和表值参数必须位于同一数据库中，在应用程序使用表值参数时不能设置 SQL_CA_SS_TYPE_CATALOG_NAME。 否则，SQLSetDescField 将报告错误。  
  
 对于此方案的示例代码位于过程`demo_fixed_TVP_binding`中[使用表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>行流式处理情况下的表值参数（使用执行时数据将数据作为 TVP 发送）  
 在此情况下，应用程序在驱动程序请求行时向其提供行，并且这些行流向服务器。 这样就无需将所有行缓存在内存中。 这是大容量插入/更新时的典型情况。 表值参数提供了介于参数数组和大容量复制之间的某个性能点。 也就是说：表值参数可以像参数数组那样易于编程，但它们在服务器端提供更高的灵活性。  
  
 表值参数及其列按上一节“完全绑定多行缓冲区情况下的表值参数”所述进行绑定，但是表值参数本身的长度指示器设置为 SQL_DATA_AT_EXEC。 该驱动程序响应 SQLExecute 或 SQLExecuteDirect 按常规方式执行时数据参数的-也就是说，通过返回 SQL_NEED_DATA。 SQLParamData 时驱动程序已准备好接受表值参数的数据，返回的值*ParameterValuePtr*在 SQLBindParameter 中。  
  
 应用程序使用 SQLPutData 为表值参数以指示表值参数构成列的数据的可用性。 对于表值参数，调用时 SQLPutData *DataPtr*必须始终为 null 和*StrLen_or_Ind*必须是 0 或非数字小于或等于数组大小为指定表值参数缓冲区 ( *ColumnSize* SQLBindParameter 参数)。 0 表示表值参数没有更多的行，驱动程序将继续处理下一个实际过程参数。 当*StrLen_or_Ind*是不为 0，驱动程序将处理表值参数构成列相同的方式为非表值参数绑定参数： 每个表值参数列可以指定其实际数据长度、 SQL_NULL_DATA，或它可以指定通过其长度/指示器缓冲区执行时数据。 表值参数列可以通过传递值重复调用 SQLPutData 像往常一样的字符或二进制值是要分块传递时。  
  
 处理完所有表值参数列后，驱动程序将返回到表值参数以处理更多的表值参数数据行。 因此，对于执行时数据表值参数，驱动程序不遵循通常的顺序扫描绑定参数的方式。 绑定的表值参数进行轮询，直到使用调用 SQLPutData *StrLen_Or_IndPtr*等于 0，届时，驱动程序将跳过表值参数列并将移动到下一个实际的存储的过程参数。  在 SQLPutData 通过指示器值大于或等于 1，驱动程序表值参数列和行按顺序处理直到它具有的所有绑定的行和列的值。 然后驱动程序返回到表值参数。 从 SQLParamData 接收表值参数的标记，对于表值参数调用 SQLPutData (hstmt，NULL，n)，该应用程序必须设置表值参数构成列数据和指示器缓冲区内容下一步的行或行要传递到服务器。  
  
 此方案的示例代码位于在例程`demo_variable_TVP_binding`中[使用表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>从系统目录中检索表值参数元数据  
 当应用程序具有表值参数的参数的过程调用 SQLProcedureColumns 时，DATA_TYPE 将返回为 SQL_SS_TABLE，并且 TYPE_NAME 是表值参数的表类型的名称。 两个其他列添加到 SQLProcedureColumns 返回的结果集： SS_TYPE_CATALOG_NAME 返回其中定义表值参数的表类型，并且 SS_TYPE_SCHEMA_NAME 返回的架构的名称的目录的名称，定义表类型的表值参数的位置。 为了符合 ODBC 规范，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 出现在之前的早期版本中已添加的所有驱动程序特定列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和通过 ODBC 自身委托的所有列之后。  
  
 不仅将为表值参数填充这些新列，还将为 CLR 用户定义类型参数填充这些新列。 仍将填充 UDT 参数的现有架构和目录列，但是为数据类型提供所需的常见架构和目录列将简化未来的应用程序开发。 （请注意，XML 架构集合稍有不同，未包括在此更改中。）  
  
 应用程序使用 SQLTables 来确定的是相同的持久性表、 系统表和视图的表类型的名称。 引入了一个新的表类型 TABLE TYPE，该类型支持应用程序标识与表值参数关联的表类型。 表类型和常规表使用不同的命名空间。 这意味着可以对表类型和实际表使用相同的名称。 为处理同名情况，引入了一个新的语句属性 SQL_SOPT_SS_NAME_SCOPE。 此属性指定是否 SQLTables 和表名称作为参数的其他目录函数应解释为实际表名称的表名或表类型的名称。  
  
 应用程序使用 SQLColumns 以它为持久表，但必须首先设置 SQL_SOPT_SS_NAME_SCOPE 以指示它正在与表类型而不是实际表相同的方式确定表类型的列。 SQLPrimaryKeys 还用于表类型，使用 SQL_SOPT_SS_NAME_SCOPE。  
  
 此方案的示例代码位于在例程`demo_metadata_from_catalog_APIs`中[使用表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>检索准备的语句的表值参数元数据  
 在此方案中，应用程序使用 SQLNumParameters 和 SQLDescribeParam 来检索表值参数的元数据。  
  
 IPD 字段 SQL_CA_SS_TYPE_NAME 用于检索表值参数的类型名称。 IPD 字段 SQL_CA_SS_TYPE_SCHEMA_NAME 和 SQL_CA_SS_TYPE_CATALOG_NAME 分别用于检索表值参数的目录和架构。  
  
 表类型定义和表值参数必须位于同一数据库中。 如果使用表值参数时，应用程序设置了 SQL_CA_SS_TYPE_CATALOG_NAME，SQLSetDescField 将报告错误。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 还可以用于检索与 CLR 用户定义类型参数关联的目录和架构。 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 是 CLR UDT 类型的现有类型特定目录架构属性的替代属性。  
  
 应用程序使用 SQLColumns 检索列元数据的表值参数在此方案中，也因为 SQLDescribeParam 不返回表值参数列的列的元数据。  
  
 此用例的示例代码位于在例程`demo_metadata_from_prepared_statement`中[使用表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
