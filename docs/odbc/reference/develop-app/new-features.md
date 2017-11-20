---
title: "新增功能 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e2b48097b6c398772e14d2594a583d89e6825e0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="new-features"></a>新功能
ODBC 3 中引入了以下新功能。*x*。 一个 ODBC 3。*x*应用程序使用 ODBC 2*.x*驱动程序将不能使用此功能。 ODBC 3。*x*驱动程序管理器使用 ODBC 2 时不将这些功能*.x*驱动程序。  
  
-   采用一个说明符的函数处理作为自变量： **SQLSetDescField**， **SQLGetDescField**， **SQLSetDescRec**， **SQLGetDescRec**，和**SQLCopyDesc**。  
  
-   函数**SQLSetEnvAttr**和**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**分配的描述符句柄。 (使用**SQLAllocHandle**分配环境、 连接和语句的句柄是重复的、 不是新功能。)  
  
-   使用**SQLGetConnectAttr**获取 SQL_ATTR_AUTO_IPD 连接属性。 (使用**SQLSetConnectAttr**若要设置，和**SQLGetConnectAttr**若要获取，其他连接属性是重复的、 不是新功能。)  
  
-   使用**SQLSetStmtAttr**若要设置，和**SQLGetStmtAttr**若要获取，以下语句属性。 (使用**SQLSetStmtAttr**若要设置，和**SQLGetStmtAttr**若要获取，其他语句属性是重复的、 不是新功能。)  
  
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
  
-   使用**SQLGetStmtAttr**以获取以下语句属性。 (使用**SQLGetStmtAttr**以获取其他语句属性是重复的功能，不是新功能。)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用间隔 C 数据类型、 间隔 SQL 数据类型、 BIGINT C 数据类型和 SQL_C_NUMERIC 数据结构。  
  
-   按行绑定的参数。  
  
-   基于偏移量的书签提取，例如，调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK 和指定的偏移量 0 以外的参数。  
  
-   **SQLFetch**返回行状态数组，提取的行数，读取多行，与混合调用**SQLFetchScroll**，并使用混合调用**SQLBulkOperations**或**SQLSetPos**。 有关详细信息，请参阅下一部分中，[块状游标可滚动游标，对于 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   命名的参数。  
  
-   任何 ODBC 3。*x*– 特定**SQLGetInfo**选项。 （如果检测到 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序将调用具有替代几个 ODBC 2 的 SQL_XXX_CURSOR_ATTRIBUTES1 信息类型。*x*信息类型的某些信息可能可靠，但一些可能是不可靠。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)  
  
-   将绑定偏移量。  
  
-   更新、 刷新，以及删除书签 (通过调用**SQLBulkOperations**)。  
  
-   调用**SQLBulkOperations**或**SQLSetPos** S5 状态中。  
  
-   中的诊断记录的方式和 COLUMN_NUMBER 字段 (其中包含要由替换函数检索**SQLGetDiagField**或**SQLGetDiagRec**)。  
  
-   近似的行计数。  
  
-   警告信息 (从 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**)。  
  
-   长度可变的书签。  
  
-   扩展的错误信息的数组的参数。  
  
-   所有中由目录函数返回的结果集的新列。  
  
-   利用**SQLDescribeCol**和**SQLColAttribute**列 0。  
  
-   使用任何 ODBC 3。*x*– 对的调用中的特定列属性**SQLColAttribute**。  
  
-   使用多个环境句柄。  
  
 本部分包含以下主题。  
  
-   [块状游标可滚动游标，对于 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)

