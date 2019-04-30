---
title: 编写 ODBC 3.x 应用程序 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 93c8510bb23bb57244590a472073fc882f9fe64f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208455"
---
# <a name="writing-odbc-3x-applications"></a>编写 ODBC 3.x 应用程序
当 ODBC 2。*x*应用程序升级到 ODBC 3。*x*，它应该这样编写的它适用于这两个 ODBC 2。*x*和 3。*x*驱动程序。 应用程序应将条件代码充分利用 ODBC 3。*x*功能。  
  
 SQL_ATTR_ODBC_VERSION 环境属性应设置为 SQL_OV_ODBC2。 这将确保，驱动程序的行为类似于 ODBC 2 *.x*驱动程序的部分中所述的更改方面[行为的更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 应用程序将使用的部分中所述的功能[新增功能](../../../odbc/reference/develop-app/new-features.md)，应使用条件代码以确定驱动程序是否为 ODBC 3。*x*或 ODBC 2 *.x*驱动程序。 应用程序使用**SQLGetDiagField**并**SQLGetDiagRec**若要获取 ODBC 3。*x* SQLSTATEs 的同时对这些条件的代码片段的处理的错误。 应考虑的新功能有关的以下几点：  
  
-   受影响的行集大小行为中的更改应用程序应小心，不要调用**SQLFetch**数组大小大于 1 时。 这些应用程序应替换为调用**SQLExtendedFetch**通过调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ARRAY_STATUS_PTR 语句属性和**SQLFetchScroll**，以便它们具有适用于这两个 ODBC 3 的通用代码。*x*和 ODBC 2。*x*驱动程序。 因为**SQLSetStmtAttr**使用 SQL_ATTR_ROW_ARRAY_SIZE 将映射到**SQLSetStmtAttr**与 ODBC 2 SQL_ROWSET_SIZE。*x*驱动程序，应用程序可以只将 SQL_ATTR_ROW_ARRAY_SIZE 设置为其多行提取操作。  
  
-   要升级的大多数应用程序实际上不受 SQLSTATE 代码中的更改。 对于这些应用程序会受到影响，它们可以执行机械搜索和替换在大多数情况下使用"SQLSTATE 映射"部分中的错误转换表以转换 ODBC 3。*x*错误代码为 ODBC 2 *.x*代码。 ODBC 3 以来 *.x*驱动程序管理器将从 ODBC 2 执行映射。*x* SQLSTATEs 到 ODBC 3。*x* SQLSTATEs，这些应用程序编写器需要仅检查对 ODBC 3。*x* SQLSTATEs 并且不用担心包括 ODBC 2。*x* SQLSTATEs 中的条件代码。  
  
-   如果应用程序充分利用了日期、 时间和时间戳数据类型，该应用程序可以将其自身声明为 ODBC 2。*x*应用程序和使用其现有的代码而不是使用空调代码。  
  
 升级还应包括以下步骤：  
  
-   调用**SQLSetEnvAttr**之前分配的连接将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2。  
  
-   替换为对所有调用**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**通过调用**SQLAllocHandle**具有相应*HandleType* SQL_HANDLE_ENV、 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的参数。  
  
-   替换为对所有调用**SQLFreeEnv**或**SQLFreeConnect**通过调用**SQLFreeHandle**具有相应*HandleType*参数SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
-   替换为对所有调用**SQLSetConnectOption**通过调用**SQLSetConnectAttr**。 如果一个字符串，其值设置属性，则设置*StringLength*参数正确。 更改*特性*SQL_ATTR_XXXX 从 SQL_XXXX 参数。  
  
-   替换为对所有调用**SQLGetConnectOption**通过调用**SQLGetConnectAttr**。 如果得到的字符串或二进制属性，设置*BufferLength*到适当的值并传入*StringLength*参数。 更改*特性*SQL_ATTR_XXXX 从 SQL_XXXX 参数。  
  
-   替换为对所有调用**SQLSetStmtOption**通过调用**SQLSetStmtAttr**。 如果一个字符串，其值设置属性，则设置*StringLength*参数正确。 更改*特性*SQL_ATTR_XXXX 从 SQL_XXXX 参数。  
  
-   替换为对所有调用**SQLGetStmtOption**通过调用**SQLGetStmtAttr**。 如果得到的字符串或二进制属性，设置*BufferLength*到适当的值并传入*StringLength*参数。 更改*特性*SQL_ATTR_XXXX 从 SQL_XXXX 参数。  
  
-   替换为对所有调用**SQLTransact**通过调用**SQLEndTran**。 如果在最右侧的有效句柄**SQLTransact**调用是环境句柄， *HandleType*应在中使用参数设为 SQL_HANDLE_ENV **SQLEndTran**调用适当*处理*参数。 如果在最右侧的有效句柄你**SQLTransact**调用是连接句柄， *HandleType*应在中使用参数设为 SQL_HANDLE_DBC **SQLEndTran**调用适当*处理*参数。  
  
-   替换为对所有调用**SQLColAttributes**通过调用**SQLColAttribute**。 如果*FieldIdentifier*参数为 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH 时，不会更改函数的名称之外的任何内容。 如果没有，请更改*FieldIdentifier*从到 SQL_DESC_XXXX SQL_COLUMN_XXXX。 如果*FieldIdentifier*为 SQL_DESC_CONCISE_TYPE 且数据类型为 datetime 数据类型，将更改为相应的 ODBC 3 *.x*数据类型。  
  
-   如果使用块游标、 可滚动游标，或这两者，应用程序执行以下任务：  
  
    -   设置行集大小、 游标类型和游标并发使用**SQLSetStmtAttr**。  
  
    -   调用**SQLSetStmtAttr**若要将 SQL_ATTR_ROW_STATUS_PTR 设置为指向状态记录的数组。  
  
    -   调用**SQLSetStmtAttr**设置为指向 SQLINTEGER SQL_ATTR_ROWS_FETCHED_PTR。  
  
    -   执行所需的绑定，并执行 SQL 语句。  
  
    -   调用**SQLFetchScroll**在一个循环，以便提取行，然后在结果中移动设置。  
  
    -   如果想要按书签提取，在应用程序调用**SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR 设的变量将包含书签的行，其目的是要提取，并调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK 参数。  
  
-   如果使用的参数的数组，该应用程序执行以下任务：  
  
    -   调用**SQLSetStmtAttr**将 SQL_ATTR_PARAMSET_SIZE 特性设置为参数数组的大小。  
  
    -   调用**SQLSetStmtAttr**设置 SQL_ATTR_ROWS_PROCESSED_PTR 为指向一个内部 UDWORD 变量。  
  
    -   执行准备、 绑定，并执行相应操作。  
  
    -   如果出于某种原因 （如 SQL_NEED_DATA) 就会停止执行，它可以通过检查由 SQL_ATTR_ROWS_PROCESSED_PTR 指向的位置查找参数的"当前"行。  
  
 本部分包含以下主题。  
  
-   [映射替换函数以实现应用程序后向兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [调用 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [调用 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [调用 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [游标库操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [映射游标 Attributes1 信息类型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
