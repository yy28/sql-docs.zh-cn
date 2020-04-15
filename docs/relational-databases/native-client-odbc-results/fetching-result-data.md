---
title: 提取结果数据 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304595"
---
# <a name="fetching-result-data"></a>提取结果数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 应用程序具有三个用于提取结果数据的选项。  
  
 第一个选项基于[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)。 在获取结果集之前，应用程序使用**SQLBindCol**将结果集中的每个列绑定到程序变量。 绑定列后，驱动程序将当前行的数据传输到每次应用程序调用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)时绑定到结果集列的变量中。 如果结果集列和程序变量具有不同的数据类型，则驱动程序将处理数据转换。 如果应用程序SQL_ATTR_ROW_ARRAY_SIZE设置为大于 1，则可以将结果列绑定到变量数组，这些变量列将在每次调用**SQLFetchScroll**时填充这些数组。  
  
 第二个选项基于[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 应用程序不使用**SQLBindCol**将结果集列绑定到程序变量。 每次调用**SQLFetch**后，应用程序都会在结果集中的每一列调用**SQLGetData**一次。 **SQLGetData**指示驱动程序将数据从特定结果集列传输到特定程序变量，并指定列和变量的数据类型。 如果结果集列和程序变量具有不同的数据类型，则上述操作将允许驱动程序转换数据。 **文本****、ntext**和**图像**列通常太大，无法放入程序变量中，但仍可以使用**SQLGetData**检索。 如果结果列**中的文本****、ntext**或**图像**数据大于程序变量 **，SQLGetData**将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004（字符串数据，右截断）。 对**SQLGetData**的连续调用返回**文本**或**图像**数据的连续块。 到达数据结束时 **，SQLGetData**返回SQL_SUCCESS。 如果 SQL_ATTR_ROW_ARRAY_SIZE 大于 1，则每个提取都将返回一组行或行集。 在使用**SQLGetData**之前，必须首先使用**SQLSetPos**将行集中的特定行指定为当前行。  
  
 第三个选项是使用**SQLBindCol**和**SQLGetData**的组合。 例如，应用程序可以绑定结果集的前十列，然后，每次提取时，调用**SQLGetData**三次从三个未绑定列检索数据。 当结果集包含一个或多个**文本**或**图像**列时，通常会使用此选项。  
  
 根据为结果集设置的游标选项，应用程序还可以使用**SQLFetchScroll**的滚动选项在结果集周围滚动。  
  
 过度使用**SQLBindCol**将结果集列绑定到程序变量的成本很高，因为**SQLBindCol**会导致 ODBC 驱动程序分配内存。 将结果列绑定到变量时，该绑定将保持有效状态，直到调用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)以释放语句句柄或将[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)设置为*fOption*SQL_UNBIND。 在该语句完成前绑定不自动撤消。  
  
 通过这一逻辑，您可以高效地处理使用不同参数多次执行同一 SELECT 语句的情况。 由于结果集保持相同的结构，因此可以绑定结果集一次，处理所有 SELECT 语句，然后调用**SQLFreeStmt，fOption**设置为上次执行后SQL_UNBIND。 *fOption* 如果不首先调用**SQLFreeStmt，** 则不应调用**SQLBindCol**将列绑定到结果集中，*而 fOption*设置为SQL_UNBIND以释放任何以前的绑定。  
  
 使用**SQLBindCol**时，可以执行按行绑定或按列绑定。 按行绑定比按列绑定稍快。  
  
 您可以使用**SQLGetData**逐列检索数据，而不是使用**SQLBindCol**绑定结果集列。 如果结果集仅包含几行，则使用**SQLGetData**而不是**SQLBindCol**会更快;否则 **，SQLBindCol**可提供最佳性能。 如果不总是将数据放在同一组变量中，则应使用**SQLGetData**而不是不断重新绑定。 只有在所有列都绑定到**SQLBindCol**后，才能在选择列表中的列上使用**SQLGetData。** 该列还必须显示在已使用**SQLGetData**的任何列之后。  
  
 处理将数据移动到程序变量（如**SQLGetData、SQLBindCol**和[SQLBind参数](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)）的**SQLBindCol**ODBC 函数支持隐式数据类型转换。 例如，如果应用程序将某一整数列绑定到某一字符串程序变量，则驱动程序将会首先自动把数据从整数转换为字符，然后将其置于该程序变量中。  
  
 应用程序中的数据转换应尽可能少。 如果对应用程序执行的处理不要求数据转换，则应用程序应将列和参数绑定到同一数据类型的程序变量。 但是，如果数据必须从一种类型转换为另一种类型，让驱动程序执行转换比在应用程序中执行转换的效率更高。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通常只将数据直接从网络缓冲区传输到应用程序的变量。 请求驱动程序执行数据转换将强制驱动程序把数据存入缓冲区并使用 CPU 周期来转换数据。  
  
 程序变量应足够大，以保存从列传输的数据，文本 **、ntext**和**text****图像**数据除外。 如果某一应用程序尝试检索结果集数据，而放置这些数据的变量太小以致无法保存数据，则驱动程序将生成一个警告。 这强制驱动程序为消息分配内存，并且驱动程序和应用程序都必须将 CPU 周期花在处理消息和执行错误处理上。 应用程序应或者分配在大小上足以存放检索的数据的变量，或者在选择列表中使用 SUBSTRING 函数减小结果集中列的大小。  
  
 在使用 SQL_C_DEFAULT 指定 C 变量的类型时必须小心。 SQL_C_DEFAULT 指定 C 变量的类型与列或参数的 SQL 数据类型匹配。 如果为**ntext、nchar****nchar**或**nvarchar**列指定SQL_C_DEFAULT，则 Unicode 数据将返回到应用程序。 如果尚未对应用程序进行编码以处理 Unicode 数据，则上述操作可能导致不同的问题。 **唯一标识符**（SQL_GUID） 数据类型也可能发生相同类型的问题。  
  
 **文本****、ntext**和**图像**数据通常太大，无法放入单个程序变量中，通常使用**SQLGetData**而不是**SQLBindCol**进行处理。 使用服务器游[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标时，本机客户端 ODBC 驱动程序经过优化，在提取行时不会传输未绑定**文本****、ntext**或**图像**列的数据。 在应用程序为列发出**SQLGetData**之前，实际上不会从服务器检索**文本****、ntext**或**图像**数据。  
  
 此优化可以应用于应用程序，以便在用户上下滚动光标时不显示**文本****、ntext**或**图像**数据。 用户选择行后，应用程序可以调用**SQLGetData**来检索**文本****、ntext**或**图像**数据。 这样可以节省用户未选择的任何行的传输**文本****、ntext**或**图像**数据，并可以保存传输大量数据。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
