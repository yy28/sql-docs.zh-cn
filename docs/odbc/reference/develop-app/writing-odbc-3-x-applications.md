---
title: 编写 ODBC 3.x 应用程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288985"
---
# <a name="writing-odbc-3x-applications"></a>编写 ODBC 3.x 应用程序
当 ODBC *2.x*应用程序升级到 ODBC *3.x*时，应编写它，以便它同时适用于 ODBC *2.x*和*3.x*驱动程序。 应用程序应合并条件代码以充分利用 ODBC *3.x*功能。  
  
 SQL_ATTR_ODBC_VERSION环境属性应设置为SQL_OV_ODBC2。 这将确保驱动程序的行为类似于 ODBC *2.x*驱动程序相对于"[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)"部分中描述的更改。  
  
 如果应用程序将使用"[新功能](../../../odbc/reference/develop-app/new-features.md)"部分中描述的任何功能，则应使用条件代码来确定驱动程序是 ODBC *3.x*还是 ODBC *2.x*驱动程序。 应用程序使用**SQLGetDiagField**和**SQLGetDiagRec**来获取 ODBC *3.x* SQLSTATEs，同时对这些条件代码片段执行错误处理。 应考虑有关新功能的以下几点：  
  
-   受行组大小行为更改影响的应用程序在数组大小大于 1 时，应小心不要调用**SQLFetch。** 这些应用程序应用对**SQLSetStmtAttr**的调用替换对**SQLAtttAttr**的调用，以设置SQL_ATTR_ARRAY_STATUS_PTR语句属性和**SQLFetchScroll，** 以便它们具有适用于 ODBC *3.x*和 ODBC *2.x*驱动程序的通用代码。 由于带有SQL_ATTR_ROW_ARRAY_SIZE的**SQLSetStmtAttr**将映射到具有 SQL_ROWSET_SIZE的 ODBC *2.x*驱动程序的**SQLSetStmtAttr，** 因此应用程序只需为其多行提取操作设置SQL_ATTR_ROW_ARRAY_SIZE即可。  
  
-   大多数正在升级的应用程序实际上不受 SQLSTATE 代码更改的影响。 对于受影响的应用程序，在大多数情况下，可以使用"SQLSTATE 映射"部分中的错误转换表将 ODBC *3.x*错误代码转换为 ODBC *2.x*代码，进行机械搜索和替换。 由于 ODBC *3.x*驱动程序管理器将执行从 ODBC *2.x* SQLSTAT 到 ODBC *3.x* SQLSTAT 的映射，因此这些应用程序编写器只需检查 ODBC *3.x* SQLSTATEs，而不必担心在条件代码中包括 ODBC *2.x* SQLSTAT。  
  
-   如果应用程序充分利用了日期、时间和时间戳数据类型，则应用程序可以声明自己是 ODBC *2.x*应用程序，并使用其现有代码而不是使用调理代码。  
  
 升级还应包括以下步骤：  
  
-   在分配连接以将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC2之前，请调用**SQLSetEnvAttr。**  
  
-   将对**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt**的所有调用替换为对**SQLAllocHandle**的调用，以及SQL_HANDLE_ENV、SQL_HANDLE_DBC或SQL_HANDLE_STMT的相应*HandleType*参数。 **SQLAllocConnect**  
  
-   将**SQLFreeEnv**或**SQLFreeConnect**的所有调用替换为对**SQLFreeHandle**的调用，以及SQL_HANDLE_DBC或SQL_HANDLE_STMT的相应*HandleType*参数。  
  
-   将**SQLSetConnectOption**的所有调用替换为对**SQLSetConnectAttr 的**调用。 如果设置其值为字符串的属性，则适当设置*StringLength*参数。 将*属性*参数从SQL_XXXX更改为SQL_ATTR_XXXX。  
  
-   将**SQLGetConnectOption**的所有调用替换为对**SQLGetConnectAttr 的**调用。 如果获取字符串或二进制属性，则将*BufferLength*设置为适当的值并传递*StringLength 参数*。 将*属性*参数从SQL_XXXX更改为SQL_ATTR_XXXX。  
  
-   将**SQLSetStmtOption**的所有调用替换为对**SQLSetStmtAttr 的**调用。 如果设置其值为字符串的属性，则适当设置*StringLength*参数。 将*属性*参数从SQL_XXXX更改为SQL_ATTR_XXXX。  
  
-   将所有对**SQLGetStmtOption**的调用替换为对**SQLGetStmtAttr 的**调用。 如果获取字符串或二进制属性，则将*BufferLength*设置为适当的值并传递*StringLength 参数*。 将*属性*参数从SQL_XXXX更改为SQL_ATTR_XXXX。  
  
-   将**SQLTransact**的所有调用替换为对**SQLEndTran**的调用。 如果**SQLTransact**调用中最正确的句柄是环境句柄，则应在**SQLEndTran**调用中使用 SQL_HANDLE_ENV的*句柄类型*参数，并带有相应的*句柄*参数。 如果**SQLTransact**调用中最正确的句柄是连接句柄，则应在**SQLEndTran**调用中使用SQL_HANDLE_DBC的*句柄类型*参数，并带有相应的*句柄*参数。  
  
-   将**SQLColattributes**的所有调用替换为对**SQLColattribute 的**调用。 如果*FieldIdentifier*参数是SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE或SQL_COLUMN_LENGTH，则不要更改函数名称以外的任何内容。 如果没有，则将*字段标识符*从SQL_COLUMN_XXXX更改为SQL_DESC_XXXX。 如果*字段标识符*SQL_DESC_CONCISE_TYPE并且数据类型是日期时间数据类型，则更改为相应的 ODBC *3.x*数据类型。  
  
-   如果使用块游标、可滚动游标或两者，则应用程序执行以下操作：  
  
    -   使用**SQLSetStmtAttr**设置行组大小、游标类型和游标并发。  
  
    -   调用**SQLSetStmtAttr**以设置SQL_ATTR_ROW_STATUS_PTR以指向状态记录数组。  
  
    -   调用**SQLSetStmtAttr**以设置SQL_ATTR_ROWS_FETCHED_PTR以指向 SQLINTEGER。  
  
    -   执行所需的绑定并执行 SQL 语句。  
  
    -   在循环中调用**SQLFetchScroll**以提取行并在结果集中移动。  
  
    -   如果应用程序希望按书签获取，则应用程序将调用**SQLSetStmtAttr**以将SQL_ATTR_FETCH_BOOKMARK_PTR设置为一个变量，该变量将包含要提取的行的书签，并且使用 SQL_FETCH_BOOKMARK的 Fetch*方向*参数调用**SQLFetchScroll。**  
  
-   如果使用参数数组，应用程序将执行以下操作：  
  
    -   调用**SQLSetStmtAttr**将SQL_ATTR_PARAMSET_SIZE属性设置为参数数组的大小。  
  
    -   调用**SQLSetStmtAttr**以设置SQL_ATTR_ROWS_PROCESSED_PTR以指向内部 UDWORD 变量。  
  
    -   根据需要执行准备、绑定和执行操作。  
  
    -   如果执行由于某种原因（如SQL_NEED_DATA）停止，它可以通过检查SQL_ATTR_ROWS_PROCESSED_PTR指向的位置来查找参数的"当前"行。  
  
 本部分包含以下主题。  
  
-   [映射替换函数以实现应用程序后向兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [调用 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [调用 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [调用 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [游标库操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [映射游标 Attributes1 信息类型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
