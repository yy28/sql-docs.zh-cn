---
title: SQLSetStmtOption 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91264cee0dfceeb7195e2bad40d1638a88e1e01a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304898"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLSetStmtOption**时，调用  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 结果如下：  
  
-   如果*fOption*指示作为字符串的 ODBC 定义的语句属性，驱动程序管理器将调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值的 ODBC 定义的语句属性，则驱动程序管理器将调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句属性，则驱动程序管理器调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在前面三种情况下，**语句句柄**参数设置为*hstmt*中的值，*属性*参数设置为*fOption*中的值 *，ValuePtr*参数设置为*vParam*的值。  
  
 由于驱动程序管理器不知道驱动程序定义的语句属性是否需要字符串还是 32 位整数值，因此必须为**SQLSetStmtAttr**的*StringLength*参数传递一个有效值。 如果驱动程序为驱动程序定义的语句属性定义了特殊语义，并且需要使用**SQLSetStmtOption**调用 ，则必须支持**SQLSetStmtOption**。  
  
 如果应用程序调用**SQLSetStmtOption**在 ODBC *3.x*驱动程序中设置特定于驱动程序的语句选项，并且该选项在驱动程序的 ODBC *2.x*版本中定义，则应为 ODBC *3.x*驱动程序中的选项定义新的清单常量。 如果在调用**SQLSetStmtOption**时使用旧的清单常量，驱动程序管理器将调用**SQLSetStmtAttr，***字符串长度*参数设置为 0。  
  
 当应用程序调用**SQLSetStmtAttr**将 SQL_ATTR_USE_BOOKMARKS设置为在 ODBC *3.x*驱动程序中SQL_UB_ON时，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_FIXED。 SQL_UB_ON与SQL_UB_FIXED的常量相同。 驾驶员管理器将SQL_UB_FIXED传递给驾驶员。 SQL_UB_FIXED已在 ODBC *3.x*中弃用，但 ODBC *3.x*驱动程序必须实现它才能与使用固定长度书签的 ODBC *2.x*应用程序配合使用。  
  
 对于 ODBC *3.x*驱动程序，驱动程序管理器不再检查*选项*是否位于SQL_STMT_OPT_MIN和SQL_STMT_OPT_MAX之间，还是大于SQL_CONNECT_OPT_DRVR_START。
