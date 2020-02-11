---
title: 编写 ODBC 1.x 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9939d11e3a779cc25d7faeb4950783353947f140
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081448"
---
# <a name="writing-odbc-3x-applications"></a>编写 ODBC 3.x 应用程序
当 ODBC 2.x*应用程序*升级到 odbc 2.x*时，应*编写该*应用程序，* 使其适用于 odbc *2.x 和 1.x*版驱动程序。 应用程序应结合使用条件代码才能充分*利用 ODBC 1.x*功能。  
  
 SQL_ATTR_ODBC_VERSION 环境特性应设置为 SQL_OV_ODBC2。 这将确保*驱动程序的行为与 ODBC 2.x*驱动程序的行为类似于 "[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)" 部分中描述的更改。  
  
 如果应用程序将使用 "[新功能](../../../odbc/reference/develop-app/new-features.md)" 一节中所述的任何功能，则应该使用条件代码来确定驱动程序*是 ODBC 3.x 还是 odbc 2.x*驱动*程序*。 应用程序使用**SQLGetDiagField**和**SQLGetDiagRec** *获取 ODBC 2.x* SQLSTATEs，同时在这些条件代码段上执行错误处理。 应考虑有关新功能的下列几点：  
  
-   当数组大小大于1时，受行集大小行为更改影响的应用程序应注意不要调用**SQLFetch** 。 这些应用程序应将对**SQLExtendedFetch**的调用替换为对**SQLSetStmtAttr**的调用，以设置 SQL_ATTR_ARRAY_STATUS_PTR 语句特性和**SQLFetchScroll**，因此它们具有适用*于 ODBC 1.x 和 odbc 2.x*驱动程序的通用*代码。* 由于带有 SQL_ATTR_ROW_ARRAY_SIZE 的**SQLSetStmtAttr**将映射到**SQLSetStmtAttr** *的 ODBC 2.X*驱动程序的 SQL_ROWSET_SIZE，因此应用程序只需为其多行提取操作设置 SQL_ATTR_ROW_ARRAY_SIZE。  
  
-   大多数正在升级的应用程序实际上不受 SQLSTATE 代码中的更改的影响。 对于受影响的应用程序，他们可以在大多数情况下使用 "SQLSTATE 映射" 一节中的错误转换表，将 ODBC 2.x*错误代码转换*为*odbc 2.x*代码，并进行机械搜索和替换。 由于 ODBC 1.x*驱动程序*管理器将执行从 odbc *2.X SQLSTATEs 到*odbc *1.x SQLSTATEs 的*映射，因此，这些应用程序编写器只需检查 odbc 2.x SQLSTATEs，无需担心在条件代码中*包含 odbc 2.x* *SQLSTATEs。*  
  
-   如果应用程序充分利用了日期、时间和时间戳数据类型，应用程序可以将其自身声明*为 ODBC 2.x*应用程序并使用其现有代码，而不是使用调节代码。  
  
 升级还应包括以下步骤：  
  
-   在分配连接之前调用**SQLSetEnvAttr** ，以将 SQL_ATTR_ODBC_VERSION 环境特性设置为 SQL_OV_ODBC2。  
  
-   将对**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**的所有调用替换为带有 SQL_HANDLE_ENV、SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 相应*HandleType*参数的**SQLAllocHandle**调用。  
  
-   将对**SQLFreeEnv**或**SQLFreeConnect**的所有调用替换为带有 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的相应*HandleType*参数的**SQLFreeHandle**调用。  
  
-   将对**SQLSetConnectOption**的所有调用替换为对**SQLSetConnectAttr**的调用。 如果设置的属性的值为字符串，则相应地设置*StringLength*参数。 将*属性*参数从 SQL_XXXX 更改为 SQL_ATTR_XXXX。  
  
-   将对**SQLGetConnectOption**的所有调用替换为对**SQLGetConnectAttr**的调用。 如果获取字符串或二进制属性，请将*BufferLength*设置为适当的值，并传入*StringLength*参数。 将*属性*参数从 SQL_XXXX 更改为 SQL_ATTR_XXXX。  
  
-   将对**SQLSetStmtOption**的所有调用替换为对**SQLSetStmtAttr**的调用。 如果设置的属性的值为字符串，则相应地设置*StringLength*参数。 将*属性*参数从 SQL_XXXX 更改为 SQL_ATTR_XXXX。  
  
-   将对**SQLGetStmtOption**的所有调用替换为对**SQLGetStmtAttr**的调用。 如果获取字符串或二进制属性，请将*BufferLength*设置为适当的值，并传入*StringLength*参数。 将*属性*参数从 SQL_XXXX 更改为 SQL_ATTR_XXXX。  
  
-   将对**SQLTransact**的所有调用替换为对**SQLEndTran**的调用。 如果**SQLTransact**调用中最右边的有效句柄为环境句柄，则应在**SQLEndTran**调用中使用合适的*句*柄参数来使用*HandleType* SQL_HANDLE_ENV 参数。 如果**SQLTransact**调用中最右边的有效句柄是一个连接句柄，则应在**SQLEndTran**调用中将一个*HandleType* SQL_HANDLE_DBC 参数用于适当的*句柄*参数。  
  
-   将对**SQLColAttributes**的所有调用替换为对**SQLColAttribute**的调用。 如果*FieldIdentifier*参数 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH，请不要更改函数名称以外的任何内容。 否则，请将*FieldIdentifier*从 SQL_COLUMN_XXXX 更改为 SQL_DESC_XXXX。 如果*FieldIdentifier* SQL_DESC_CONCISE_TYPE 并且数据类型为 datetime 数据类型，请将更改为相应*的 ODBC 2.x*数据类型。  
  
-   如果使用块游标、可滚动游标或同时使用这两种游标，则应用程序会执行以下操作：  
  
    -   使用**SQLSetStmtAttr**设置行集大小、游标类型和游标并发。  
  
    -   调用**SQLSetStmtAttr** ，将 SQL_ATTR_ROW_STATUS_PTR 设置为指向状态记录的数组。  
  
    -   调用**SQLSetStmtAttr** ，将 SQL_ATTR_ROWS_FETCHED_PTR 设置为指向 SQLINTEGER。  
  
    -   执行所需的绑定并执行 SQL 语句。  
  
    -   调用**SQLFetchScroll**中的以提取行并在结果集内移动。  
  
    -   如果需要按书签提取，应用程序将调用**SQLSetStmtAttr** ，将 SQL_ATTR_FETCH_BOOKMARK_PTR 设置为一个变量，该变量将包含要提取的行的书签，并使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*参数调用**SQLFetchScroll** 。  
  
-   如果使用参数数组，应用程序会执行以下操作：  
  
    -   调用**SQLSetStmtAttr** ，将 SQL_ATTR_PARAMSET_SIZE 特性设置为参数数组的大小。  
  
    -   调用**SQLSetStmtAttr** ，将 SQL_ATTR_ROWS_PROCESSED_PTR 设置为指向内部 UDWORD 变量。  
  
    -   根据需要执行准备、绑定和执行操作。  
  
    -   如果由于某种原因（例如 SQL_NEED_DATA）而暂停执行，则可以通过检查 SQL_ATTR_ROWS_PROCESSED_PTR 指向的位置来查找参数的 "当前" 行。  
  
 本部分包含下列主题。  
  
-   [映射替换函数以实现应用程序后向兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [调用 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [调用 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [调用 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [游标库操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [映射游标 Attributes1 信息类型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
