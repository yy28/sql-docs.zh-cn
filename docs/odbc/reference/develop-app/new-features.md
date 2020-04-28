---
title: 新增功能 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302395"
---
# <a name="new-features"></a>新增功能
ODBC 2.x 中引入了以下新*功能。* 使用*odbc 2.x* *驱动程序的 odbc 1.x 应用程序*将无法使用此功能。 当使用*odbc 2.x*驱动程序时，odbc 2.X*驱动程序管理*器不会映射这些功能。  
  
-   采用描述符句柄作为参数的函数： **SQLSetDescField**、 **SQLGetDescField**、 **SQLSetDescRec**、 **SQLGetDescRec**和**SQLCopyDesc**。  
  
-   函数**SQLSetEnvAttr**和**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**分配描述符句柄。 （使用**SQLAllocHandle**分配环境、连接和语句句柄是重复的，而不是新的功能。）  
  
-   使用**SQLGetConnectAttr**获取 SQL_ATTR_AUTO_IPD 连接属性。 （使用**SQLSetConnectAttr**设置和**SQLGetConnectAttr**获取，其他连接属性将重复，而不是新的功能。）  
  
-   使用**SQLSetStmtAttr**设置和**SQLGetStmtAttr**获取下面的语句属性。 （使用**SQLSetStmtAttr**设置和**SQLGetStmtAttr**获取，其他语句特性是重复的，而不是新的功能。）  
  
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
  
-   使用**SQLGetStmtAttr**获取以下语句属性。 （使用**SQLGetStmtAttr**获取其他语句特性是重复的功能，而不是新的功能。）  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用 interval C 数据类型、间隔 SQL 数据类型、BIGINT C 数据类型和 SQL_C_NUMERIC 的数据结构。  
  
-   参数的按行绑定。  
  
-   基于偏移量的书签提取，如使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*参数调用**SQLFetchScroll**并指定0以外的偏移量。  
  
-   **SQLFetch**返回行状态数组、提取的行数、提取多行、通过**SQLFetchScroll**调用混合调用和混合调用（ **SQLBulkOperations**或**SQLSetPos**）。 有关详细信息，请参阅下一节： [ODBC 1.X 应用程序的块游标、可滚动游标和后向兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   命名的参数。  
  
-   任何*ODBC 3.x 特定的* **SQLGetInfo**选项。 （如果使用 ODBC 2.x*驱动程序的 odbc* *1.x 应用程序*调用了已替换几*个 ODBC 2.x*信息类型的 SQL_XXX_CURSOR_ATTRIBUTES1 信息类型，则某些信息可能是可靠的，但有些信息可能是不可靠的。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。）  
  
-   绑定偏移量。  
  
-   由书签更新、刷新和删除（通过调用**SQLBulkOperations**）。  
  
-   调用 S5 状态的**SQLBulkOperations**或**SQLSetPos** 。  
  
-   诊断记录中的 "ROW_NUMBER" 和 "COLUMN_NUMBER" 字段（必须通过替换函数**SQLGetDiagField**或**SQLGetDiagRec**来检索）。  
  
-   大约行计数。  
  
-   警告信息（从**SQLFetchScroll**SQL_ROW_SUCCESS_WITH_INFO）。  
  
-   可变长度书签。  
  
-   有关参数数组的扩展错误信息。  
  
-   目录函数返回的结果集中的所有新列。  
  
-   在列0上使用**SQLDescribeCol**和**SQLColAttribute** 。  
  
-   在对**SQLColAttribute**的调用中使用*任何 ODBC 3.x*特定列特性。  
  
-   使用多个环境句柄。  
  
 本部分包含以下主题。  
  
-   [ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
