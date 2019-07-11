---
title: SQLSetStmtOption Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5284fd0065e3d1b2c23725a05b71dbb5d2f0810b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793001"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 映射
当应用程序调用**SQLSetStmtOption**通过 ODBC *3.x*驱动程序，将会调用  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 将生成按如下所示：  
  
-   如果*fOption*指示是一个字符串，该驱动程序管理器调用 ODBC 定义的语句属性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值，驱动程序管理器调用 ODBC 定义的语句属性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句属性，驱动程序管理器调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在前面的三种情况下， **StatementHandle**参数设置为中的值*hstmt*，则*特性*参数设置中的值为*fOption*，并*ValuePtr*参数设置为的值*vParam*。  
  
 驱动程序管理器不知道驱动程序定义的语句属性需要字符串或 32 位整数值，因为它必须是有效的值传入*StringLength*自变量的**SQLSetStmtAttr**. 如果该驱动程序具有定义驱动程序定义的语句属性的特殊语义，并且需要使用调用**SQLSetStmtOption**，则它必须支持**SQLSetStmtOption**。  
  
 如果应用程序调用**SQLSetStmtOption**若要在 ODBC 中设置特定于驱动程序的语句选项*3.x*驱动程序和选项已在 ODBC 中定义*2.x*的版本驱动程序，应为 ODBC 中的选项定义新的清单常量*3.x*驱动程序。 如果在调用中使用旧清单常量**SQLSetStmtOption**，驱动程序管理器将调用**SQLSetStmtAttr**与*StringLength*参数设置为 0。  
  
 当应用程序调用**SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS 设在 ODBC 中的 SQL_UB_ON *3.x*驱动程序，SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_FIXED。 SQL_UB_ON 是作为 SQL_UB_FIXED 相同的常量。 驱动程序管理器将通过 SQL_UB_FIXED 传递给驱动程序。 ODBC 中已弃用 SQL_UB_FIXED *3.x*，但 ODBC *3.x*驱动程序必须实现它以使用 ODBC *2.x*使用定长书签的应用程序。  
  
 用于 ODBC *3.x*驱动程序，驱动程序管理器不再检查以查看是否*选项*介于 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，或者大于 SQL_CONNECT_OPT_DRVR_START。
