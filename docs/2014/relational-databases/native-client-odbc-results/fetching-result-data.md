---
title: 提取结果数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b803ca3742f9cb831e51105aab9d0ed75ad78e16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200079"
---
# <a name="fetching-result-data"></a>提取结果数据
  ODBC 应用程序具有三个用于提取结果数据的选项。  
  
 第一个选项基于[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)。 应用程序提取结果集之前，请使用**SQLBindCol**可将每个列绑定的结果集到程序变量中。 驱动程序传输到的变量的当前行的数据绑定到每个结果集列每个绑定列后，时间的应用程序调用**SQLFetch**或[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。 如果结果集列和程序变量具有不同的数据类型，则驱动程序将处理数据转换。 如果应用程序将 SQL_ATTR_ROW_ARRAY_SIZE 设置大于 1，它可以将结果列绑定到变量，将被全部填充每次调用数组**SQLFetchScroll**。  
  
 第二个选项基于[SQLGetData](../native-client-odbc-api/sqlgetdata.md)。 应用程序不使用**SQLBindCol**绑定结果集列移至程序变量。 每次调用后**SQLFetch**，应用程序调用**SQLGetData**一次对于结果中每个列设置。 **SQLGetData**指示驱动程序将数据从一个特定结果集列传输到特定的程序变量，并指定数据类型的列和变量。 如果结果集列和程序变量具有不同的数据类型，则上述操作将允许驱动程序转换数据。 **文本**， **ntext**，和**图像**列通常太大而无法放入某一程序变量，但仍可以使用检索**SQLGetData**。 如果**文本**， **ntext**，或**图像**结果列中的数据大于程序变量**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字符串数据，右端被截断）。 后续调用**SQLGetData**返回的连续块区**文本**或**图像**数据。 当达到数据末尾时， **SQLGetData**返回 SQL_SUCCESS。 如果 SQL_ATTR_ROW_ARRAY_SIZE 大于 1，则每个提取都将返回一组行或行集。 使用之前**SQLGetData**，必须先使用**SQLSetPos**以指定该行集内的特定行作为当前行。  
  
 第三个选项是使用多种**SQLBindCol**并**SQLGetData**。 应用程序可能，例如，将绑定结果集的前十个列，然后，每次提取时，调用**SQLGetData**三次以从三个未绑定的列中检索数据。 这通常时使用结果集包含一个或多个**文本**或**映像**列。  
  
 根据设置为结果集的游标选项，应用程序还可以使用的滚动选项**SQLFetchScroll**滚动结果集。  
  
 过多地利用**SQLBindCol**若要将结果绑定到程序变量的集列是昂贵因为**SQLBindCol**导致 ODBC 驱动程序分配内存。 当结果列绑定到一个变量时，该绑定保持有效，直到调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)以释放语句句柄或调用[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)与*fOption*设置为 SQL_UNBIND。 在该语句完成前绑定不自动撤消。  
  
 通过这一逻辑，您可以高效地处理使用不同参数多次执行同一 SELECT 语句的情况。 由于结果集保持相同的结构，可以一次绑定该结果集，处理所有 SELECT 语句，然后调用**SQLFreeStmt**与*fOption*在上一次执行后设置为 SQL_UNBIND。 不应调用**SQLBindCol**将列绑定结果集中没有首先调用**SQLFreeStmt**与*fOption*设置为 SQL_UNBIND 以释放任何以前的绑定。  
  
 使用时**SQLBindCol**，您可以执行按行或按列绑定。 按行绑定比按列绑定稍快。  
  
 可以使用**SQLGetData**来检索数据而不是绑定结果基于列的列集使用的列**SQLBindCol**。 如果结果集包含只有几行，使用**SQLGetData**而不是**SQLBindCol**速度更快; 否则为**SQLBindCol**可提供最佳性能。 如果您不要在同一变量集中始终将数据，则应使用**SQLGetData**而不是不断地重新绑定。 您只能使用**SQLGetData**与绑定所有列后，将选择列表中的列**SQLBindCol**。 你已使用的任何列之后必须还显示该列**SQLGetData**。  
  
 ODBC 函数将数据移入或移出程序变量，如**SQLGetData**， **SQLBindCol**，并[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)，支持隐式数据类型转换。 例如，如果应用程序将某一整数列绑定到某一字符串程序变量，则驱动程序将会首先自动把数据从整数转换为字符，然后将其置于该程序变量中。  
  
 应用程序中的数据转换应尽可能少。 如果对应用程序执行的处理不要求数据转换，则应用程序应将列和参数绑定到同一数据类型的程序变量。 但是，如果数据必须从一种类型转换为另一种类型，让驱动程序执行转换比在应用程序中执行转换的效率更高。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通常只将数据直接从网络缓冲区传输到应用程序的变量。 请求驱动程序执行数据转换将强制驱动程序把数据存入缓冲区并使用 CPU 周期来转换数据。  
  
 程序变量应该足够大以保存数据从某一列，在传输除外**文本**， **ntext**，并**图像**数据。 如果某一应用程序尝试检索结果集数据，而放置这些数据的变量太小以致无法保存数据，则驱动程序将生成一个警告。 这强制驱动程序为消息分配内存，并且驱动程序和应用程序都必须将 CPU 周期花在处理消息和执行错误处理上。 应用程序应或者分配在大小上足以存放检索的数据的变量，或者在选择列表中使用 SUBSTRING 函数减小结果集中列的大小。  
  
 在使用 SQL_C_DEFAULT 指定 C 变量的类型时必须小心。 SQL_C_DEFAULT 指定 C 变量的类型与列或参数的 SQL 数据类型匹配。 如果为指定 SQL_C_DEFAULT **ntext**， **nchar**，或**nvarchar**列中，Unicode 数据返回到应用程序。 如果尚未对应用程序进行编码以处理 Unicode 数据，则上述操作可能导致不同的问题。 相同类型的问题可能会出现**uniqueidentifier** (SQL_GUID) 数据类型。  
  
 **文本**， **ntext**，和**图像**数据通常太大而无法放入单个程序变量，并使用通常处理**SQLGetData**而不是**SQLBindCol**。 使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序经过优化，可不传输未绑定数据**文本**， **ntext**，或**映像**上的列提取行时的时间。 **文本**， **ntext**，或**图像**数据不实际从服务器检索到应用程序问题**SQLGetData**为列。  
  
 这种优化可以应用于应用程序，以便无**文本**， **ntext**，或**图像**显示数据，而用户上下滚动游标。 用户选择某一行后，应用程序可以调用**SQLGetData**检索**文本**， **ntext**，或者**映像**数据。 这可以避免传输**文本**， **ntext**，或**图像**的任何行的数据的用户不会选择，并可以避免传输非常大量的数据。  
  
## <a name="see-also"></a>请参阅  
 [处理结果&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
