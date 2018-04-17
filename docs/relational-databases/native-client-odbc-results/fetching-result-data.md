---
title: 提取结果数据 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f1c828f3e63e3167a0685f450e318055a9b71fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-result-data"></a>提取结果数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 应用程序具有三个用于提取结果数据的选项。  
  
 第一个选项基于[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)。 提取结果集之前，应用程序使用**SQLBindCol**可将每个列绑定的结果集到程序变量中。 驱动程序传输到变量的当前行的数据绑定到每个结果集列每个列已绑定后，时间的应用程序调用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。 如果结果集列和程序变量具有不同的数据类型，则驱动程序将处理数据转换。 如果应用程序具有 SQL_ATTR_ROW_ARRAY_SIZE 设置大于 1，它可以将结果列绑定到的变量，将所有填充每次调用数组**SQLFetchScroll**。  
  
 第二个选项取决于[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 应用程序不使用**SQLBindCol**绑定结果集列移至程序变量。 每次调用后**SQLFetch**，应用程序调用**SQLGetData**一次对于结果中每个列设置。 **SQLGetData**指示驱动程序将从一个特定结果集列的数据传输到特定程序变量以及指定的列和变量的数据类型。 如果结果集列和程序变量具有不同的数据类型，则上述操作将允许驱动程序转换数据。 **文本**， **ntext**，和**映像**列通常是太大而无法放入程序变量，但仍可以使用检索**SQLGetData**。 如果**文本**， **ntext**，或**映像**结果列中的数据大于程序变量中， **SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字符串数据，右截断）。 对连续调用**SQLGetData**返回的连续区块**文本**或**映像**数据。 当达到数据末尾时， **SQLGetData**返回 SQL_SUCCESS。 如果 SQL_ATTR_ROW_ARRAY_SIZE 大于 1，则每个提取都将返回一组行或行集。 在使用之前**SQLGetData**，必须首先使用**SQLSetPos**若要指定为当前行的行集内的特定行。  
  
 第三个选项是使用多种**SQLBindCol**和**SQLGetData**。 应用程序无法，例如，绑定结果集的前 10 个列，然后，在每次提取调用**SQLGetData**三次以从三个未绑定列检索数据。 将通常时使用此结果集包含一个或多个**文本**或**映像**列。  
  
 具体取决于游标选项设置为结果集，应用程序也可以使用的滚动选项**SQLFetchScroll**滚动解决结果集。  
  
 额外的使用**SQLBindCol**将结果绑定到程序变量集列将占用大量资源因为**SQLBindCol**导致 ODBC 驱动程序分配内存。 绑定时的结果列给一个变量，该绑定保持有效，直到你调用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)要释放的语句句柄或调用[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)与*fOption*设置为 SQL_UNBIND。 在该语句完成前绑定不自动撤消。  
  
 通过这一逻辑，您可以高效地处理使用不同参数多次执行同一 SELECT 语句的情况。 因为结果集保留相同的结构，你可以一次绑定结果集，处理所有 SELECT 语句，然后调用**SQLFreeStmt**与*fOption*在上一次执行后设置为 SQL_UNBIND。 不应调用**SQLBindCol**将列绑定中的结果集而无需首先调用**SQLFreeStmt**与*fOption*设置为 SQL_UNBIND 以释放以前的任何绑定。  
  
 使用时**SQLBindCol**，你可以按行或列绑定任一执行。 按行绑定比按列绑定稍快。  
  
 你可以使用**SQLGetData**以检索上而不是绑定结果的列由列基础数据集使用的列**SQLBindCol**。 如果结果集包含仅少量的行，使用**SQLGetData**而不是**SQLBindCol**更快; 否则为**SQLBindCol**能够提供最佳性能。 如果你不将数据在相同的变量集始终放，则应使用**SQLGetData**而不是不断地重新绑定。 你只能使用**SQLGetData**上列都选择列表中的所有列都绑定使用之后**SQLBindCol**。 之后你已使用在其的任何列，该列必须还显示**SQLGetData**。  
  
 ODBC 函数将数据移入 （出） 程序变量，如以便处理**SQLGetData**， **SQLBindCol**，和[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)，支持隐式数据类型转换。 例如，如果应用程序将某一整数列绑定到某一字符串程序变量，则驱动程序将会首先自动把数据从整数转换为字符，然后将其置于该程序变量中。  
  
 应用程序中的数据转换应尽可能少。 如果对应用程序执行的处理不要求数据转换，则应用程序应将列和参数绑定到同一数据类型的程序变量。 但是，如果数据必须从一种类型转换为另一种类型，让驱动程序执行转换比在应用程序中执行转换的效率更高。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序通常只将数据直接从网络缓冲区传输到应用程序的变量。 请求驱动程序执行数据转换将强制驱动程序把数据存入缓冲区并使用 CPU 周期来转换数据。  
  
 程序变量应足够大以保存从列，在传输除外的数据**文本**， **ntext**，和**映像**数据。 如果某一应用程序尝试检索结果集数据，而放置这些数据的变量太小以致无法保存数据，则驱动程序将生成一个警告。 这强制驱动程序为消息分配内存，并且驱动程序和应用程序都必须将 CPU 周期花在处理消息和执行错误处理上。 应用程序应或者分配在大小上足以存放检索的数据的变量，或者在选择列表中使用 SUBSTRING 函数减小结果集中列的大小。  
  
 在使用 SQL_C_DEFAULT 指定 C 变量的类型时必须小心。 SQL_C_DEFAULT 指定 C 变量的类型与列或参数的 SQL 数据类型匹配。 如果为指定 SQL_C_DEFAULT **ntext**， **nchar**，或**nvarchar**列中，Unicode 数据返回到应用程序。 如果尚未对应用程序进行编码以处理 Unicode 数据，则上述操作可能导致不同的问题。 相同类型的问题可能会出现**uniqueidentifier** (SQL_GUID) 数据类型。  
  
 **文本**， **ntext**，和**映像**数据通常是太大而无法放到单个程序变量中，并且通常与处理**SQLGetData**而不是**SQLBindCol**。 使用服务器游标时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序进行了优化以不传输数据的未绑定**文本**， **ntext**，或**映像**上的列提取行的时间。 **文本**， **ntext**，或**映像**数据不实际从服务器检索之前应用程序问题**SQLGetData**的列。  
  
 此优化可以应用于应用程序，以便不**文本**， **ntext**，或**映像**用户滚动向上和向下游标时，将显示数据。 用户选择一行后，应用程序可以调用**SQLGetData**检索**文本**， **ntext**，或**映像**数据。 这将保存传输**文本**， **ntext**，或**映像**数据的任何行用户不会选择，并可以保存的数据量非常大的传输。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
