---
title: SQLGetStmtOption Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2423d41b1e9c549b7202a68fb2a0e085e0a6e11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297960"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 映射
当应用程序调用**SQLGetStmtOption**到 ODBC 3 *.x*驱动程序不支持该对的调用  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 将生成按如下所示：  
  
-   如果*fOption*指示返回的字符串，该驱动程序管理器调用一个 ODBC 定义的语句选项  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值，驱动程序管理器调用一个 ODBC 定义的语句选项  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，驱动程序管理器调用  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面的三种情况下， *StatementHandle*参数设置为中的值*hstmt*，则*特性*参数设置中的值为*fOption*，并*ValuePtr*参数设置为相同的值*pvParam*。  
  
 有关 ODBC 定义的字符串连接选项，驱动程序管理器设置*BufferLength*调用中的参数**SQLGetConnectAttr**为预定义的最大长度 (SQL_MAX_OPTION_STRING_LENGTH);对于非字符串连接选项，请*BufferLength*设置为 0。  
  
 在 ODBC 3 已弃用 SQL_GET_BOOKMARK 语句选项 *.x*。 对于 ODBC 3 *.x*驱动程序以使用 ODBC 2。*x*的应用程序使用 SQL_GET_BOOKMARK，则它必须支持 SQL_GET_BOOKMARK。 对于 ODBC 3 *.x*驱动程序以使用 ODBC 2。*x*应用程序，它必须支持将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON 和应公开固定长度的书签。 如果 ODBC 3 *.x*驱动程序支持仅长度可变的书签，不固定长度的书签，则它必须返回 SQLSTATE HYC00 （未实现的可选功能） 如果 ODBC 2。*x*应用程序尝试设置 SQL_USE_BOOKMARKS 为 SQL_UB_ON。  
  
 对于 ODBC 3 *.x*驱动程序，驱动程序管理器不再检查以查看是否*选项*介于 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，或者大于 SQL_CONNECT_OPT_DRVR_START。 该驱动程序必须选中此项。
