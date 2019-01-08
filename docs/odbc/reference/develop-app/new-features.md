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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d425a6896a64f06bf1610ed8f6be87dd60af25d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507418"
---
# <a name="new-features"></a>新功能
在 ODBC 3 引入了以下新功能。*x*。 ODBC 3。*x*应用程序使用 ODBC 2 *.x*驱动程序将不能使用此功能。 ODBC 3。*x*驱动程序管理器不映射这些功能时使用的 ODBC 2 *.x*驱动程序。  
  
-   采用一个说明符的函数处理作为自变量：**SQLSetDescField**， **SQLGetDescField**， **SQLSetDescRec**， **SQLGetDescRec**，并且**SQLCopyDesc**。  
  
-   函数**SQLSetEnvAttr**并**SQLGetEnvAttr**。  
  
-   利用**SQLAllocHandle**以分配描述符句柄。 (使用**SQLAllocHandle**分配环境、 连接和语句句柄是重复的不是新功能。)  
  
-   利用**SQLGetConnectAttr**以获取 SQL_ATTR_AUTO_IPD 连接属性。 (使用**SQLSetConnectAttr**若要设置，并**SQLGetConnectAttr**若要获取，其他连接属性是重复的不是新功能。)  
  
-   利用**SQLSetStmtAttr**若要设置，并**SQLGetStmtAttr**若要获取，以下语句属性。 (使用**SQLSetStmtAttr**若要设置，并**SQLGetStmtAttr**若要获取，其他语句属性是重复的不是新功能。)  
  
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
  
-   利用**SQLGetStmtAttr**以获取以下语句属性。 (使用**SQLGetStmtAttr**以获取其他语句属性是重复的功能，不是新功能。)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   间隔 C 数据类型、 interval SQL 数据类型、 BIGINT C 数据类型和 SQL_C_NUMERIC 数据结构的使用。  
  
-   按行绑定的参数。  
  
-   例如，调用基于偏移量的书签提取**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK 和指定的偏移量 0 以外的参数。  
  
-   **SQLFetch**返回的行状态数组提取的行数，提取多个行，使用混合调用**SQLFetchScroll**，和使用进行混合调用**SQLBulkOperations**或**SQLSetPos**。 有关详细信息，请参阅下一部分中，[块状游标、 可滚动游标和 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   命名的参数。  
  
-   任何 ODBC 3。*x*的特定**SQLGetInfo**选项。 （如果检测到 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用 SQL_XXX_CURSOR_ATTRIBUTES1 信息类型，已取代多个 ODBC 2。*x*信息类型的一些信息可能可靠，但某些可能会不可靠。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)  
  
-   将绑定的偏移量。  
  
-   更新、 刷新和删除书签 (通过调用**SQLBulkOperations**)。  
  
-   调用**SQLBulkOperations**或**SQLSetPos** S5 状态中。  
  
-   诊断记录中的 ROW_NUMBER 和 COLUMN_NUMBER 字段 (其中包含要检索的替代函数**SQLGetDiagField**或**SQLGetDiagRec**)。  
  
-   近似行计数。  
  
-   警告信息 (从 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**)。  
  
-   长度可变的书签。  
  
-   扩展错误信息的数组的参数。  
  
-   所有目录函数返回的结果集中的新列。  
  
-   利用**SQLDescribeCol**并**SQLColAttribute**上第 0 列。  
  
-   使用的任何 ODBC 3。*x*的调用中的特定列属性**SQLColAttribute**。  
  
-   使用多个环境句柄。  
  
 本部分包含以下主题。  
  
-   [ODBC 3.x 应用程序的块游标、可滚动游标和后向兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
