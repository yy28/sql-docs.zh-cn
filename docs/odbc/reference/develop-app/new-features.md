---
title: 新功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302395"
---
# <a name="new-features"></a>新增功能
ODBC *3.x*中引入了以下新功能。 使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序将无法使用此功能。 使用 ODBC *2.x*驱动程序时，ODBC *3.x*驱动程序管理器不会映射这些功能。  
  
-   以描述符句柄为参数的函数：SQLSetDescField、SQLGetDescField、SQLSetDescRec、SQLGetDescRec 和**SQLCopyDesc**。 **SQLSetDescField** **SQLGetDescField** **SQLSetDescRec** **SQLGetDescRec**  
  
-   函数**SQLSetEnvAttr**和**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**来分配描述符句柄。 （使用**SQLAllocHandle**分配环境、连接和语句句柄是重复的，而不是新的功能。  
  
-   使用**SQLGetConnectAttr**获取SQL_ATTR_AUTO_IPD连接属性。 （使用**SQLSetConnectAttr**设置，并使用**SQLGetConnectAttr**来获取其他连接属性是重复的，而不是新的功能。  
  
-   使用**SQLSetStmtAttr 设置 SQLTmtAttr，** 以及**SQLGetStmtAttr**来获取以下语句属性。 （使用**SQLSetStmtAttr**来设置，并且**SQLGetStmtAttr**来获取其他语句属性是重复的，而不是新的。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   使用**SQLGetStmtAttr**获取以下语句属性。 （使用**SQLGetStmtAttr**获取其他语句属性是重复的功能，而不是新功能。  
  
     SQL_ATTR_IMP_ROW_DESCSQL_ATTR_IMP_PARAM_DESC  
  
-   使用间隔 C 数据类型、间隔 SQL 数据类型、BIGINT C 数据类型和SQL_C_NUMERIC数据结构。  
  
-   参数的行绑定。  
  
-   基于偏移的书签提取，例如使用fetch*方向*参数SQL_FETCH_BOOKMARK调用**SQLFetchScroll，** 并指定偏移量（而不是 0）。  
  
-   **SQLFetch**返回行状态数组、提取的行数、获取多行、将调用与**SQLFetchScroll**混合，以及将调用与**SQLBulk 操作**或**SQLSetPos**混合。 有关详细信息，请参阅下一节"[块光标、可滚动光标"和 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   命名参数。  
  
-   任何 ODBC *3.x*特定**SQLGetInfo**选项。 （如果使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用SQL_XXX_CURSOR_ATTRIBUTES1信息类型，这些类型已替换了多个 ODBC *2.x*信息类型，则某些信息可能可靠，但有些信息可能不可靠。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。）  
  
-   绑定偏移。  
  
-   按书签（通过调用**SQLBulk 操作**）更新、刷新和删除。  
  
-   在 S5 状态下调用**SQLBulk 操作**或**SQLSetPos。**  
  
-   诊断记录中ROW_NUMBER和COLUMN_NUMBER字段（必须通过替换函数**SQLGetDiagField**或**SQLGetDiagRec**检索）。  
  
-   近似行计数。  
  
-   警告信息（从**SQLFetchScroll SQL_ROW_SUCCESS_WITH_INFO）。**  
  
-   可变长度书签。  
  
-   参数数组的扩展错误信息。  
  
-   目录函数返回的结果集中的所有新列。  
  
-   在列 0 上使用**SQLDescribeCol**和**SQLColAttribute。**  
  
-   在调用**SQLColAttribute**中使用任何 ODBC *3.x*特定的列属性。  
  
-   使用多个环境句柄。  
  
 本节包含以下主题。  
  
-   [ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
