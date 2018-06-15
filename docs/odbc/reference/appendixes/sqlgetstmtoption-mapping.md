---
title: SQLGetStmtOption 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02eaacbe3503b5d93677633aa0e98326b14e304f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907382"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 映射
在应用程序调用**SQLGetStmtOption**为 ODBC 3 *.x*驱动程序不支持它，对的调用  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 将导致，如下所示：  
  
-   如果*fOption*指示返回的字符串，驱动程序管理器调用 ODBC 定义语句选项  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示返回一个 32 位整数值，驱动程序管理器调用 ODBC 定义语句选项  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，驱动程序管理器调用  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面的三种情况下， *StatementHandle*参数设置中的值为*hstmt*、*属性*参数设置中的值为*fOption*，和*ValuePtr*参数设置为相同的值*pvParam*。  
  
 有关 ODBC 定义的字符串连接选项，驱动程序管理器设置*BufferLength*对的调用中的自变量**SQLGetConnectAttr**的预定义的最大长度 (SQL_MAX_OPTION_STRING_LENGTH);对于非字符串连接选项， *BufferLength*设置为 0。  
  
 SQL_GET_BOOKMARK 语句选项已弃用 ODBC 3 中 *.x*。 ODBC 3 *.x*驱动程序以使用 ODBC 2。*x*应用程序使用 SQL_GET_BOOKMARK，则它必须支持 SQL_GET_BOOKMARK。 ODBC 3 *.x*驱动程序以使用 ODBC 2。*x*应用程序，它必须支持将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON 和应公开固定长度书签。 如果 ODBC 3 *.x*驱动程序还支持仅长度可变的书签，不固定长度书签，则它必须返回 SQLSTATE HYC00 （未实现的可选功能） 如果 ODBC 2。*x*应用程序尝试设置 SQL_USE_BOOKMARKS 为 SQL_UB_ON。  
  
 ODBC 3 *.x*驱动程序，驱动程序管理器将不再检查以查看是否*选项*SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，之间或大于 SQL_CONNECT_OPT_DRVR_START。 该驱动程序必须选中此项。
