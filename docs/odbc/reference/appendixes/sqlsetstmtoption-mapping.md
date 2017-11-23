---
title: "SQLSetStmtOption 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e70f226277b3ad4932756095a8ebc2f3121ee0d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 映射
在应用程序调用**SQLSetStmtOption**到 ODBC 3*.x*驱动程序，将会调用  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 将导致，如下所示：  
  
-   如果*fOption*指示是一个字符串，驱动程序管理器调用 ODBC 定义语句属性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回一个 32 位整数值，驱动程序管理器调用 ODBC 定义语句属性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义语句特性，则驱动程序管理器调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在前面的三种情况下， **StatementHandle**参数设置中的值为*hstmt*、*属性*参数设置中的值为*fOption*，和*ValuePtr*参数设置为的值*vParam*。  
  
 驱动程序管理器不知道驱动程序定义的语句属性需要字符串或 32 位整数值，因此可以传递中的有效值*StringLength*参数**SQLSetStmtAttr**. 如果该驱动程序已定义的驱动程序定义的语句属性了特殊语义，并且需要使用来调用**SQLSetStmtOption**，则它必须支持**SQLSetStmtOption**。  
  
 如果应用程序调用**SQLSetStmtOption**在 ODBC 3 中设置特定于驱动程序的语句选项*.x*驱动程序和选项已在 ODBC 2 中定义。*x*应为 ODBC 3 中的选项定义版本的驱动程序，新的清单常量*.x*驱动程序。 如果在调用中使用旧的清单常量**SQLSetStmtOption**，驱动程序管理器将调用**SQLSetStmtAttr**与*StringLength*参数设置为 0。  
  
 在应用程序调用**SQLSetStmtAttr**将 SQL_ATTR_USE_BOOKMARKS 设置为在 ODBC 3 SQL_UB_ON*.x*驱动程序，SQL_ATTR_USE_BOOKMARKS 语句特性设置为 SQL_UB_FIXED。 SQL_UB_ON 是作为 SQL_UB_FIXED 相同的常量。 驱动程序管理器将通过 SQL_UB_FIXED 传递给该驱动程序。 ODBC 3 中已弃用 SQL_UB_FIXED*.x*，但 ODBC 3*.x*驱动程序必须实现它以使用 ODBC 2。*x*使用固定长度书签的应用程序。  
  
 ODBC 3*.x*驱动程序，驱动程序管理器不再将检查以查看*选项*SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，之间或大于 SQL_CONNECT_OPT_DRVR_START。
