---
title: 编写 ODBC 3.x 应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61809072272ae91c32d4780971735c29c53fe977
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="writing-odbc-3x-applications"></a>编写 ODBC 3.x 应用程序
当一个 ODBC 2。*x*应用程序升级到 ODBC 3。*x*，以便它适用于这两个 ODBC 2 应编写它。*x*和 3。*x*驱动程序。 应用程序应满足条件的代码，以充分利用 ODBC 3。*x*功能。  
  
 SQL_ATTR_ODBC_VERSION 环境属性应设置为 SQL_OV_ODBC2。 这将确保该驱动程序的行为类似 ODBC 2 *.x*方面的部分中所述的更改的驱动程序[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 如果应用程序将使用的任何部分所述功能[新功能](../../../odbc/reference/develop-app/new-features.md)，应使用条件代码以确定是否有 ODBC 3 驱动程序。*x*或 ODBC 2 *.x*驱动程序。 应用程序使用**SQLGetDiagField**和**SQLGetDiagRec**获取 ODBC 3。*x* SQLSTATEs 在执行操作时对这些条件的代码片段的处理的错误。 应考虑的新功能有关的以下几点：  
  
-   受此更改的行集大小行为影响应用程序应注意不要调用**SQLFetch**数组大小大于 1 时。 这些应用程序应替换对的调用**SQLExtendedFetch**通过调用**SQLSetStmtAttr**设置 SQL_ATTR_ARRAY_STATUS_PTR 语句属性并对其**SQLFetchScroll**，以便它们具有公共适用于这两个 ODBC 3 的代码。*x*和 ODBC 2。*x*驱动程序。 因为**SQLSetStmtAttr**与 SQL_ATTR_ROW_ARRAY_SIZE 将映射到**SQLSetStmtAttr**与 ODBC 2 SQL_ROWSET_SIZE。*x*驱动程序，应用程序可以仅将设置 SQL_ATTR_ROW_ARRAY_SIZE 来执行其多行提取操作。  
  
-   要升级的大多数应用程序实际上不受 SQLSTATE 代码中的更改。 对于这些应用程序会受到影响，它们可以执行机械搜索和替换在大多数情况下使用"SQLSTATE 映射"部分中的错误转换表转换 ODBC 3。*x*错误代码为 ODBC 2 *.x*代码。 因为 ODBC 3 *.x*驱动程序管理器将执行从 ODBC 2 的映射。*x*到 ODBC 3 SQLSTATEs。*x* SQLSTATEs，这些应用程序编写器需要不仅检查对 ODBC 3。*x* SQLSTATEs 并且不用担心包括 ODBC 2。*x* SQLSTATEs 条件的代码中。  
  
-   如果应用程序能够很好地使用日期、 时间和时间戳数据类型，应用程序可以将其自身声明为 ODBC 2。*x*应用程序并使用其现有代码，而不是使用调节代码。  
  
 升级还应包括以下步骤：  
  
-   调用**SQLSetEnvAttr**之前分配的连接将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2。  
  
-   将对所有调用**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**通过调用**SQLAllocHandle**使用相应*HandleType* SQL_HANDLE_ENV、 SQL_HANDLE_DBC，或 SQL_HANDLE_STMT 的自变量。  
  
-   将对所有调用**SQLFreeEnv**或**SQLFreeConnect**通过调用**SQLFreeHandle**使用相应*HandleType*自变量SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
-   将对所有调用**SQLSetConnectOption**通过调用**SQLSetConnectAttr**。 如果将属性设置其值是字符串，设置*StringLength*参数正确。 更改*属性*SQL_ATTR_XXXX SQL_XXXX 从自变量。  
  
-   将对所有调用**SQLGetConnectOption**通过调用**SQLGetConnectAttr**。 如果缺少字符串或二进制属性，请设置*BufferLength*到适当的值并传入*StringLength*自变量。 更改*属性*SQL_ATTR_XXXX SQL_XXXX 从自变量。  
  
-   将对所有调用**SQLSetStmtOption**通过调用**SQLSetStmtAttr**。 如果将属性设置其值是字符串，设置*StringLength*参数正确。 更改*属性*SQL_ATTR_XXXX SQL_XXXX 从自变量。  
  
-   将对所有调用**SQLGetStmtOption**通过调用**SQLGetStmtAttr**。 如果缺少字符串或二进制属性，请设置*BufferLength*到适当的值并传入*StringLength*自变量。 更改*属性*SQL_ATTR_XXXX SQL_XXXX 从自变量。  
  
-   将对所有调用**SQLTransact**通过调用**SQLEndTran**。 如果在最右边的有效句柄**SQLTransact**调用是环境句柄， *HandleType* SQL_HANDLE_ENV 参数应在**SQLEndTran**调用相应*处理*自变量。 如果在最右边的有效句柄你**SQLTransact**调用是连接句柄， *HandleType* SQL_HANDLE_DBC 参数应在**SQLEndTran**调用相应*处理*自变量。  
  
-   将对所有调用**SQLColAttributes**通过调用**SQLColAttribute**。 如果*FieldIdentifier*参数或者为 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE，或者 SQL_COLUMN_LENGTH，不将更改的函数名称之外的任何内容。 如果没有，则更改*FieldIdentifier*从到 SQL_DESC_XXXX SQL_COLUMN_XXXX。 如果*FieldIdentifier*是 SQL_DESC_CONCISE_TYPE 和数据类型为 datetime 数据类型，将更改为相应的 ODBC 3 *.x*数据类型。  
  
-   如果使用块状游标和 / 或可滚动游标，该应用程序执行以下任务：  
  
    -   设置行集大小、 游标类型和光标并发使用**SQLSetStmtAttr**。  
  
    -   调用**SQLSetStmtAttr**设置 SQL_ATTR_ROW_STATUS_PTR 为指向数组的状态记录。  
  
    -   调用**SQLSetStmtAttr**设置 SQL_ATTR_ROWS_FETCHED_PTR 以指向 SQLINTEGER。  
  
    -   执行所需的绑定，并执行 SQL 语句。  
  
    -   调用**SQLFetchScroll** in 循环来提取行并移动文件结果中设置。  
  
    -   如果想要提取的书签，在应用程序调用**SQLSetStmtAttr**将 SQL_ATTR_FETCH_BOOKMARK_PTR 设置为变量将包含它想要提取的行和调用的书签**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK 自变量。  
  
-   如果使用的参数数组，该应用程序执行以下任务：  
  
    -   调用**SQLSetStmtAttr**将 SQL_ATTR_PARAMSET_SIZE 特性设置为参数数组的大小。  
  
    -   调用**SQLSetStmtAttr**设置 SQL_ATTR_ROWS_PROCESSED_PTR 为指向一个内部 UDWORD 变量。  
  
    -   执行准备，将绑定，并执行适当的操作。  
  
    -   如果出于某些原因 （例如 SQL_NEED_DATA) 就会停止执行，它可以通过检查由 SQL_ATTR_ROWS_PROCESSED_PTR 指向的位置中查找参数的"当前"的行。  
  
 本部分包含以下主题。  
  
-   [映射替换函数以实现应用程序后向兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [调用 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [调用 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [调用 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [游标库操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [映射游标 Attributes1 信息类型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
